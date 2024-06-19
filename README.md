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

## Descrição do funcionamento

### Cadastro Cartão Mestre:
O cartão mestre será o primeiro cartão a ser cadastrado no Arduino. Por isso, ele terá mais permissões, podendo cadastrar outros cartões no sistema da fechadura. O cadastro é feito com a aproximação do cartão perto do sensor até que o último LED da direita pare de piscar. Quando isso ocorrer, o cartão já foi cadastrado.

### Cadastro Cartão de Acesso: 
Depois de cadastrar o cartão mestre, é possível cadastrar outros cartões também. Para isso, é necessário aproximar o cartão mestre do sensor, em seguida aproximar o cartão a ser cadastrado e, por fim, aproximar novamente o cartão mestre. Dessa maneira, o novo cartão registrado também terá permissão para abrir a fechadura.

### Acesso:
Para a abertura da fechadura basta aproximar o cartão à placa RFID e esperar a liberação. O acesso ocorre apenas com cartões cadastrados. Portanto, para permitir que outras pessoas entrem em um local com essa fechadura, é necessário registrar um novo cartão de acesso.

### Reset do Cartão Mestre: 
Às vezes, por algum motivo qualquer, pode ocorrer a perda do cartão mestre. Por isso, a fechadura possui um procedimento para substituí-lo. Para isso, é necessário pressionar o botão por 10 segundos até que o segundo LED da esquerda para a direita pare de voltar a brilhar. Após isso, basta realizar o cadastro do novo cartão mestre.

### Circuito tinkercad

![Design sem nome (2)](https://github.com/JhonatanBarboza/Arduino/assets/170869780/8a1e4160-2e35-4807-8d3e-955325a2affa)

## Fotos do Projeto

![foto 2](https://github.com/JhonatanBarboza/Arduino/assets/170869780/fa4411ff-dc62-465f-b4b5-a9c23a04056c)

### Vídeo do projeto funcionando

[video](https://www.youtube.com/shorts/f6pqwsJiKrs)

#### Cógido para seguir linha (arquivo segue_linha)

      #include <SPI.h>
      #include <MFRC522.h>
      #include <stdbool.h>
      
      //Definindo nomeando os pinos
      #define   SS_PIN 10
      #define   RST_PIN 9
      #define   led1 7
      #define   led2 6
      #define   led3 5
      #define   ledf 4
      #define   button 3
      
      //Criando uma instância do mfrc
      MFRC522 mfrc522(SS_PIN, RST_PIN);
      
      //Protótipo da função de funcionamento do RFID
      void rfid_func(); 
      
      //Variável responsável por indicar a presença do cartão mestre
      bool mestre = 0;
      
      //Vetor de string que irá armazenar os códigos
      String keys[100];
      
      //Índices do vetor de strings
      int cont = 0;
      
      //Setando os valores iniciais
      void setup() 
      {
      
        //Setando os output e inputs que serão usados
        pinMode(led1, OUTPUT);
        pinMode(led2, OUTPUT);
        pinMode(led3, OUTPUT);
        pinMode(ledf, OUTPUT);
        pinMode(button, INPUT);
        
        Serial.begin(9600);   // Inicia comunicação Serial em 9600 baud rate
        SPI.begin();          // Inicia comunicação SPI bus
        mfrc522.PCD_Init();   // Inicia MFRC522
        
        Serial.println("Aproxime o seu cartao do leitor...");
        Serial.println();
      
        //O led azul(led3) começa ligado
        digitalWrite(led1, LOW);
        digitalWrite(led2, LOW);
        digitalWrite(led3, HIGH);
        digitalWrite(ledf, LOW);
        
         
        
      } //end setup
      
      
      // --- Loop Infinito ---
      void loop() 
      {
          rfid_func();   //chama função para identificação de tags RFID
      } //end loop
      
      
      void rfid_func()                            //Função para identificação das tags RFID
      {
            // -- Verifica novas tags --
            if ( ! mfrc522.PICC_IsNewCardPresent()) 
            {
              return;
            }
            // Seleciona um dos cartões
            if ( ! mfrc522.PICC_ReadCardSerial()) 
            {
              return;
            }
      
      //Se nenhum cartão mestre estiver cadastrado
      if(mestre == 0)
      {
          //Leitura do número do cartão
          Serial.print("UID da tag :");
          String conteudo= "";
          String conteudo1= "";
          byte letra;
          for (byte i = 0; i < mfrc522.uid.size; i++) 
          {
             Serial.print(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " ");
             Serial.print(mfrc522.uid.uidByte[i], HEX);
             conteudo.concat(String(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " "));
             conteudo.concat(String(mfrc522.uid.uidByte[i], HEX));
             conteudo1.concat(String(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " "));
             conteudo1.concat(String(mfrc522.uid.uidByte[i], HEX));
          }
          keys[cont] = conteudo1;
          //Incremento índice
          cont++;
          //Trocando o valor de "mestre", uma vez que ele já foi cadastrado
          mestre = 1;
          //Piscando o led azul uma vez
          digitalWrite(led3, LOW);
          delay(800);
          digitalWrite(led3, HIGH);
          Serial.println();
          Serial.print("Mensagem : ");
          conteudo.toUpperCase(); 
          return;
      }
      
      //Leitura do cartão, já com o cartão mestre cadastrado
      Serial.print("UID da tag :");
      String conteudo= "";
      byte letra;
      for (byte i = 0; i < mfrc522.uid.size; i++) 
      {
         Serial.print(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " ");
         Serial.print(mfrc522.uid.uidByte[i], HEX);
         conteudo.concat(String(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " "));
         conteudo.concat(String(mfrc522.uid.uidByte[i], HEX));
         keys[cont].concat(String(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " "));
         keys[cont].concat(String(mfrc522.uid.uidByte[i], HEX));
      }
      cont++;
      Serial.println();
      Serial.print("Mensagem : ");
      conteudo.toUpperCase(); 
      
      //Se o cartão aproximado for o mestre
      if (conteudo.substring(1) == keys[0])
      {
        int finish = 0;
        
        
        //Piscar todos os leds 3 vezes para sinalizar que o mestre foi lido
        digitalWrite(led1, HIGH);
        digitalWrite(led2, HIGH);
        digitalWrite(led3, HIGH);
        delay(800);
        digitalWrite(led1, LOW);
        digitalWrite(led2, LOW);
        digitalWrite(led3, LOW);
        delay(800);
        digitalWrite(led1, HIGH);
        digitalWrite(led2, HIGH);
        digitalWrite(led3, HIGH);
        delay(800);
        digitalWrite(led1, LOW);
        digitalWrite(led2, LOW);
        digitalWrite(led3, LOW);
        
        Serial.println("Aproxime o cartão a ser cadastrado");
        Serial.println();
        
        //Loop até ser aproximado outro cartão(cartão a ser cadastrado)
        while(finish == 0)
        {
            if(mfrc522.PICC_IsNewCardPresent())
            {
                if(mfrc522.PICC_ReadCardSerial())
                {
                    Serial.print("UID da tag :");
                      String conteudo= "";
                      byte letra;
                      for (byte i = 0; i < mfrc522.uid.size; i++) 
                      {
                         Serial.print(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " ");
                         Serial.print(mfrc522.uid.uidByte[i], HEX);
                         conteudo.concat(String(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " "));
                         conteudo.concat(String(mfrc522.uid.uidByte[i], HEX));
                         keys[cont].concat(String(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " "));
                         keys[cont].concat(String(mfrc522.uid.uidByte[i], HEX));
                      }
                      cont++;
                      //Led verde piscar 2 vezes para sinalizar que o cartão foi cadastrado
                      digitalWrite(led1, HIGH);
                      delay(800);
                      digitalWrite(led1, LOW);
                      delay(800);
                      digitalWrite(led1, HIGH);
                      delay(800);
                      digitalWrite(led1, LOW);
                      digitalWrite(led3, HIGH);
                      Serial.println();
                      Serial.print("Mensagem : ");
                      conteudo.toUpperCase(); 
                      finish = 1;
                      
                }
            }
        }
         
      }
     
      //Se o cartão não for o mestre
      if (conteudo.substring(1) != keys[0]) //outras tags
      {
        int finish = 0;
        //Loop para percorrer o vetor de strings
        for(int i=0;i<cont-1 && finish == 0;i++)
        {
            //Se for encontrado uma string igual ao do cartão, finish = 1 e sairá do loop
            if(conteudo.substring(1) == keys[i])
            {
                finish = 1;
            }
        }
        
        //Se finish == 1, então foi encontrado
        if(finish == 1)
        {
            //Piscar 3 vezes o led verde
            digitalWrite(led1, HIGH);
            delay(800);
            digitalWrite(led1, LOW);
            delay(800);
            digitalWrite(led1, HIGH);
            delay(800);
            digitalWrite(led1, LOW);
            delay(800);
            digitalWrite(led1, HIGH);
            delay(800);
            digitalWrite(led1, LOW);
        }
        //Se finish == 0, então não foi encontrado
        else
        {
            //Piscar 3 vezes o led vermelho
            digitalWrite(led2, HIGH);
            delay(800);
            digitalWrite(led2, LOW);
            delay(800);
            digitalWrite(led2, HIGH);
            delay(800);
            digitalWrite(led2, LOW);
            delay(800);
            digitalWrite(led2, HIGH);
            delay(800);
            digitalWrite(led2, LOW);
        }
        digitalWrite(led3, HIGH);
      }
  
  
} //end rfid_func
      
[Código](https://www.arduinoecia.com.br/controle-de-acesso-modulo-rfid-rc522/)

### Resposáveis
- Jhonatan Barboza da Silva
- João Gabriel Pieroli da Silva
- Pedro Henrique de Sousa Prestes
- Kevin Ryoji Nakashima
