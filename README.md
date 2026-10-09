# 5toAzul-David-Makhoul
<img width="2464" height="1642" alt="Photo on 10-1-26 at 1 30 PM" src="https://github.com/user-attachments/assets/9ef467ad-102c-41ab-a066-880688c35b87" />
Tinkercad Usuario:davidmakhoul20@gmail.com Contrasena: sybKoz-mopmaq-wivpy9
<img width="1042" height="634" alt="PHOTO-2026-10-09-00-51-35" src="https://github.com/user-attachments/assets/f8ace0e7-c05f-4abb-89c9-1109d5c81d7a" />
// ===== PINES =====
const int pinPulsador    = 2;
const int pinInterruptor = 3;
const int pinLeds6       = 8;
const int pinLedVerde    = 9;
const int pinLedAzul     = 10;
 
// ===== VARIABLES 6 LEDs =====
bool sistemaActivo = false;
unsigned long inicioFase = 0;
bool faseParpadeo = true;      // true = parpadeando, false = apagado
unsigned long tiempoParpadeo = 0;
bool estadoLed6 = false;
 
const unsigned long DURACION_FASE = 8000;   // 8 segundos cada fase
const unsigned long VELOCIDAD_PARPADEO = 300; // Cambia cada 300 ms
 
// ===== VARIABLES 2 LEDs =====
unsigned long tiempoIntercalado = 0;
const unsigned long VELOCIDAD = 500;
bool toggle = false;
 
void setup() {
  pinMode(pinPulsador, INPUT_PULLUP);
  pinMode(pinInterruptor, INPUT);
  pinMode(pinLeds6, OUTPUT);
  pinMode(pinLedVerde, OUTPUT);
  pinMode(pinLedAzul, OUTPUT);
 
  digitalWrite(pinLeds6, LOW);
  digitalWrite(pinLedVerde, LOW);
  digitalWrite(pinLedAzul, LOW);
}
 
void loop() {
  // ===== PARTE 1: Pulsador arranca el ciclo de parpadeo =====
  int estadoPulsador = digitalRead(pinPulsador);
 
  if (estadoPulsador == LOW && !sistemaActivo) {
    sistemaActivo = true;
    inicioFase = millis();
    faseParpadeo = true;
    tiempoParpadeo = millis();
    estadoLed6 = true;
    digitalWrite(pinLeds6, HIGH);
  }
 
  if (sistemaActivo) {
    unsigned long tiempoActual = millis();
 
    // Cambio de fase cada 8 segundos
    if (tiempoActual - inicioFase >= DURACION_FASE) {
      inicioFase = tiempoActual;
      faseParpadeo = !faseParpadeo;
 
      if (!faseParpadeo) {
        // Empieza fase apagado
        digitalWrite(pinLeds6, LOW);
        estadoLed6 = false;
      } else {
        // Empieza fase parpadeo
        estadoLed6 = true;
        digitalWrite(pinLeds6, HIGH);
      }
    }
 
    // Durante la fase de parpadeo, alternar rápido
    if (faseParpadeo) {
      if (tiempoActual - tiempoParpadeo >= VELOCIDAD_PARPADEO) {
        tiempoParpadeo = tiempoActual;
        estadoLed6 = !estadoLed6;
        digitalWrite(pinLeds6, estadoLed6 ? HIGH : LOW);
      }
    }
  }
 
  // ===== PARTE 2: Interruptor deslizante alterna los 2 LEDs =====
  int estadoInterruptor = digitalRead(pinInterruptor);
 
  if (estadoInterruptor == HIGH) {
    if (millis() - tiempoIntercalado >= VELOCIDAD) {
      tiempoIntercalado = millis();
      toggle = !toggle;
      digitalWrite(pinLedVerde, toggle ? HIGH : LOW);
      digitalWrite(pinLedAzul, toggle ? LOW : HIGH);
    }
  } else {
    digitalWrite(pinLedVerde, LOW);
    digitalWrite(pinLedAzul, LOW);
  }
}
https://www.tinkercad.com/things/bEzW0rxxLcM-cool-bombul/editel?returnTo=https%3A%2F%2Fwww.tinkercad.com%2Fdashboard&sharecode=RA36k2pzXn7skN4pp9Bcrdy8sy3EGcTC2NEyWfLlsSM
<img width="980" height="1280" alt="PHOTO-2026-10-09-00-51-36" src="https://github.com/user-attachments/assets/1f73766c-ad68-4d65-9ab0-d3f6e07ea0bc" />
