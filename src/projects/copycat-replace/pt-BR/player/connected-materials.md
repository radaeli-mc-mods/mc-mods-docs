---
title: Materiais conectados
description: Aplique, substitua ou remova materiais em Copycats do mesmo tipo conectados por faces.
---

# Materiais conectados

Segure **Bulk Action on Connected Copycats** ao clicar com o botão direito. O padrão é **Left Alt**, remapeável em **Controls**. O HUD mostra uma estimativa local e destaca as posições selecionadas.

| Ação | Mãos | Alvo |
| --- | --- | --- |
| Aplicar | Wrench e material | Copycat vazio |
| Substituir | Wrench e novo material | Copycat com o material a substituir |
| Remover | Apenas wrench; outra mão vazia | Copycat com o material a remover |

Por exemplo, coloque quatro Copycats do mesmo tipo conectados por faces, segure uma wrench e quatro blocos de pedra e clique no grupo vazio segurando a tecla. Até quatro posições recebem pedra, conforme limite e permissões do servidor. Repita com outro material para substituir a pedra. Esvazie a mão do material para remover o material clicado do grupo.

## Seleção e limites

Segure a tecla de ação e role a roda do mouse para alternar o modo sem trocar o slot da hotbar. O HUD mostra o modo ativo. Solte a tecla para devolver à roda a troca normal de slots. O modo é lembrado nesta conexão; reconectar volta a Conectado.

| Modo | Seleção |
| --- | --- |
| Conectado | Conexões pelas seis faces entre Copycats do mesmo tipo |
| Plano | Mesmo tipo, no plano que passa pela origem e é perpendicular à face clicada |
| Todos os tipos | Conexões pelas seis faces entre quaisquer tipos de Copycat suportados |

Para uma parede, clique na face frontal em Plano para ficar naquela camada. Para um piso, clique na face superior. Diagonais nunca conectam blocos.

- Aplicar segue alvos vazios elegíveis; substituir/remover segue o material clicado. Outros materiais permanecem intactos, inclusive em formatos multipartes.
- O limite padrão do servidor é **64 posições**, incluindo a origem, ajustável de **1 a 256**. Um bloco multiparte conta uma posição.
- Survival consome primeiro a pilha da mão escolhida, depois itens idênticos do inventário principal (hotbar e armazenamento). Tags/componentes precisam coincidir; armadura e outra mão ficam fora. Isso está sempre ativo nas ações em grupo, sem configuração adicional. Estoque insuficiente altera somente as posições que podem ser pagas. Creative não consome.
- Chunks descarregados ficam fora. Posições recusadas pelas permissões de interação ou edição do servidor ficam fora e não propagam a ação por aquele caminho.
- O preview desconhece claims do servidor, então o resultado pode ser menor que a estimativa. Uma conexão alternativa permitida pode alcançar uma posição além do caminho bloqueado.

[Configurações](configuration) explica como ajustar o limite. Segure **Sneak** para usar a ação normal da wrench do Create.

Um material recusado mostra uma mensagem curta acima da hotbar. Uma ação negada, um material já igual ou uma pilha esgotada não produz aviso de material inválido.

Por exemplo, segure um bloco de ouro e deixe outros 64 idênticos no inventário principal: um grupo permitido pode usar os 65, até o limite de posições configurado. Devoluções durante essa ação não aumentam seu orçamento inicial. Trocas individuais continuam usando somente a pilha da mão.

Em formatos multipartes, aplicar seleciona uma parte pela face clicada e pelas mesmas coordenadas relativas do clique em cada posição, inclusive entre formatos diferentes. Substituir/remover segue todas as partes existentes com o material clicado em cada posição selecionada. Outros materiais permanecem intactos.
