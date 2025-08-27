#include <ESP32Servo.h>//inclue a bliblioteca esp32servo.h

int servo=32;//atribui o pino 32 ao servo

Servo meuServo;//atribui meuServo ao Servo

int sensorUmidade=35;//atribui o pino 35 ao sebsor de umidade do solo
int sensorChuva=34;//atribui o pino 34 ao sensor de chuva

void setup() {
  Serial.begin(9600);//informa qual serial esta utilizando

 meuServo.setPeriodHertz(50);//esta informando os Hz do servo
 meuServo.attach(servo);//assosia o objeto servo s um pino pwm

 pinMode(sensorUmidade,INPUT);//informa para a esp que o sensor é um dado de entrada
 pinMode(sensorChuva,INPUT);//<--


}
void loop() {
 int leituraUmidade=digitalRead(sensorUmidade);
 int leituraChuva=digitalRead(sensorChuva);
//as duas variaveis acima fazem os pinos 34 e 35 serem "lidos"
  meuServo.write(0);//faz o servo retornar a posição inicial
  

   if(leituraChuva==1 && leituraUmidade==0){
      meuServo.write(90);

      //se o sensor de chuva não detectar chuva e o sensor de umidade do solo detectar que o solo esta seco,o servo muda para 90 graus
    }else{
      meuServo.write(0);
      //se não,o servo permanesse parado

    }
    Serial.print(leituraUmidade);
    Serial.println(leituraChuva);
    //faz os valores serem lidos no monitor serial

  delay(1000);
//espera 1 segundo

}
