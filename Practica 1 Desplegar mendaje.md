```cpp
/*
  Programa: Programa Desplegar Mensaje
  Autor:    Noriega Hernandez Jorge Ivan / Gutierrez Pascual Jorge / Pelaez Flores Jhonatan
  Fecha: 10 / mayo / 2024

  Descripción:
 Programa Desplegar Mensaje

  Licencia: Active Learning Labs
  Harvard University 
*/
```

Desplegar mensaje "Hello World"


```cpp
void setup() {
  // put your setup code here, to run once:

}

void loop() {
  // put your main code here, to run repeatedly:
 Serial.println("Hello World");
  // Retraso mínimo para evitar saturar el bucle.
  delay(100);
}

```
![image](https://github.com/JorgeGutierrez-TEC/PicoW-TEC/assets/158111129/cb3b8b5c-9e41-4052-989b-5532bc690f0e)


4.1 (PRACTICA 1) Practicas Csharp PicoW

CÓDIGO EN ARDUINO
```cpp
// Código de Arduino
String incomingData; // Cadena para almacenar los datos entrantes

void setup() {
  Serial.begin(9600); // Inicializa la comunicación serial a 9600 baudios
}

void loop() {
  // Verifica si hay datos disponibles en el puerto serial
  if (Serial.available() > 0) {
    // Lee los datos entrantes y los almacena en la cadena incomingData
    incomingData = Serial.readString();

    // Imprime los datos recibidos en la consola de Arduino
    Serial.print("Mensaje recibido: ");
    Serial.println(incomingData);
  }
}
```
![image](https://github.com/JorgeGutierrez-TEC/PicoW-TEC/assets/158111129/c3dbd933-6f9d-419b-b8e2-346c330186de)

CÓDIGO EN C#
```cpp
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.IO.Ports;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace holaMundo
{
    public partial class Form1 : Form
    {
        private SerialPort serialPort;
        public Form1()
        {
            InitializeComponent();
            PopulateComPorts();
        }
        private void PopulateComPorts()

        { 
            string[] ports = SerialPort.GetPortNames();

            cmbPorts.Items.AddRange(ports);
        }
        private void button1_Click(object sender, EventArgs e)
        {
            if (cmbPorts.SelectedItem != null)

            {
                string selectedPort = cmbPorts.SelectedItem.ToString();

                serialPort = new SerialPort(selectedPort, 9600, Parity.None, 8, StopBits.One);
                try
                {
                    serialPort.Open();
                    MessageBox.Show("Conectado al puerto " + selectedPort);
                }
                catch (Exception ex)
                {
                    MessageBox.Show("Error al conectar: " + ex.Message);
                }
            }
            else
            {
                MessageBox.Show("Seleccione un puerto válido");
            }
        }

        private void button2_Click(object sender, EventArgs e)
        {
            if (serialPort != null && serialPort.IsOpen)
            {
                serialPort.Close();
                MessageBox.Show("Desconectado del puerto");
            }
            else
            {
                MessageBox.Show("No hay conexión activa");
            }
        }

        private void button3_Click(object sender, EventArgs e)
        {
            txtBoxMensaje.Clear();
        }

        private void button4_Click(object sender, EventArgs e)
        {
            if (serialPort != null && serialPort.IsOpen)
            {
                string message = txtBoxMensaje.Text.Trim();

                if (!string.IsNullOrEmpty(message))
                {
                    serialPort.Write(message);
                    txtBoxMensaje.Clear();
                }
            }
            else
            { 
                MessageBox.Show("No hay conexión activa");
            }
        }
    }
}

```
![image](https://github.com/JorgeGutierrez-TEC/PicoW-TEC/assets/158111129/9f9217b0-fd4d-4436-9234-c833b6fcb798)


