# Passo a Passo como inserir no local

- Cole o arquivo script_medida.sql no Mysql Workbench e crie o banco de dados e as tabelas;
- Se precisar mude o arquivo de conexão com o banco de dados dentro de /app/connection.js;
- Veja se as portas estão configuradas de maneira correta;
- Insira o Arduino no Computador e teste dentro do Software arduino se os dados estão chegando OK no Monitor Serial;
- Após isso, no terminal do VS Code, instale os pacotes do node, com 'npm i';
- Quando os pacotes forem instalados, dê 'npm start' e os dados começaram a vir no terminal e uma aba no navegador irá abrir e assim, os dados serão gravados no Banco de Dados Local Mysql - Sensor.
 
---------
## Código Arduino

```c++
#include <DHT.h>
#include <DHT_U.h>

#include <Adafruit_Sensor.h>

#include <DHT.h>
#include <DHT_U.h>

#include "DHT.h"

#define DHTPIN A1
#define LM35PIN A5
#define LUMIPIN A0
#define CHAVPIN 7


DHT dht(DHTPIN, DHT11);

void setup()
{
  pinMode(DHTPIN, INPUT);
  pinMode(CHAVPIN, INPUT);
  Serial.begin(9600);
  dht.begin();
}

void loop()
{
  float dht11_umidade = dht.readHumidity();
  float dht11_temperatura = dht.readTemperature();
  Serial.print(dht11_umidade);
  Serial.print(";");
  Serial.print(dht11_temperatura);
  Serial.print(";");

  float luminosidade =  analogRead(LUMIPIN);
  Serial.print(luminosidade);
  Serial.print(";");

  float lm35_temperatura = analogRead(LM35PIN);
  lm35_temperatura = lm35_temperatura * 0.00488;
  lm35_temperatura = lm35_temperatura * 100;
  Serial.print(lm35_temperatura);
  Serial.print(";");

  int chave = digitalRead(7);
  if (chave == 0)
  {
    Serial.print("1");
  }
  else
  {
    Serial.print("0");
  }

  Serial.println();
  delay(100);
}
```
