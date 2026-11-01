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

- Somente conexões pelas seis faces entre Copycats do mesmo tipo participam; diagonais não conectam blocos.
- Aplicar segue alvos vazios elegíveis; substituir/remover segue o material clicado. Outros materiais permanecem intactos, inclusive em formatos multipartes.
- O limite padrão do servidor é **64 posições**, incluindo a origem, ajustável de **1 a 256**. Um bloco multiparte conta uma posição.
- Survival usa a pilha na mão escolhida e para quando ela acaba. Não repõe material de outras pilhas do inventário.
- Chunks descarregados ficam fora. Posições recusadas pelas permissões de interação ou edição do servidor ficam fora e não propagam a ação por aquele caminho.
- O preview desconhece claims do servidor, então o resultado pode ser menor que a estimativa. Uma conexão alternativa permitida pode alcançar uma posição além do caminho bloqueado.

[Configurações](configuration) explica como ajustar o limite. Segure **Sneak** para usar a ação normal da wrench do Create.
