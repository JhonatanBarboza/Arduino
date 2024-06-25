# SSC0180-Eletrônica
## Projeto: Sonar
Este projeto consiste em um protótipo de sonar projetado para detectar e rastrear a aproximação de objetos. Os dados coletados pelo sonar serão processados e exibidos em tempo real na tela de um computador, permitindo uma visualização dos objetos.

## Componentes Eletrônicos
| Quantidade     | Componentes | Especificações | Valor |
| ---      | ---       | ---      | ---     |
| 1 | [Arduino](https://www.wjcomponentes.com.br/uno-ch340?parceiro=6298&gad_source=4&gclid=EAIaIQobChMIqNidsZvmhgMVYB6tBh0KiQYaEAQYCCABEgKJufD_BwE)     | 5V   | R$ 54,00  |
| 1 | [Protoboard](https://www.wjcomponentes.com.br/protoboard-830?parceiro=6298&gad_source=1&gclid=EAIaIQobChMIzp6Mz5zmhgMVSFxIAB1AOAIeEAQYBCABEgJrq_D_BwE)        | 830 furos    | R$ 10,00  |
| 4 | [Jumpers M/F](https://www.eletrogate.com/jumpers-macho-femea-20-unidades-de-20-cm)  | 10 uni    |  R$ 7,00   |
| 7 | [Jumpers M/M](https://www.eletrogate.com/jumpers-macho-macho-40-unidades-de-10-cm) | 10 uni | R$ 7,00 |
| 1 | [Ultrassom](https://www.eletrogate.com/modulo-sensor-de-distancia-ultrassonico-hc-sr04) |  HC-SR04 | R$ 16,00 |
| 1 | [Servo Motor 9g](https://www.eletrogate.com/micro-servo-9g-sg90-towerpro)     | 1kg/cm | R$ 30,40  |

Valor Total: R$ 124,40

## Fotos do Projeto

![WhatsApp Image 2024-06-25 at 11 28 03](https://github.com/JhonatanBarboza/Arduino/assets/151884657/7cb289fe-aab0-4572-8081-41f82ddb4d20)
![WhatsApp Image 2024-06-25 at 11 27 50](https://github.com/JhonatanBarboza/Arduino/assets/151884657/7412aac4-38b3-4f7a-b373-a06188cb41af)

## Descrição dos Componentes
### Arduino: 
Arduino é uma placa de prototipagem eletrônica que permite, de maneira fácil, a integração entre software e hardware. Além disso, devido a sua versatilidade, o Arduino é usado em vários tipos de projetos, desde brinquedos até automações para a melhora da vida cotidiana.

### Ultrassom:
O sensor de ultrassom HC-SR04 é utilizado para medir distâncias. Ele funciona emitindo pulsos ultrassônicos e calculando o tempo que leva para os ecos retornarem após refletirem em um objeto. No contexto de um projeto de radar, o HC-SR04 foi montado em um micro servo motor, permitindo que ele gire e faça varreduras do ambiente. Conectado ao Arduino, o sensor HC-SR04 fornece leituras de distância em tempo real, que são processadas e exibidas na tela do computador.

### Servo Motor:
Um micro servo motor de 9g é um componente ideal para projetos que requerem controle preciso de movimento. Este tipo de servo é compacto e eficiente, oferece torque suficiente para movimentar componentes leves. No contexto de um projeto do radar, o micro servo motor é utilizado para rotacionar sensor do sonar, permitindo a varredura do ambiente.

## Descrição do funcionamento
Este projeto consiste em um sistema de sonar baseado em Arduino, utilizando um micro servo motor de 9g e um sensor de ultrassom HC-SR04 para detectar e rastrear a aproximação de objetos. O funcionamento do projeto é descrito em etapas a seguir:

1. **Montagem do Hardware**:
   - O sensor de ultrassom HC-SR04 é montado sobre o micro servo motor de 9g.
   - O servo motor é controlado pelo Arduino, permitindo que o sensor gire em diferentes ângulos para realizar varreduras do ambiente.

2. **Configuração do Arduino**:
   - O Arduino é programado para controlar o servo motor, ajustando sua posição em intervalos regulares.
   - O Arduino também envia sinais de controle ao sensor de ultrassom para emitir pulsos ultrassônicos e medir o tempo de retorno do eco.

3. **Aquisição de Dados**:
   - O sensor HC-SR04 emite pulsos ultrassônicos e mede o tempo que os ecos levam para retornar após refletirem em um objeto.
   - O Arduino calcula a distância dos objetos com base no tempo de retorno dos ecos.

4. **Processamento de Dados**:
   - O Arduino processa os dados de distância e ângulo do servo motor para determinar a posição dos objetos no ambiente.
   - Os dados coletados são enviados para um computador.

5. **Visualização dos Resultados**:
   - Os resultados da varredura do sonar são exibidos em tempo real na tela do computador.


### Circuito tinkercad

![WhatsApp Image 2024-06-24 at 12 50 58](https://github.com/JhonatanBarboza/Arduino/assets/151884657/90c1848d-c845-414b-b9c0-ab1ac9897838)

### Vídeo do projeto funcionando

https://github.com/JhonatanBarboza/Arduino/assets/151884657/1bbd1c38-a06d-427c-8672-8a163b56fc5b

### Código arduino
          
          // Inclui a biblioteca Servo Motor
          #include <Servo.h>. 
          
          // Define os pinos Trig e Echo do sensor ultrassônico
          const int trigPin = 10;
          const int echoPin = 11;
          // Variáveis para a duração e a distância
          long duration;
          int distance;
          
          Servo myServo; // Cria um objeto servo para controlar o servo motor
          
          void setup() {
            pinMode(trigPin, OUTPUT); 
            pinMode(echoPin, INPUT);
            Serial.begin(9600);
            myServo.attach(12); // Define em qual pino o Servo Motor está conectado
          }
          void loop() {
            // gira o Servo Motor de 15 a 165 graus
            for(int i=15;i<=165;i++){  
            myServo.write(i);
            delay(30);
            distance = calculateDistance();// Chama uma função para calcular a distância medida pelo sensor ultrassônico para cada grau
            
            Serial.print(i); // Envia o grau atual para a porta serial
            Serial.print(","); // Envia o caractere de adição ao lado do valor anterior necessário posteriormente no IDE de processamento para indexação
            Serial.print(distance); // Envia o valor da distância para a porta serial
            Serial.print("."); // Envia o caractere de adição ao lado do valor anterior necessário posteriormente no IDE de processamento para indexação
            }
            // Repete as linhas anteriores de 165 a 15 graus
            for(int i=165;i>15;i--){  
            myServo.write(i);
            delay(30);
            distance = calculateDistance();
            Serial.print(i);
            Serial.print(",");
            Serial.print(distance);
            Serial.print(".");
            }
          }
          // Função para calcular a distância medida pelo sensor ultrassônico
          int calculateDistance(){ 
            
            digitalWrite(trigPin, LOW); 
            delayMicroseconds(2);
            // Define o trigPin no estado HIGH por 10 micro segundos
            digitalWrite(trigPin, HIGH); 
            delayMicroseconds(10);
            digitalWrite(trigPin, LOW);
            duration = pulseIn(echoPin, HIGH); // Lê o echoPin, retorna o tempo de viagem da onda sonora em microssegundos
            distance= duration*0.034/2;
            return distance;
          }

#### Código Processing

        /*   Arduino Radar Project
         *  
         *  by Dejan Nedelkovski, 
         *  www.HowToMechatronics.com
         *  Tradução: PontoMakers
         *
         */
        
        import processing.serial.*; // importa biblioteca para comunicação serial
        import java.awt.event.KeyEvent; // biblioteca de importações para ler os dados da porta serial
        import java.io.IOException;
        
        Serial myPort; 
        // variáveis
        String angle="";
        String distance="";
        String data="";
        String noObject;
        float pixsDistance;
        int iAngle, iDistance;
        int index1=0;
        int index2=0;
        PFont orcFont;
        
        void setup() {
          
         size (1366, 768); // ***MUDE ISTO PARA SUA RESOLUÇÃO DE TELA***
         smooth();
         myPort = new Serial(this,"COM4", 9600); // inicia a comunicação serial
         myPort.bufferUntil('.'); // lê os dados da porta serial até o caractere '.' Então, na verdade, lê isto: ângulo, distância.
         orcFont = loadFont("AgencyFB-Reg-30.vlw");
        }
        
        void draw() {
          
          fill(98,245,31);
          textFont(orcFont);
          // simulating motion blur and slow fade of the moving line
          noStroke();
          fill(0,4); 
          rect(0, 0, width, height-height*0.065); 
          
          fill(98,245,31); // cor verde
          // chama as funções para desenhar o radar
          drawRadar(); 
          drawLine();
          drawObject();
          drawText();
        }
        
        void serialEvent (Serial myPort) { // começa a ler dados da porta serial
          // lê os dados da porta serial até o caractere '.' e coloca na variável String "data".
          data = myPort.readStringUntil('.');
          data = data.substring(0,data.length()-1);
          
          index1 = data.indexOf(","); // encontre o caractere ',' e coloque-o na variável "index1"
          angle= data.substring(0, index1); // leia os dados da posição "0" para a posição da variável index1 ou seja o valor do ângulo que a placa Arduino enviou para a porta serial
          distance= data.substring(index1+1, data.length()); // ler os dados da posição "index1" para o final dos dados pr thats o valor da distância
          
          // converts the String variables into Integer
          iAngle = int(angle);
          iDistance = int(distance);
        }
        
        void drawRadar() {
          pushMatrix();
          translate(width/2,height-height*0.074); // move as coordenadas iniciais para o novo local
          noFill();
          strokeWeight(2);
          stroke(98,245,31);
          // desenha as linhas do arco
          arc(0,0,(width-width*0.0625),(width-width*0.0625),PI,TWO_PI);
          arc(0,0,(width-width*0.27),(width-width*0.27),PI,TWO_PI);
          arc(0,0,(width-width*0.479),(width-width*0.479),PI,TWO_PI);
          arc(0,0,(width-width*0.687),(width-width*0.687),PI,TWO_PI);
          // desenha as linhas angulares
          line(-width/2,0,width/2,0);
          line(0,0,(-width/2)*cos(radians(30)),(-width/2)*sin(radians(30)));
          line(0,0,(-width/2)*cos(radians(60)),(-width/2)*sin(radians(60)));
          line(0,0,(-width/2)*cos(radians(90)),(-width/2)*sin(radians(90)));
          line(0,0,(-width/2)*cos(radians(120)),(-width/2)*sin(radians(120)));
          line(0,0,(-width/2)*cos(radians(150)),(-width/2)*sin(radians(150)));
          line((-width/2)*cos(radians(30)),0,width/2,0);
          popMatrix();
        }
        
        void drawObject() {
          pushMatrix();
          translate(width/2,height-height*0.074); // move as coordenadas iniciais para o novo local
          strokeWeight(9);
          stroke(255,10,10); // cor vermelha
          pixsDistance = iDistance*((height-height*0.1666)*0.025); // cobre a distância do sensor de cm para pixels
          // limitando o alcance a 40 cms
          if(iDistance<40){
            // draws the object according to the angle and the distance
          line(pixsDistance*cos(radians(iAngle)),-pixsDistance*sin(radians(iAngle)),(width-width*0.505)*cos(radians(iAngle)),-(width-width*0.505)*sin(radians(iAngle)));
          }
          popMatrix();
        }
        
        void drawLine() {
          pushMatrix();
          strokeWeight(9);
          stroke(30,250,60);
          translate(width/2,height-height*0.074); // move as coordenadas iniciais para o novo local
          line(0,0,(height-height*0.12)*cos(radians(iAngle)),-(height-height*0.12)*sin(radians(iAngle))); // desenha a linha de acordo com o ângulo
          popMatrix();
        }
        
        void drawText() { // desenha os textos na tela
          
          pushMatrix();
          if(iDistance>40) {
          noObject = "Fora do Radar";
          }
          else {
          noObject = "Objeto Detectado";
          }
          fill(0,0,0);
          noStroke();
          rect(0, height-height*0.0648, width, height);
          fill(98,245,31);
          textSize(25);
          
          text("10cm",width-width*0.3854,height-height*0.0833);
          text("20cm",width-width*0.281,height-height*0.0833);
          text("30cm",width-width*0.177,height-height*0.0833);
          text("40cm",width-width*0.0729,height-height*0.0833);
          textSize(40);
          text("Objeto: " + noObject, width-width*0.875, height-height*0.0277);
          text("Anglo: " + iAngle +" °", width-width*0.48, height-height*0.0277);
          text("Distancia: ", width-width*0.26, height-height*0.0277);
          if(iDistance<40) {
          text("        " + iDistance +" cm", width-width*0.225, height-height*0.0277);
          }
          textSize(25);
          fill(98,245,60);
          translate((width-width*0.4994)+width/2*cos(radians(30)),(height-height*0.0907)-width/2*sin(radians(30)));
          rotate(-radians(-60));
          text("30°",0,0);
          resetMatrix();
          translate((width-width*0.503)+width/2*cos(radians(60)),(height-height*0.0888)-width/2*sin(radians(60)));
          rotate(-radians(-30));
          text("60°",0,0);
          resetMatrix();
          translate((width-width*0.507)+width/2*cos(radians(90)),(height-height*0.0833)-width/2*sin(radians(90)));
          rotate(radians(0));
          text("90°",0,0);
          resetMatrix();
          translate(width-width*0.513+width/2*cos(radians(120)),(height-height*0.07129)-width/2*sin(radians(120)));
          rotate(radians(-30));
          text("120°",0,0);
          resetMatrix();
          translate((width-width*0.5104)+width/2*cos(radians(150)),(height-height*0.0574)-width/2*sin(radians(150)));
          rotate(radians(-60));
          text("150°",0,0);
          popMatrix(); 
        }

### Responsáveis
- Jhonatan Barboza da Silva
- João Gabriel Pieroli da Silva
- Pedro Henrique de Sousa Prestes
- Kevin Ryoji Nakashima
