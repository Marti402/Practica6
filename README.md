# Practica6: BUSOS DE COMUNICACIO 2/ SPI
## Introducció:
En la práctica anterior, exploramos los buses de comunicación. Ahora, en esta práctica, continuaremos con ese estudio, concentrándonos especialmente en el bus SPI.

La práctica constará de: 
 - Lectura i escritura de la memoria SD
 - Lectura de la etiqueta RFID


## EJERCICIO 1 
```c++
#include <SPI.h>
#include <SD.h>
File myFile;
void setup()
{
Serial.begin(9600);
Serial.print("Iniciando SD ...");
if (!SD.begin(4)) {
Serial.println("No se pudo inicializar");
return;
}
Serial.println("inicializacion exitosa");
myFile = SD.open("archivo.txt");
if (myFile) {
Serial.println("archivo.txt:");
while (myFile.available()) {
Serial.write(myFile.read());
}
myFile.close(); //cerramos el archivo
} else {
Serial.println("Error al abrir el archivo");
}
}
void loop()
{
}
```
Este código inicializa una tarjeta SD, luego abre un archivo llamado "archivo.txt". Una vez abierto, lee el contenido del archivo y lo envía a través del puerto serie, y finalmente cierra el archivo.

###**El "void setup"**: 

Este subprograma configura la comunicación serial, intenta inicializar la tarjeta SD en el pin 4, abre el archivo "archivo.txt" si la inicialización tiene éxito, y lee su contenido para enviarlo a través de la comunicación serial.

**En este caso el *"void loop()"* no contiene instrucciones**

## EJERCICIO 2

```c++
#include <SPI.h>
#include <MFRC522.h>
#define RST_PIN 9 
#define SS_PIN 10 
MFRC522 mfrc522(SS_PIN, RST_PIN); 
void setup() {
Serial.begin(9600); 
SPI.begin(); 
mfrc522.PCD_Init(); 
Serial.println("Lectura del UID");
}
void loop() {

if ( mfrc522.PICC_IsNewCardPresent())
{
//Seleccionamos una tarjeta
if ( mfrc522.PICC_ReadCardSerial())
{
// Enviamos serialemente su UID
Serial.print("Card UID:");
for (byte i = 0; i < mfrc522.uid.size; i++) {
Serial.print(mfrc522.uid.uidByte[i] < 0x10 ? " 0"
: " ");
Serial.print(mfrc522.uid.uidByte[i], HEX);
}
Serial.println();
// Terminamos la lectura de la tarjeta actual
mfrc522.PICC_HaltA();
}
}
}
```




