```cpp
/*
  Programa: Programa Programacion OLED Dispositivo
  Autor:    Noriega Hernandez Jorge Ivan / Gutierrez Pascual Jorge / Pelaez Flores Jhonatan
  Fecha: 10 / mayo / 2024

  Descripción:
 Programa OLED Dispositivo

  Licencia: Active Learning Labs
  Harvard University 
*/
```

Objetivo
Desarrollar un programa en C/C++ que permita mostrar un mensaje en un display OLED, facilitando la comprensión del manejo de displays gráficos y la programación en C/C++.

Requisitos del Proyecto
Configuración del Display: Inicializar y configurar el display OLED para asegurar la correcta visualización de los mensajes.
Interfaz de Usuario: Implementar una función que permita al usuario introducir el mensaje que desea desplegar.
Despliegue del Mensaje: Programar la lógica necesaria para que el mensaje introducido por el usuario se muestre correctamente en el display OLED.

Codigo del proyecto
```cpp
#include <Wire.h>
#include <Adafruit_GFX.h>
#include <Adafruit_SSD1306.h>

#define SCREEN_WIDTH 128
#define SCREEN_HEIGHT 64
#define OLED_RESET -1

Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, OLED_RESET);

void setup() {
  Serial.begin(9600);
  
  if(!display.begin(SSD1306_SWITCHCAPVCC, 0x3C)) { 
    Serial.println(F("Error al iniciar la pantalla OLED"));
    for(;;);
  }
  
  display.display();
  delay(2000);
  display.clearDisplay();
}

void loop() {
  display.setTextSize(1);
  display.setTextColor(SSD1306_WHITE);
  display.setCursor(0,0);
  display.print("hola bunas nochs");
  display.display();
  
  delay(1000);
  display.clearDisplay();
}

```

Resultados del proyecto en simulador
![image](https://github.com/JorgeGutierrez-TEC/PicoW-TEC/assets/158111129/78c7932d-95e7-45b3-b84e-e956fb8d11cc)
![image](https://github.com/JorgeGutierrez-TEC/PicoW-TEC/assets/158111129/4bd5a050-1e87-43b2-ad3e-8574503aa2df)

Resultados en fisico 
![image](https://github.com/JorgeGutierrez-TEC/PicoW-TEC/assets/158111129/d3b83ffc-6095-4e28-ac1c-70a1b1909690)
![image](https://github.com/JorgeGutierrez-TEC/PicoW-TEC/assets/158111129/07619ba2-ac2b-4e11-b6ca-0d625876fffb)



