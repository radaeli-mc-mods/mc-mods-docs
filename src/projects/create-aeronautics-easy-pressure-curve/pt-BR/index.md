---
title: "Create: Aeronautics Easy Pressure Curve"
description: "Altere a curva de pressão do ar do Sable ao vivo, por dimensão, sem reiniciar."
---

# Create: Aeronautics Easy Pressure Curve

[![CurseForge](https://cf.way2muchnoise.eu/title/1792363.svg)](https://www.curseforge.com/minecraft/mc-mods/create-aeronautics-easy-pressure-curve)

Balões, hélices e burners do Create Aeronautics dependem de quanto o ar fica rarefeito com a altitude. O Sable define essa **curva de pressão do ar** em um datapack. O Create: Aeronautics Easy Pressure Curve permite alterá-la **com o mundo em execução**: a nova curva vale na hora no servidor e para todos os jogadores conectados, sem reiniciar, sem recarregar o mundo e sem um `/reload` completo. O mod não adiciona blocos, itens nem receitas.

**Documentação referente à versão 0.1.0 de Create: Aeronautics Easy Pressure Curve.**

| Minecraft | Loader | Requer | Opcional |
| --- | --- | --- | --- |
| 1.21.1 | NeoForge 21.1.236 | Sable 2.0.5 ou mais recente; R-Ui Lib 0.10.0 ou mais recente no cliente | Create Aeronautics 1.3 ou mais recente |

Instale o mod no servidor (obrigatório). No cliente ele é opcional: jogadores sem o mod entram normalmente e a curva também vale para eles; quem o instalar (com o R-Ui Lib) ganha também a tela do editor.

## Para jogadores

- [Instalação e uso](player/): edite a curva em um gráfico ou com `/pressurecurve`, consulte-a, edite pontos avulsos e volte ao padrão.
- [Configurações](player/configuration): a tecla do editor e o fato de o mod não ter arquivos de configuração.

## Para desenvolvedores

- [API para desenvolvedores](technical/api): `PressureCurveService`, `PressureCurve` e o payload do cliente para o servidor.

## Changelog

[Consultar notas de versão](changelog)
