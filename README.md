#include <LiquidCrystal.h>

// Configuración de pines del LCD: RS, E, D4, D5, D6, D7
LiquidCrystal lcd(12, 11, 5, 4, 3, 2);

// Pines del sistema
const int TMP36_PIN = A0;  // Sensor TMP36
const int LED_PIN = 7;     // LED indicador
const int FAN_PIN = 9;     // Motor/ventilador

float temperatura = 0;

void setup() {
  lcd.begin(16, 2);
  pinMode(LED_PIN, OUTPUT);
  pinMode(FAN_PIN, OUTPUT);
  pinMode(TMP36_PIN, INPUT);

  lcd.print("Sensor TMP36");
  delay(2000);
  lcd.clear();
}

void loop() {
  // Lectura del sensor TMP36
  int valorADC = analogRead(TMP36_PIN);
  float voltaje = (valorADC * 5.0) / 1024.0;
  temperatura = (voltaje - 0.5) * 100.0;  // Conversión a °C

  // Mostrar la temperatura
  lcd.setCursor(0, 0);
  lcd.print("Temp: ");
  lcd.print(temperatura);
  lcd.print(" C   "); // Espacios para limpiar valores anteriores

  // -------------------------------
  // Validación 1: Temperatura <= 10°C
  // -------------------------------
  if (temperatura <= 10) {
    digitalWrite(FAN_PIN, LOW);   // Ventilador apagado
    // Parpadeo del LED
    digitalWrite(LED_PIN, HIGH);
    delay(500);
    digitalWrite(LED_PIN, LOW);
    delay(500);

    lcd.setCursor(0, 1);
    lcd.print("Frio  FAN:OFF  ");
  }

  // -------------------------------
  // Validación 2: 11°C <= Temp <= 25°C
  // -------------------------------
  else if (temperatura > 10 && temperatura <= 25) {
    digitalWrite(LED_PIN, LOW);   // LED apagado
    digitalWrite(FAN_PIN, LOW);   // Ventilador apagado

    lcd.setCursor(0, 1);
    lcd.print("Normal FAN:OFF ");
    delay(1000);
  }

  // -------------------------------
  // Validación 3: Temperatura >= 26°C
  // -------------------------------
  else if (temperatura >= 26) {
    digitalWrite(LED_PIN, HIGH);  // LED encendido fijo
    digitalWrite(FAN_PIN, HIGH);  // Ventilador encendido

    lcd.setCursor(0, 1);
    lcd.print("Calor  FAN:ON  ");
    delay(1000);
  }
}
