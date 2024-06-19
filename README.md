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
O cartão mestre será o primeiro cartão a ser cadastrado no Arduino. Por isso, ele terá mais permissões, podendo cadastrar outros cartões no sistema da fechadura. O cadastro é feito com a aproximação do cartão perto do sensor até que o último LED da direita pare de piscar. Quando isso ocorrer, o cartão já foi cadastrado.

### Cadastro Cartão de Acesso: 
Depois de cadastrar o cartão mestre, é possível cadastrar outros cartões também. Para isso, é necessário aproximar o cartão mestre do sensor, em seguida aproximar o cartão a ser cadastrado e, por fim, aproximar novamente o cartão mestre. Dessa maneira, o novo cartão registrado também terá permissão para abrir a fechadura.

### Acesso:
Para a abertura da fechadura basta aproximar o cartão à placa RFID e esperar a liberação. O acesso ocorre apenas com cartões cadastrados. Portanto, para permitir que outras pessoas entrem em um local com essa fechadura, é necessário registrar um novo cartão de acesso.

### Reset do Cartão Mestre: 
Às vezes, por algum motivo qualquer, pode ocorrer a perda do cartão mestre. Por isso, a fechadura possui um procedimento para substituí-lo. Para isso, é necessário pressionar o botão por 10 segundos até que o segundo LED da esquerda para a direita pare de voltar a brilhar. Após isso, basta realizar o cadastro do novo cartão mestre.


### Código: https://www.arduinoecia.com.br/controle-de-acesso-modulo-rfid-rc522/


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

