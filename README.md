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



