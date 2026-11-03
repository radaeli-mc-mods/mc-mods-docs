# Compatibilidade com Tectonic 3

Este guia cobre o [fork do RoadWeaver](https://github.com/radaelilucca/RoadWeaver-Tectonic3), versão 2.4.1-1.21.1, no NeoForge 1.21.1 com Tectonic 3.0.28.

## Instalar e usar

Instale o JAR do RoadWeaver deste fork no cliente e no servidor. Use apenas um JAR do RoadWeaver por instalação. Tectonic continua opcional; quando instalado, também exige Lithostitched. Tectonic 3.0.28 inclui Apollib. Mantenha os mesmos mods e configurações de geração nos dois lados.

Crie ou abra o mundo. As estradas são planejadas entre as estruturas configuradas. Pressione **H** para abrir o mapa; o botão de configurações abre as opções. Espere o planejamento e a geração antes de se aproximar de novos trechos.

## Mundos existentes

Faça backup do mundo antes de atualizar mods. Chunks e estradas persistidas permanecem. Amostras de terreno, imagens do mapa e caches de caminhos pendentes são reconstruídos sob uma identidade que inclui a configuração efetiva do Tectonic. As estradas são aplicadas durante a geração de chunks novos; instalar o fork não pavimenta chunks explorados.

## Terreno e desempenho

O fork acompanha os limites verticais e níveis de fluidos configurados no Tectonic. As escalas de ruído normal e alternativa são suportadas. OpenCL é opcional: a aceleração precisa exige GPU FP64, e dispositivos incompatíveis ou divergências numéricas usam amostragem CPU. Alterar o raio inicial de planejamento muda a quantidade de terreno amostrada.

Administradores com nível de permissão 2 podem executar **/roadweaver diagnostics** para consultar limites do gerador, modelo de fluidos, identidade do terreno, backend e motivo de fallback.

Veja [Configurações](configuration.md) para os padrões e todas as opções.
