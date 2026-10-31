---
title: Vínculo
description: Vincule um upgrade remoto ao AE2, Refined Storage ou Tom's Simple Storage.
---

# Vínculo

Cada upgrade remoto guarda seu próprio vínculo com um ponto da rede. Os oito tipos usam o mesmo método: podem se conectar ao Applied Energistics 2, Refined Storage ou Tom's Simple Storage. Com SCC 1.5.3 ou mais recente no NeoForge 1.21.1, também podem se conectar ao Super Cool Calculator. Não é preciso obter uma variante do upgrade para cada rede.

## Vincular um upgrade

1. Faça o upgrade remoto que deseja usar.
2. Segure-o em qualquer uma das mãos.
3. Dê **Shift + clique direito** em um bloco compatível da rede desejada:
   - **AE2:** ME Wireless Access Point.
   - **Refined Storage:** Controller.
   - **Tom's Simple Storage:** Storage Terminal.
   - **SCC (somente NeoForge 1.21.1):** Network Antenna.
4. Uma mensagem confirma quando o vínculo é salvo. Coloque o upgrade em um slot de upgrade da mochila e abra sua aba para configurá-lo.

## Como fica um upgrade vinculado

O upgrade muda de aparência conforme o vínculo, nos slots, na mão e no mundo:

- **Sem vínculo:** tela verde, com o ícone do upgrade nas cores originais.
- **Vinculado:** tela escura, e o ícone assume a cor da rede: roxo para Applied Energistics 2, azul para Refined Storage, carvalho para Tom's Simple Storage e dourado para Super Cool Calculator.
- **Quinas:** as quatro quinas sempre mostram as redes compatíveis, uma em cada (AE2 em cima à esquerda, SCC em cima à direita, Tom's Simple Storage embaixo à esquerda, Refined Storage embaixo à direita).

Ao vincular, toca uma animação curta: a cor da rede corre pelo aro a partir da quina dela, varre a tela e assenta. Trocar para outra rede toca a mesma animação a partir do visual da rede anterior. Desvincular pela criação volta direto ao visual verde, sem animação.

<img src="https://raw.githubusercontent.com/radaelilucca/mc-sophisticated-backpacks-digital-storage/main/docs/gallery/upgrade_link_states.png" alt="Remote Feeding Upgrade sem vínculo e vinculado ao Applied Energistics 2, Refined Storage, Tom's Simple Storage e Super Cool Calculator" width="420">

O jogador precisa ter permissão para interagir com o bloco e acessar a rede. A disponibilidade da rede, o alcance sem fio e as permissões continuam sob controle do mod de armazenamento. O upgrade não cria acesso sem fio nem contorna essas regras.

## Trocar ou remover o vínculo

Para trocar de rede, segure o upgrade e dê Shift + clique direito em um bloco compatível da nova rede. O novo ponto substitui o antigo; filtros e outras configurações permanecem no upgrade.

Para desvincular sem perder as configurações, coloque o upgrade sozinho em uma grade de criação. Isso remove o ponto da rede. A criação ou a troca de vínculo fica temporariamente bloqueada enquanto houver itens ou fluidos aguardando recuperação; recupere-os primeiro.

O upgrade pode indicar que a rede está indisponível se o mod de integração estiver ausente, o ponto estiver descarregado ou não existir, a dimensão estiver indisponível ou o acesso for negado. O vínculo é mantido se o mod da rede estiver ausente.
