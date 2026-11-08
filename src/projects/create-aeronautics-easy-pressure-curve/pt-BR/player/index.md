---
title: Instalação e uso
description: "Instale o Create: Aeronautics Easy Pressure Curve e altere a curva de pressão do ar com /pressurecurve."
---

# Instalação e uso

## Requisitos

- Minecraft **1.21.1** com NeoForge **21.1.236** ou mais recente.
- **Sable** 2.0.5 ou mais recente (obrigatório).
- **R-Ui Lib** 0.10.0 ou mais recente nos clientes que instalarem o mod (para a tela do editor).
- **Create Aeronautics** 1.3 ou mais recente (opcional: é um dos mods que leem a curva).
- Instale o mod no servidor (obrigatório). No cliente ele é opcional e serve só para o editor; nesse caso o cliente precisa do R-Ui Lib, e o servidor não.

## Como a curva funciona

O Sable calcula a pressão do ar em função da altitude (Y do mundo), definida por pontos: cada um tem `altitude`, um `value` de pressão e um `slope`. O Create Aeronautics lê essa pressão para balões, hélices, tooltips do burner e do steam vent e o Altitude Sensor; alterar a curva muda o comportamento deles.

Uma curva definida por este mod:

- vale na hora no servidor e para todos os jogadores, inclusive os que entram depois;
- é salva com o mundo e continua após reabrir o mundo, reiniciar o servidor e usar `/reload`;
- vence o datapack naquela dimensão até você fazer o reset;
- substitui apenas a pressão; gravidade, arrasto e o resto continuam vindo do datapack.

O `value` de cada ponto é a **pressão real**: a curva definida substitui o `base_pressure` do datapack. Como referência, a curva usual do Overworld vale 1.0 em Y=63.

## Editar a curva em um gráfico

Aperte **F9** no jogo para abrir o editor da curva (mude a tecla em **Opções → Controles → Teclas → Aeronautics Easy Pressure Curve**). Ele abre na dimensão em que você está, e um dropdown no topo permite escolher qualquer outra dimensão. Ele abre já preenchido com a curva em vigor e seus pontos. A curva embutida do Sable aparece ao fundo para comparação.

- **Arraste um ponto** para movê-lo e **arraste as alças** para mudar a inclinação ali.
- **Clique duas vezes** no gráfico para adicionar um ponto e **clique com o botão direito** em um ponto (ou aperte Delete) para removê-lo. As setas movem o ponto selecionado.
- **Y máx.** e **Pressão máx.** escolhem quanto do gráfico você vê e até onde os pontos podem ir.
- **Aplicar** envia a curva ao servidor, que a salva e a aplica para todos os jogadores. **Desfazer** descarta suas edições não salvas. **Voltar ao datapack** remove a curva do mod na dimensão. **Fechar** sai da tela.

Só operadores (nível 2) abrem o editor; para os demais jogadores a tecla não faz nada e fica livre para outras ações. As altitudes são ajustadas para blocos inteiros e as pressões para centésimos.

## Definir uma curva com comandos

É preciso ser operador (nível 2). Execute os comandos na dimensão que quer alterar ou acrescente a dimensão no final.

1. Veja a curva atual: `/pressurecurve show`. Ele lista cada ponto com seu índice e informa se a curva vem do mod ou do datapack.
2. Defina uma nova com `/pressurecurve set <dimension> <json>`:

   ```text
   /pressurecurve set minecraft:overworld [{"altitude":0,"value":2.0,"slope":0.0},{"altitude":1000,"value":0.2,"slope":0.0}]
   ```

3. Confira o resultado com `/pressurecurve sample 500`. Com a curva acima, o resultado é `1.10000`.

## Comandos

| Comando | O que faz |
| --- | --- |
| `/pressurecurve show [dimension]` | Lista os pontos e informa se a curva é do mod ou do datapack. |
| `/pressurecurve sample <altitude> [dimension]` | Pressão naquela altitude, como o jogo a calcula. |
| `/pressurecurve set <dimension> <json>` | Substitui a curva pela lista de pontos informada. |
| `/pressurecurve point add <altitude> <value> <slope> [dimension]` | Adiciona um ponto à curva atual. |
| `/pressurecurve point remove <index> [dimension]` | Remove um ponto; o primeiro é o `0`. |
| `/pressurecurve copy-datapack [dimension]` | Transforma a curva do datapack em uma curva editável do mod. |
| `/pressurecurve reset [dimension]` | Remove a sua curva; a dimensão volta ao datapack. |

A dimensão padrão é a de quem executa o comando (o Overworld, pelo console). `point add` e `point remove` partem da curva em vigor, seja a sua ou a do datapack.

## Regras da curva

- De 1 a 64 pontos.
- Cada `altitude` é diferente (os pontos podem vir em qualquer ordem; eles são ordenados).
- `altitude`, `value` e `slope` são números finitos, e `value` não é negativo.

Um comando que quebra uma regra ou tem JSON inválido é rejeitado com uma mensagem e não altera nada.

## Cenário: rarefazer o ar para uma nave em grande altitude

1. `/pressurecurve copy-datapack` transforma a curva atual em uma curva editável.
2. `/pressurecurve point add 400 0.05 0` adiciona uma camada muito rarefeita em Y=400.
3. `/pressurecurve sample 400` informa a nova pressão, que tudo o que lê a pressão do ar do Sable passa a usar na hora.
4. `/pressurecurve reset` traz de volta a curva do datapack.

## Solução de problemas

- **O comando não existe ou é negado:** ele exige operador nível 2, e o mod precisa estar instalado junto com o Sable.
- **Jogadores ainda veem os valores antigos:** rode antes `/pressurecurve show` e `/pressurecurve sample` no servidor; o mod só precisa estar no servidor, os clientes recebem a curva pelo Sable. Não é preciso reconectar.
- **Meu `base_pressure` parece ignorado:** é o esperado em dimensões com curva deste mod; coloque o valor final em cada ponto.

Veja [Configurações](configuration) para saber o que controla o mod.
