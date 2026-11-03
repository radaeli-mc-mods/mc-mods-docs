---
title: Build e verificação do artefato
description: Compile e inspecione o artefato Forge de produção de Digital Storage Expansion.
---

# Build e verificação do artefato

Esta referência cobre o módulo Forge 1.20.1 no código-fonte da versão 0.4.1. Execute o wrapper Gradle na raiz do repositório com Java 21 para o Gradle e uma toolchain Java 17 para compilação e runtime Forge.

```powershell
.\gradlew.bat :forge:build
.\gradlew.bat :forge:verifyForgeProductionJar
.\gradlew.bat :forge:testForgeProductionJarVerification
```

O build inclui as duas verificações de artefato por `:forge:check`, além dos testes existentes e GameTests Forge. O verificador de produção executa após `reobfJar` e abre seu JAR em `forge/build/libs`. O artefato de desenvolvimento com nomes legíveis em `forge/build/devlibs` não é o arquivo de distribuição.

## O que a verificação do artefato comprova

O verificador confere a declaração `MixinConfigs` do manifesto, a referência explícita ao refmap na configuração Mixin, o refmap e a classe do accessor empacotados e o mapeamento de `pickupDelay` para `f_31986_:I` nos contextos padrão e `searge`. Também confere a declaração Jar-in-Jar e o runtime MixinExtras incorporado, necessário ao contexto de pickup. A versão incorporada é 0.4.1, com o intervalo Jar-in-Jar `[0.4.1,)` para seleção compartilhada.

A tarefa de regressão rejeita cópias temporárias sem referência ao refmap, sem refmap, sem mapeamento do accessor, com mapeamento `searge` incorreto, sem manifesto, sem metadados Jar-in-Jar ou sem declaração MixinExtras. Ela usa o mesmo verificador da tarefa de produção.

Para inspecionar um JAR compilado anteriormente:

```powershell
.\gradlew.bat :forge:verifyForgeProductionJar -PforgeProductionJar=C:/path/to/addon.jar
```

Um caminho relativo é resolvido a partir da raiz do repositório. A opção muda somente o arquivo inspecionado; a tarefa continua dependendo de `reobfJar`. Artefatos inválidos fazem a tarefa falhar com um erro que descreve o contrato ausente.

## Verificações de runtime

Verificações de artefato comprovam o empacotamento, não a compatibilidade em jogo. Carregue o JAR final em uma instalação isolada de Minecraft 1.20.1 com Java 17, Forge e Sophisticated Core/Backpacks. Teste a base suportada e as versões exatas usadas em um problema relatado. Valide o menu principal, um mundo novo e o carregamento de servidor dedicado separadamente das inicializações de desenvolvimento.

Para Magnet, confira delay infinito de coleta (`32767`), delay finito, transferências parciais e coexistência com Pickup. Preserve as regras existentes de elegibilidade e inspecione o primeiro erro causal se surgir uma falha posterior de inicialização.
