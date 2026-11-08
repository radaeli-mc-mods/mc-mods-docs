---
title: Instalação e uso
description: "Instale Create: On Demand e solicite produtos à sua fábrica do Create."
---

# Instalação e uso

## Requisitos

- **Minecraft 1.20.1:** Forge **47.4.0** ou posterior e Create **6.0.8**.
- **Minecraft 1.21.1:** NeoForge **21.1.236** ou posterior e Create **6.0.10**.
- Instale o JAR correspondente do Create: On Demand no cliente e no servidor.

## Prepare a fábrica

1. Configure receitas nos Factory Gauges e conecte os gauges dos ingredientes.
2. Deixe os gauges em **Maintain stock and accept orders** para publicar suas receitas para pedidos. Gauges novos já usam esse modo. Escolha **Maintain stock** nos gauges que não devem aceitar pedidos; o slider de estoque normal continua funcionando.
3. Monte e ligue as máquinas. Direcione os ingredientes aos endereços de processamento e devolva os produtos prontos ao armazenamento monitorado pela rede do gauge produtor.

Create: On Demand segue as conexões configuradas nos gauges. Ele não descobre receitas pelo JEI, não monta nem liga máquinas, não transporta itens e não carrega chunks.

## Solicite um produto

1. Abra o **Stock Keeper** e escolha **All** ou **Craftable**. Produtos fabricáveis aparecem com uma marca verde, inclusive quando estão sem estoque.
2. Clique em um produto fabricável sem estoque. Para pedir uma nova fabricação mesmo havendo estoque, use **Ctrl + clique esquerdo**.
3. Escolha a quantidade e confira a prévia. Ela lista **Items to craft** na ordem de produção ou **Missing materials** quando faltam recursos.
4. Confirme. Um pedido sem todos os materiais aguarda a reposição. No painel **Orders**, acompanhe o trabalho ativo ou cancele um pedido.

A quantidade solicitada representa novos produtos finais. Lotes de receitas podem gerar excedentes, que ficam armazenados. Ingredientes já disponíveis são reaproveitados. Cancelar interrompe o trabalho ainda não enviado; não recupera ingredientes em trânsito.

## Entregue um pedido

Preencha um endereço no Stock Keeper antes de confirmar o pedido. Quando a quantidade solicitada voltar à rede produtora, Packagers enviam exatamente essa quantidade ao endereço salvo, possivelmente em várias caixas. O excedente fica armazenado. O painel Orders mostra o destino e o progresso do empacotamento. Sem endereço, os produtos prontos permanecem no estoque.

## Configurações

O mod não possui arquivos de configuração editáveis. O modo de pedidos é escolhido na tela de receita de cada Factory Gauge; consulte [Configurações](configuration) para detalhes.
