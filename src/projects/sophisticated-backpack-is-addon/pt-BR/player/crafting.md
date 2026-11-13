---
title: Remote Crafting
description: Escolha uma receita e preencha a bancada da mochila com os itens disponíveis.
---

# Remote Crafting

O upgrade Remote Crafting substitui o Crafting Upgrade comum na mochila. Abra a aba, escolha uma receita e clique em **Buscar ingredientes**. Itens compatíveis que já estão na grade 3×3 permanecem no lugar; o upgrade preenche os espaços restantes com itens da mochila e, quando há vínculo, da rede. O botão **+** busca na rede vinculada os ingredientes que faltarem, quando disponível. A grade, o resultado e os recipientes devolvidos usam a tela de crafting normal do Sophisticated Backpacks.

## Usar um visualizador de receitas

Com JEI instalado, use o botão de transferência de receitas enquanto a tela da mochila estiver aberta. Um clique normal transfere uma execução. Segure **Shift** para preencher pilhas com o maior número de execuções completas permitido pelos itens e pelos slots da grade. Se o estoque não for suficiente para um lote completo, o upgrade ainda preenche o que conseguir para uma receita.

Quando o upgrade está vinculado, a transferência do JEI pode usar a mochila, a rede vinculada e o inventário principal do jogador. Sem vínculo com uma rede, a transferência normal do Sophisticated Backpacks continua disponível.

Com **Refill crafting grid** habilitado no Sophisticated Backpacks, o crafting tenta primeiro as fontes locais e depois busca na rede vinculada o ingrediente consumido, se necessário.

## Mostrar ou ocultar controles manuais

A aba tem um botão **Mostrar controles manuais** / **Ocultar controles manuais**. Ele oculta ou mostra o seletor de receitas e o botão **Buscar ingredientes** sem alterar a receita selecionada, a grade, o resultado, a prioridade de origem ou o reabastecimento.

A opção crafting.manualControls em [Configurações](configuration) controla a visibilidade padrão:

| Valor | Comportamento |
| --- | --- |
| AUTO | Mostra os controles manuais, exceto quando a transferência do JEI está pronta para a tela da mochila aberta. |
| SHOW | Sempre mostra o seletor de receitas e **Buscar ingredientes**. |
| HIDE | Sempre oculta o seletor de receitas e **Buscar ingredientes**. |

O botão da aba salva SHOW ou HIDE. Para voltar a AUTO, defina esse valor no arquivo de configuração do cliente.
