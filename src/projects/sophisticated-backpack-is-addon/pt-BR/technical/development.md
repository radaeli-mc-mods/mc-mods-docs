---
title: Build e verificação do artefato
description: Compile os três targets e execute testes de lógica, redes nativas e verificação dos artefatos.
---

# Build e verificação do artefato

O código usa builds independentes para Forge 1.20.1 (Java 17), NeoForge 1.21.1 (Java 21) e NeoForge 26.1.2 (Java 25). Instale os três JDKs e Node.js para o verificador de artefatos. O wrapper Gradle da raiz coordena os targets:

```powershell
.\gradlew.bat checkAll
.\gradlew.bat buildAll
```

`checkAll` executa os testes Java comuns e as verificações de cada target. `buildAll` também compila e inspeciona os três JARs de distribuição. Não exige `clean`. Identidade e versão vêm do `gradle.properties` da raiz; `-Pmod_version=<versão>` é propagado a todos os targets.

Os JARs de distribuição ficam em `targets/<minecraft>/<loader>/build/libs/`. As fontes Java comuns e as texturas compatíveis são incluídas em cada artefato. Os mods de armazenamento e as fixtures de integração não são incorporados.

## Dependências e perfis NeoForge 26.1.2

O build usa NeoForge 26.1.2.124, Java 25, ModDevGradle 2.0.148 e Gradle 9.4.0. `targets/26.1.2/dependencies.lock.json` registra versões auditadas, origens imutáveis de download e hashes SHA-256. Artefatos públicos ausentes são baixados e verificados antes da compilação. SCC 1.6.5 é versionado em `libs/26.1.2/`, acompanhado da licença. Nenhuma dependência usa um caminho em Downloads.

A partir de `targets/26.1.2`, execute um perfil isolado:

```powershell
.\gradlew.bat :neoforge:check -PbackendProfile=all
.\gradlew.bat :neoforge:runClient -PbackendProfile=all
.\gradlew.bat :neoforge:runServer -PbackendProfile=all
.\gradlew.bat :neoforge:runRestartVerify -PbackendProfile=all
```

Os perfis são `none`, `ae2`, `rs`, `toms`, `scc` e `all`. Core e Backpacks sempre são carregados; GuideME acompanha AE2. As verificações conferem os backends realmente carregados, executam JUnit com o servidor efêmero oficial e GameTests com blocos, redes e upgrades nativos, acionados pelos fluxos de menu ou tick. Perfis obrigatórios vazios ou incompletos e skips JUnit inesperados fazem o build falhar.

Relatórios XML e HTML JUnit ficam em `neoforge/build/test-results/<perfil>` e `neoforge/build/reports/tests/<perfil>`. Sumários e logs de integração nativa ficam em `neoforge/build/reports/integration/<perfil>`. O CI executa os seis perfis separadamente e publica os relatórios mesmo em falha.

O perfil `all` também inicia dois JVMs separados sobre o mesmo mundo de teste. O primeiro salva mochilas com reservas conhecidas e entregas incertas; o segundo verifica o conteúdo dos backends, recupera os recursos conhecidos uma vez e mantém entregas incertas em quarentena. `runRestartVerify` executa as duas fases. Relatórios XML nativos e logs ficam em `neoforge/build/reports/restart/<fase>`. Os hooks de preservação do mundo são exclusivos dos testes e não entram no JAR de produção.

## Verificações dos artefatos

Na raiz do repositório:

```powershell
.\gradlew.bat verify-forge-1.20.1
.\gradlew.bat verify-neoforge-1.21.1
.\gradlew.bat verify-neoforge-26.1.2
```

O verificador confere metadados, identidade de Minecraft e loader, versão, bytecode, nove upgrades, receitas, tags, traduções, modelos, referências locais a texturas, Mixins e ausência de código de dependências e fixtures.

No Forge, também inspeciona o JAR de produção reobfuscado, seu refmap Mixin, o mapeamento do accessor e o runtime MixinExtras incorporado. Sete fixtures de artefatos danificados exercitam o mesmo verificador. Para inspecionar outro JAR Forge, execute a partir de `targets/1.20.1`:

```powershell
.\gradlew.bat :forge:verifyForgeProductionJar -PforgeProductionJar=C:/path/to/addon.jar
.\gradlew.bat :forge:testForgeProductionJarVerification
```

Caminhos relativos no override são resolvidos a partir de `targets/1.20.1`. O artefato com nomes legíveis em `forge/build/devlibs` não é o JAR de distribuição.

Verificações de artefatos e automação de servidor não comprovam aparência da GUI nem comportamento multiplayer. Valide telas, controles sincronizados, ícones e animações de vínculo e dois jogadores com permissões diferentes em uma sessão separada de cliente e servidor dedicado. Migração de mundos entre versões de Minecraft não faz parte desse contrato de build.
