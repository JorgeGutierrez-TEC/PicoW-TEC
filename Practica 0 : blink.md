```cp
/*
  Programa: Control de Raspberry Pi Pico W
  Autor: [Jorge Ivan Norige Hernandez, Jonathan  Pelaez FLores , Jorge Gutierrez Pascual ]
  
  Fecha: [29/Abril/2024]

  Descripción:
  Este programa inicializa la comunicación serial en una Raspberry Pi Pico W y envía un mensaje de bienvenida.
  Posteriormente, entra en un bucle infinito donde puede agregar más funcionalidades.

  Licencia: [GPL3]
*/
```
```cpp
void setup() {
  pinMode(LED_BUILTIN, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalWrite(LED_BUILTIN, HIGH);  // turn the LED on (HIGH is the voltage level)
  delay(1000);                      // wait for a second
  digitalWrite(LED_BUILTIN, LOW);   // turn the LED off by making the voltage LOW
  delay(1000);                      // wait for a second
}
```
![image](https://github.com/JorgeGutierrez-TEC/PicoW-TEC/assets/158111129/019923b0-c175-4f0c-a385-0158d7149479)
![image](https://github.com/JorgeGutierrez-TEC/PicoW-TEC/assets/158111129/c84c0e4d-5f82-449e-ba3d-49b02c791c75)

![image](https://github.com/JorgeGutierrez-TEC/PicoW-TEC/assets/158111129/78c7932d-95e7-45b3-b84e-e956fb8d11cc)
![image](https://github.com/JorgeGutierrez-TEC/PicoW-TEC/assets/158111129/4bd5a050-1e87-43b2-ad3e-8574503aa2df)




