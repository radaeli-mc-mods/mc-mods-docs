---
title: Instrumentos de atitude
---

# Instrumentos de atitude

A Attitude Reference Unit experimental mede pitch, roll, rumo, razão de curva, velocidade vertical e derrapagem da aeronave. Ela publica as leituras pela rede de cabos aviônicos. O Attitude Indicator experimental exibe pitch e roll numa Modular Table. Na versão 0.4.0-beta.2, os dois blocos são exclusivos do criativo.

## Attitude Reference Unit

Coloque a unidade na aeronave e conecte um Wire Connector nela à rede aviônica. A marca de cobre identifica o eixo Nose; a marca de latão identifica Up. As direções devem ser perpendiculares. Use a Wrench do Create numa face para definir Nose e depois use-a na unidade novamente para definir Up. O bloco não precisa girar. Uma unidade recém-colocada usa como Nose a direção para a qual você olhava e como Up o topo do bloco.

Se a aeronave fica parada com pequena inclinação, abra a unidade com a mão vazia e escolha Calibrate level para tratar o pitch e o roll atuais como zero. A calibração fica disponível quando ambos os ângulos estão a até 15° do nível. Reset calibration apaga os ajustes. Damping alterna entre Off, Light e Strong para suavizar os valores publicados de atitude.

Numa aeronave em movimento, a unidade informa pitch (nariz para cima é positivo), roll (asa direita para baixo é positivo), rumo, razão de curva (virar à direita é positivo), velocidade vertical e derrapagem. Com o nariz quase na vertical, roll e rumo mantêm os últimos valores definidos e a leitura fica degradada. Fora de uma aeronave em movimento, ela informa voo nivelado.

## Attitude Indicator

Instale o módulo numa Modular Table clicando com o botão direito enquanto o segura. Ele ocupa 2 × 2 células e pode atravessar mesas unidas. Uma mesa no chão usa carcaça inclinada; mesas na parede ou no teto usam placa reta.

Conecte a mesa à mesma rede de cabos que uma Attitude Reference Unit. O indicador usa a unidade utilizável mais próxima na mesma aeronave. Clique com a mão vazia no módulo instalado para abrir a tela e conferir pitch, roll e o estado das fontes. O mostrador tem uma escala de pitch simplificada, com marcas a cada 10°, e indicações de inclinação a 30° e 60°. As cores mudam entre dia e noite, e a altitude aparece em uma faixa grande na parte inferior. Também há uma faixa de velocidade com um valor simulado temporário em blocos por segundo; ela não mede a velocidade da aeronave.

- Uma unidade utilizável mostra o horizonte artificial. Nariz para cima desloca o horizonte para baixo; asa direita para baixo é roll positivo.
- Com o nariz quase na vertical, aparece uma bandeira ATT âmbar e o último roll definido é mantido.
- Sem unidade utilizável ou com rede incompleta, a tela fica preta e mostra uma bandeira ATT vermelha.
- Um Radar Altimeter na rede acrescenta fita de altitude com a distância até o solo em blocos. A fonte é a menor leitura válida; fora do alcance do radar, aparece ----.
- Use o controle Altitude tape para exibir ou ocultar a fita. O horizonte se expande quando ela fica oculta.

O indicador não precisa de Avionics Computer. A Modular Table funciona como ponto de conexão da rede aviônica.
