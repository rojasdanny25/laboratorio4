Control de Temperatura con Sensor TMP36 y LCD

Descripción
Este proyecto implementa un sistema de monitoreo de temperatura usando un Arduino UNO, un sensor TMP36, un display LCD 16x2, un LED y un ventilador (motor DC).
El sistema mide la temperatura ambiente, la muestra en pantalla y actúa sobre el LED y el ventilador según tres condiciones de temperatura.

Componentes utilizados

Arduino UNO	1	Microcontrolador principal
Sensor TMP36	1	Sensor de temperatura analógico
LCD 16x2	1	Pantalla para mostrar datos
Potenciómetro 10kΩ	1	Control del contraste del LCD
LED	1	Indicador visual
Resistencia 220Ω	1	Limitadora de corriente para LED
Motor DC o ventilador	1	Actuador controlado por temperatura
Transistor NPN (ej. 2N2222 o TIP120)	1	Control de potencia del ventilador
Diodo 1N4007	1	Protección del motor
Resistencias adicionales (1kΩ aprox.)	1	Para base del transistor

Conexiones

Componente	Pin Arduino	Descripción
TMP36 OUT	A0	Entrada analógica
TMP36 VCC	5V	Alimentación
TMP36 GND	GND	Tierra
LED (con resistencia)	D7	Indicador visual
Base del transistor	D9	Control del ventilador
Emisor del transistor	GND	Retorno
Colector del transistor	Motor –	
Motor +	5V	
LCD RS	D12	Control RS
LCD E	D11	Control Enable
LCD D4–D7	D5–D2	Líneas de datos
LCD RW	GND	Modo escritura
LCD V0	Potenciómetro	Contraste
LCD VSS/VDD	GND / 5V	Alimentación

Código fuente principal (temp_lcd.ino)
El programa realiza las siguientes validaciones según la temperatura medida:

Validación	Condición	Acción
1	Temperatura ≤ 10 °C	LED parpadea y ventilador apagado
2	11 °C ≤ Temperatura ≤ 25 °C	LED y ventilador apagados
3	Temperatura ≥ 26 °C	LED encendido fijo y ventilador encendido

La temperatura se muestra en el LCD junto con el estado del ventilador.


Instrucciones de uso

Ensambla el circuito siguiendo las conexiones indicadas.
Abre el IDE de Arduino o Tinkercad Circuits.
Carga el archivo temp_lcd.ino.
Abre el monitor serial o verifica la lectura en el LCD.
Cambia la temperatura (simulada o real) y observa el comportamiento del LED y ventilador.

Autor

Juan Camilo Yampuezan
Danny Esneyder Rojas
Brandon Delgado Yesid

Universidad CESMAG
Espacio académico: Sistemas Operativos – Laboratorio 4
Docente: joan ayala
