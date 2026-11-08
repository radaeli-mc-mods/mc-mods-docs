---
title: Configurações
description: Limite de ações, localização dos arquivos e recarga.
---

# Configurações

O administrador do servidor ou dono do mundo singleplayer edita **copycat_replace-server.toml** (TOML). O limite controla as ações conectadas do mundo e é enviado aos clientes para o preview. Não há config própria de cliente nem opções adicionais de proteção do addon.

## Localização dos arquivos

| Variante | Arquivo ativo |
| --- | --- |
| Forge 1.20.1 / 47.4.0 | `<servidor>/<mundo>/serverconfig/copycat_replace-server.toml`, gerado ao carregar o mundo. Em singleplayer: `saves/<mundo>/serverconfig/`. |
| Fabric 1.20.1 | `config/copycat_replace-server.toml` por padrão, gerado ao iniciar o servidor ou mundo. Com `forceGlobalServerConfigs` desativado em `config/forgeconfigapiport.toml`, use a pasta `serverconfig/` do mundo. |
| NeoForge 1.21.1 / 21.1.236 | `config/copycat_replace-server.toml`, gerado ao carregar a configuração SERVER. Um arquivo existente em `<mundo>/serverconfig/copycat_replace-server.toml` tem precedência para aquele mundo. Em singleplayer: `saves/<mundo>/serverconfig/`. |

Para um limite próprio de mundo no NeoForge, pare o servidor ou feche o mundo, copie a base para o serverconfig daquele mundo, edite a cópia e abra o mundo novamente. Mundos sem override usam a base compartilhada. Criar override com o mundo aberto tem efeito no próximo carregamento. No Forge, `defaultconfigs/copycat_replace-server.toml` pode servir de modelo para novos arquivos de mundo; não substitui a configuração de um mundo existente.

## Padrão completo

Padrão gerado no Forge e no Fabric.

```toml
#Maximum connected Copycat positions affected by one bulk action (1-256).
#Range: 1 ~ 256
max_connected_blocks = 64
```

Padrão gerado no NeoForge:

```toml
#Maximum connected Copycat positions affected by one bulk action (1-256).
# Default: 64
# Range: 1 ~ 256
max_connected_blocks = 64
```

## Schema

| Chave | Tipo | Padrão | Valores aceitos | Efeito |
| --- | --- | --- | --- | --- |
| `max_connected_blocks` | Inteiro | 64 | 1–256 inclusive, em posições de blocos | Máximo de posições por ação conectada de aplicar, substituir ou remover, incluindo a origem. Um bloco multiparte conta uma vez. |

Não há grupos nem outras chaves editáveis do addon. O valor 1 limita o grupo à origem; 0 e negativos são inválidos. Estoque, conectividade, tipo, material e permissões podem reduzir o resultado. O preview é uma estimativa e desconhece claims do servidor.

O loader limita números abaixo de 1 a 1 e acima de 256 a 256; chaves ausentes ou valores de tipo incompatível usam o padrão 64. Use inteiros; entradas numéricas fracionárias podem ser convertidas para inteiro pelo loader. TOML malformado pode provocar recuperação do arquivo ou erro de carregamento pelo loader. Faça backup antes de editar.

## Aplicar alterações

O NeoForge monitora o arquivo ativo. Forge e Fabric conferem o arquivo ativo a cada 20 ticks do servidor e aplicam mudanças após duas leituras iguais. No Fabric, uma gravação incompleta mantém o limite anterior até que o arquivo volte a ser válido. Uma recarga válida atualiza a regra do servidor e envia o novo limite de preview aos clientes conectados. Se o monitor estiver desabilitado nas opções do NeoForge, reinicie o servidor ou reabra o mundo. Mover ou criar um override também exige carregar o mundo novamente.

**Bulk Action on Connected Copycats** é remapeada em **Controls**, com padrão **Left Alt**; não é chave TOML. Regras de claims pertencem ao mod de proteção do servidor.

[Materiais conectados](connected-materials) explica como o limite se aplica durante o jogo.
