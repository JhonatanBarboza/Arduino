# SSC0180-Eletrônica
## Projeto: RFID
Este projeto é um exemplo de aplicação da placa RFID usando como base o Arduino. A ideia geral do projeto é simular uma fechadura eletrônica que é aberta apenas com cartões autorizados. 

## Componentes Eletrônicos
| Quantidade     | Componentes | Especificações | Valor |
| ---      | ---       | ---      | ---     |
| 1 | [Arduino](https://www.wjcomponentes.com.br/uno-ch340?parceiro=6298&gad_source=4&gclid=EAIaIQobChMIqNidsZvmhgMVYB6tBh0KiQYaEAQYCCABEgKJufD_BwE)     | 5V   | R$ 54,00  |
| 1 | [Kit RFID](https://www.wjcomponentes.com.br/sensor-rfid?parceiro=6298&gad_source=4&gclid=EAIaIQobChMIq6bMpJnmhgMV1SCtBh31tAkMEAQYAyABEgK4evD_BwE)  | 13,56Mhz    |  R$ 20,00   |
| 2 | [LED Cristal](https://www.wjcomponentes.com.br/resistores-leds/leds/led-5-mm-difuso?variant_id=257&parceiro=6298&gad_source=4&gclid=EAIaIQobChMIhY7UsZrmhgMVGzStBh1BAQ8tEAQYBiABEgKwevD_BwE) | 2V/20mA | R$ 2,00 |
| 2 | [LED Vermelho](https://www.wjcomponentes.com.br/resistores-leds/leds/led-5-mm-difuso?variant_id=257&parceiro=6298&gad_source=4&gclid=EAIaIQobChMIhY7UsZrmhgMVGzStBh1BAQ8tEAQYBiABEgKwevD_BwE) | 2V/20mA | R$ 2,00 |
| 4     | [Resistor 2k2](https://www.edfcomponentes.com.br/resistor/resistor-2k2-14w-5-2200-ohms-cr25)     | 2200 Ω 1/4W    | R$ 0,07  |
| 1     | [Protoboard](https://www.wjcomponentes.com.br/protoboard-830?parceiro=6298&gad_source=1&gclid=EAIaIQobChMIzp6Mz5zmhgMVSFxIAB1AOAIeEAQYBCABEgJrq_D_BwE)        | 830 furos    | R$ 10,00  |

Valor Total: R$ 92,28

### Vídeos do projeto funcionando

[video]


## Descrição dos Componentes
### Arduino: 
Arduino é uma placa de prototipagem eletrônica que permite, de maneira fácil, a integração entre software e hardware. Além disso, devido a sua versatilidade, o Arduino é usado em vários tipos de projetos, desde brinquedos até automações para a melhora da vida cotidiana.

### Placa RFID:
RFID, sigla para “Radio Frequency Identification”, significa “identificação por radiofrequência”. Com essa placa, é possível detectar chips que funcionam por radiofrequência, sendo muito utilizada em identificações rápidas por meio de cartões.

### Resistores:
Um resistor é um componente elétrico que limita o fluxo de corrente em um circuito. Ele dissipa energia na forma de calor e é utilizado para controlar níveis de tensão e corrente. No nosso projeto foram utilizados quatro resistores de 2.2k.

### Botão:
Botão é um componente elétrico que, ao ser pressionado, permite que haja a passagem de corrente naquele ponto.

### Led:
Led é um componente que, ao receber corrente, começa a brilhar. Em nosso projeto, o Led será a representação da fechadura, que será aberta com determinados cartões cadastrados.



### Cadastro Cartão Mestre:


### Cadastro Cartão de Acesso: 


### Acesso:


### Reset do Cartão Mestre: 



## Cálculos

### Razão do Transformador

Para trabalhar com uma saída de tensão de \( V_s = 24,4V \) (medido na prática) e um transformador com uma razão de 6,96, usamos a equação do transformador para calcular a tensão de entrada necessária.

#### Tensão de Pico

Primeiramente, calculamos a tensão de pico V(pico) da entrada senoidal:

$$ V_{\text{pico}} = V_{\text{entrada}} \times \sqrt{2} $$

Onde:
- V(entrada) é a tensão de entrada da tomada (127V).

Substituindo os valores:

$$ V_{\text{pico}} = 127V \times \sqrt{2} = 179,6V $$

#### Razão do Transformador

Desejando um transformador que produza uma tensão de saída (Vs) de 24,4V com uma razão de 6,96, utilizamos a relação do transformador:

$$ \frac{1}{6,96} = \frac{V_s}{V_{\text{pico}}} $$

Resolvendo para V(s):

$$ V_s = \frac{V_{\text{pico}}}{6,96} $$

Substituindo os valores:

$$ V_s = \frac{179,6V}{6,96} \approx 25,8V $$

Considerando que o diodo precisa de uma tensão mínima de 0,7V cada, devemos subtrair 1,4V da tensão de saída:

$$ V_s = 25,8V - 1,4V = 24,4V $$

Portanto, a tensão de saída ajustada é de 24,4V.
##
### Cálculo da Tensão de Ripple (Vripple)

Para calcular a tensão de ripple, consideramos uma tensão de ripple de 10% da tensão de saída.

$$ V_{\text{ripple}} = 0,1 \times V_s $$

Substituindo o valor da tensão de saída:

$$ V_{\text{ripple}} = 0,1 \times 24,4V = 2,44V $$

Portanto, a tensão de ripple é 2,44V.
##
### Cálculo da Tensão Média

A tensão média V(média) é a média aritmética entre a tensão mínima e a tensão máxima, portanto:

1. **Identificação dos limites de variação**:
- Tensão mínima: 23,6V
- Tensão máxima: 24,6V

2. **Cálculo da Tensão Média**:
- A tensão média é calculada pela média aritmética entre V(min) e V (max):

$$ V_{\text{média}} = \frac{V_{\text{min}} + V_{\text{max}}}{2} $$

   Substituindo os valores conhecidos:

$$ V_{\text{média}} = \frac{23,6V + 24,6V}{2} $$

$$ V_{\text{média}} = \frac{48,2V}{2} $$

$$ V_{\text{média}} = 24,1V $$

Portanto, a tensão média entre 23,6V e 24,6V é de aproximadamente 24,1V.
##
### Correntes:
##
### Capacitância:


### Circuito FALSTAD

O circuito a seguir ilustra um esquema simplificado da Fonte de Tensão Ajustável projetada no falstad.

![Circuito fonte de tensao](https://github.com/JhonatanBarboza/Fonte_de_tensao/assets/170869780/a9bb88d5-aff1-49af-bc49-cd9261177960)

[Link do Circuito](https://tinyurl.com/24obwzt2)

### Circuito PCB no EAGLE

#### Esquemático no EAGLE

<img width="750" alt="EAGLE" src="https://github.com/JhonatanBarboza/Fonte_de_tensao/assets/170869780/ac880d5f-2a76-4c06-a4d0-f1967f057047">

#### Board no EAGLE

<img width="750" alt="Captura de tela 2024-06-12 211634" src="https://github.com/JhonatanBarboza/Fonte_de_tensao/assets/170869780/608f7f37-48ac-4ff8-a1dd-6e02533ff465">

## Fotos do Projeto

![min](https://github.com/JhonatanBarboza/Fonte_de_tensao/assets/170869780/e0ab747d-6cb8-43f0-be28-b8d9621ee088)
![max](https://github.com/JhonatanBarboza/Fonte_de_tensao/assets/170869780/7d4522fb-9ad1-4026-95a0-f721d461094a)


### Resposáveis
- Jhonatan Barboza da Silva
- João Gabriel Pieroli da Silva
- Pedro Henrique de Sousa Prestes
- Kevin Ryoji Nakashima

fonte: 

[Imagem 1](https://professor.pucgoias.edu.br/SiteDocente/admin/arquivosUpload/17742/material/Cap%204_ret%20onda%20completa_2017.pdf)

[Imagem 2](https://embarcados.com.br/aprenda-a-analisar-o-ripple-da-sua-fonte/)

