---
title: "Changelog de Aeronautics: Fly by Instruments"
description: "Histórico de versões de Aeronautics: Fly by Instruments."
---

# Changelog de Aeronautics: Fly by Instruments

## [0.3.0] - 2026-11-01

### Adicionado

- Adicionados onze tutoriais Ponder em inglês e português brasileiro para sensores, fios, painéis de cockpit e navegação FMS.

### Alterado

- Removida a marca Experimental dos blocos e módulos aviônicos; a Network Bridge continua Experimental e exclusiva do criativo.

### Corrigido

- Corrigidos fios que continuavam conectados ou visíveis após remover um conector ou suporte.
- Corrigida a devolução duplicada de fios ao remover seus nós.
- Corrigido o Advanced Terrain Scanner emitindo sinais de redstone pelas faces erradas.
- Corrigidos buzzers do mesmo canal do painel tocando fora de sincronia.
- Corrigidas lâmpadas acesas do painel sendo encobertas pelo céu e pelas nuvens com shaders.
- Corrigida a dica do buzzer para explicar o silenciamento e a configuração com Shift + clique.

## [0.2.0] - 2026-10-28

Um conjunto aviônico experimental: um computador de alerta de proximidade do solo, um painel de cockpit e fios físicos.

### Adicionado

- Adicionado o Avionics Computer, um sistema experimental de alerta de proximidade do solo que lê os sensores e avisa sobre terreno à frente, pull up, razão de descida, perda de altitude, voo baixo demais e inclinação excessiva.
- Adicionada uma tela de estado ao Avionics Computer com os papéis dos sensores, a sensibilidade, a inibição de cada função e um botão de autoteste.
- Adicionado o Avionics Wire experimental, com Wire Connectors de latão e Wire Supports de ferro, que pende entre os dispositivos para ligá-los.
- Adicionada a Wiring View, ligada com V, que mostra todos os fios através dos blocos, coloridos pelo estado da rede.
- Adicionado o corte de um único fio com a Wrench do Create na Wiring View.
- Adicionada a opção "Olha para" nos Terrain Scanners, que diz ao Avionics Computer qual lado da nave cada um vigia.
- Adicionadas Modular Tables unidas: mesas lado a lado formam um painel, e módulos podem ocupar várias mesas.
- Adicionado o acoplamento: uma Modular Table montada num Avionics Computer entra na rede dele sem fio.
- Adicionadas as indicações das lâmpadas (alerta GPWS, atenção, INOP ou uma função) e lâmpadas âmbar.
- Adicionado o silenciamento do alarme ao clicar numa lâmpada acesa ou buzzer tocando; Shift + clique no buzzer abre sua configuração.
- Adicionada uma bússola de proa na tela do FMS, que marca o waypoint selecionado.
- Adicionado o vínculo de uma FMS Compass com um clique pela tela do FMS.
- Adicionada luz de bloco das lâmpadas acesas da mesa.
- Adicionadas receitas para Avionics Computer, Modular Table, lâmpadas, buzzer, FMS, FMS Compass, Avionics Wire, Wire Connector e Wire Support; a Network Bridge continua exclusiva do criativo.
- Adicionadas dicas no estilo do Create com resumo ao segurar Shift para todos os blocos e módulos.

### Alterado

- Alterada a tela dos sensores para um novo layout em que as mudanças aplicam na hora, com um novo seletor de frequência do Redstone Link.
- Alterado o visual da Modular Table, das lâmpadas, do buzzer, do FMS e dos blocos aviônicos experimentais para o estilo do Create.
- Alterada a tela do FMS para um painel único, com destino, distância e rumo no topo e seleção direta de waypoints (clique direito para editar).
- Alterados novos waypoints para começarem na posição atual com o nome pronto para digitar; excluir agora pede um segundo clique.
- Renomeado o item Flight Management System Module para FMS.
- Alterada a Modular Table Base para 4 pixels de espessura, então os módulos ficam 1 pixel mais altos.
- Alterada a versão exigida do R-UI Lib para 0.8.0 ou mais recente.

### Removido

- Removido o GPWS Computer, que agora carrega como Avionics Computer e mantém só a sensibilidade.
- Removidos os perfis, modos e regras próprias de alerta do GPWS.
- Removido o peripheral `gpws` do CC:Tweaked; programas precisam usar `avionics_computer`.
- Removido `cableCount` do estado da Network Bridge e do Avionics Computer no CC:Tweaked.
- Removido o bloco Avionics Cable experimental; use Avionics Wire para ligar os dispositivos. Cabos já colocados desaparecem ao carregar o mundo.

## [0.1.0] - 2026-10-25

Primeiro lançamento, com foco em sensores de voo para Create Aeronautics.

### Adicionado

- Adicionado o Radar Altimeter, que mede a altura da nave em relação ao terreno abaixo.
- Adicionado o Terrain Scanner, que detecta obstáculos à frente da nave.
- Adicionado o Advanced Terrain Scanner, que monitora frente, esquerda e direita separadamente com campo de visão ajustável.
- Adicionado um sinal de redstone para cada sensor, crescente com a altitude ou com a proximidade de obstáculos.
- Adicionada uma tela de configuração da faixa do sinal e de transmissão sem fio pelo Redstone Link.
- Adicionado suporte a CC:Tweaked para computadores lerem o que cada sensor detecta.
- Adicionadas receitas para criar os três sensores com componentes do Create.
- Adicionado suporte a sensores instalados em naves Aeronautics em movimento.
- Adicionadas configurações de servidor para alcance dos sensores e frequência de atualização.
- Adicionados instrumentos em desenvolvimento, marcados como Experimental na aba criativa e sem receitas.

O [CHANGELOG no repositório](https://github.com/radaelilucca/mc-fly-by-instruments/blob/main/CHANGELOG.md) é o registro oficial das versões.
