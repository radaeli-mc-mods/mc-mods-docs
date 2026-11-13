---
title: Configurações
description: Arquivo de configuração do cliente e opção de visibilidade do Remote Crafting.
---

# Configurações

Digital Storage Expansion oferece um arquivo de configuração do cliente no Forge 1.20.1 e NeoForge 1.21.1 / 26.1.2. Ele se aplica somente ao cliente onde está salvo.

## Arquivo do cliente

- **Arquivo:** config/sophisticated_backpacks_digital_storages_expansion-client.toml
- **Formato:** TOML
- **Quem é afetado:** o cliente onde o arquivo está salvo; as configurações do servidor não mudam.
- **Finalidade:** controla se o seletor manual de receitas do Remote Crafting e o botão **Buscar ingredientes** aparecem.

```toml
[crafting]
	#Controls when the recipe selector and Fetch ingredients button are shown.
	#Allowed Values: AUTO, SHOW, HIDE
	manualControls = "AUTO"
```

### crafting.manualControls

| Tipo | Padrão | Valores aceitos | Efeito |
| --- | --- | --- | --- |
| Enum | AUTO | AUTO, SHOW, HIDE | AUTO mostra os controles manuais, exceto quando a transferência do JEI está pronta para a tela da mochila aberta. SHOW sempre os exibe. HIDE sempre os oculta. |

O botão na aba Remote Crafting salva uma escolha explícita SHOW ou HIDE. Para restaurar o comportamento automático, defina manualControls como AUTO neste arquivo. A opção não altera a grade de crafting, a receita selecionada, o resultado, a prioridade de origem nem o reabastecimento.

Filtros, prioridade de origem e outras opções funcionais são salvos em cada item de upgrade e alterados pela aba da mochila. Consulte [Filtros e prioridade de origem](filters), o [catálogo de upgrades](upgrades) e o [guia de Remote Crafting](crafting).

Remote Pump usa configurações de bomba do Sophisticated Backpacks para os slots de filtros de fluidos e o cálculo de vazão. Essas opções pertencem ao Sophisticated Backpacks, não a este addon; consulte a documentação desse mod para a localização e o comportamento do arquivo.
