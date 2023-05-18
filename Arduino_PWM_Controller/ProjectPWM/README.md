1- PWM é uma técnica utilizada para controlar a intensidade média de um sinal digital através da variação do ciclo de trabalho. O ciclo de trabalho se refere à proporção entre o tempo em que o sinal está em um estado ativo (geralmente alto) e o tempo total do ciclo.
O PWM é frequentemente utilizado para controlar a potência de dispositivos elétricos, como motores, lâmpadas LED, servomotores e ventiladores. Ao variar o ciclo de trabalho do sinal PWM, é possível ajustar a média da potência fornecida a esses dispositivos, permitindo, por exemplo, ajustar a velocidade de um motor ou a intensidade de uma luz. É uma técnica amplamente utilizada na eletrônica e é suportada por muitos microcontroladores e circuitos integrados, facilitando seu uso em uma variedade de aplicações.

2- Os componentes necessários são: Ociloscópio, botão, resistor, ponte H, Arduino Nano, motor e bateria

3-

- [PDF](file:///C:/Users/Bruno/Documents/PlatformIO/Projects/ProjectPWM/Microcontrolador2.PDF)

4-

```javascript
#include <Arduino.h>


#define BUTTON_PIN 2
#define PWM 9


int estado_botao = 0;
int pwm = 0;
int ultimo_estado_botao = 0;
unsigned long tempo_acionado = 0;
unsigned long tempo_delay = 50;

void setup() {
  pinMode(PWM, OUTPUT);
  pinMode(BUTTON_PIN, INPUT_PULLUP);
}

void loop() {

  int leitura = digitalRead(BUTTON_PIN);

  if (leitura != ultimo_estado_botao) {
    ultimo_estado_botao = leitura;
    if (leitura == HIGH) {  
      tempo_acionado = millis();
    }
  }

  if (leitura == HIGH && ((millis() - tempo_acionado) > tempo_delay)) {
    pwm = pwm + 64;
    
    if (pwm > 256){
        pwm = 0;
    }
  }

  analogWrite(PWM, pwm);
  
}
```