
**Práctica 3: Servidor Web con Pico W para Controlar un LED**
**Objetivo**
Desarrollar un servidor web utilizando el microcontrolador Raspberry Pi Pico W, programado en C/C++, que permita controlar el estado de un LED a través de una interfaz web.

**Requisitos del Proyecto**
Configuración del Hardware: Leer documentacion de Pico W del LED interno (no requiere uno externo).
Configuración de Red: Establecer una conexión WiFi con el Pico W para permitir el acceso remoto.
Servidor Web: Implementar un servidor web en el Pico W que pueda recibir comandos a través de HTTP para controlar el LED.
Interfaz de Usuario Web: Crear una página web sencilla con botones para "Encender" y "Apagar" el LED.
Control del LED: Programar la lógica en C/C++ para que el Pico W pueda encender y apagar el LED basándose en las solicitudes recibidas del servidor web.

**Descripción Adicional**
Utilizar bibliotecas y herramientas adecuadas para la configuración del servidor web en el Pico W.
Asegurarse de que el código esté bien documentado, explicando cómo se configura la red y se manejan las solicitudes HTTP.
Incluir medidas básicas de seguridad para la conexión WiFi y el acceso al servidor web.

CODIGO EN C
```c
#include "lwip/apps/httpd.h"
#include "pico/stdlib.h"
#include "pico/cyw43_arch.h"
#include "lwipopts.h"
#include "ssi.h"
#include "cgi.h"

// WIFI Credentials - take care if pushing to github!
const char WIFI_SSID[] = "XXX";
const char WIFI_PASSWORD[] = "XXX";

int main() {
    stdio_init_all();

    cyw43_arch_init();

    cyw43_arch_enable_sta_mode();

    // Connect to the WiFI network - loop until connected
    while(cyw43_arch_wifi_connect_timeout_ms(WIFI_SSID, WIFI_PASSWORD, CYW43_AUTH_WPA2_AES_PSK, 30000) != 0){
        printf("Attempting to connect...\n");
    }
    // Print a success message once connected
    printf("Connected! \n");
    
    // Initialise web server
    httpd_init();
    printf("Http server initialised\n");

    // Configure SSI and CGI handler
    ssi_init(); 
    printf("SSI Handler initialised\n");
    cgi_init();
    printf("CGI Handler initialised\n");
    
    // Infinite loop
    while(1);
}
```
**Codigo de la Pagina html**
```html
<!DOCTYPE html>
<html>
    <head> 
        <title>PicoW Webserver</title> 
    </head>
    <body> <h1>PicoW Webserver Tutorial</h1>
        <br>
        <h2>This bit is SSI:</h2>
        <p>Voltage: <!--#volt--></p>
        <p>Temp: <!--#temp--> C</p>
        <p>LED is: <!--#led--></p>
        <br>
        <h2>This bit is CGI:</h2>
        <a href="/led.cgi?led=1"><button>LED ON</button></a>
        <a href="/led.cgi?led=0"><button>LED OFF</button></a>
        <br>
        <br>
        <a href="/index.shtml">Refresh</a>
   </body>
</html>
```

Se presiona el boton de ON para encender el led.
![IMG_8530](https://github.com/JorgeGutierrez-TEC/PicoW-TEC/assets/133905295/1b75bbbb-561b-4cc9-b50c-bb14899ebd8e)
LED ENCENDIDO
![cbf92935-0d36-4e93-b1e7-8be95f113264](https://github.com/JorgeGutierrez-TEC/PicoW-TEC/assets/133905295/d333db9a-3337-4519-aa4b-4f1d61524720)

Se presiona el boton de OFF para apagar el led.
![IMG_8531](https://github.com/JorgeGutierrez-TEC/PicoW-TEC/assets/133905295/4ecb711a-e8d0-481d-904c-bc52136a336e)
LED APAGADO
![IMG_8563](https://github.com/JorgeGutierrez-TEC/PicoW-TEC/assets/133905295/2a0e2b4c-bb17-472d-a59b-6db42f876416)
