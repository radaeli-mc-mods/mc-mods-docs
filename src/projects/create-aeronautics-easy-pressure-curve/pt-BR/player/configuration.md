---
title: Configurações
description: "Como controlar o Create: Aeronautics Easy Pressure Curve."
---

# Configurações

A versão 0.1.0 não adiciona arquivos de configuração editáveis para jogadores nem administradores de servidor. A curva é controlada no jogo pelo [editor da curva](./#editar-a-curva-em-um-grafico) e pelo [comando `/pressurecurve`](./#comandos), e ambos exigem permissão de operador (nível 2) para alterar algo.

## Tecla

| Controle | Padrão | Onde mudar |
| --- | --- | --- |
| Abrir editor da curva de pressão | `F9` | Opções → Controles → Teclas → Aeronautics Easy Pressure Curve (cliente). |

A tecla só funciona no jogo, sem nenhuma tela aberta e só para operadores (nível 2).

As curvas definidas ficam salvas no mundo, em `data/create_aeronautics_easy_pressure_curve.dat`. Isso é estado do jogo, não um arquivo de configuração: altere as curvas pelo comando, sem editá-lo.

O datapack que fornece a curva inicial é o `data/sable/dimension_physics/*.json` do Sable. O `pressure_function` de cada arquivo tem o formato que `/pressurecurve set` aceita. Veja [Instalação e uso](./) para o guia completo.
