# Time-of-flight-vl53l0x
Nicolás Amaro Muñoz Read

Instituto de Innovación y Tecnologia Aplicada

Documentación Técnica sobre el funcionamiento del sensor Time of Flight vl53l0x

RESUMEN:

En esta documentación tecnica se verá de manera simple y breve el funcionamiento del sensor Time of Flight vl53l0x, como hacer su conexión con una Arduino Uno y como hacer conexión de dos o mas sensores. Estos son dispositivos ópticos que utilizan pulsos de luz para medir distancias, tiene un alcance máximo de 4 metros, un tiempo de medición rápido de 20 ms, y se comunica con un microcontrolador a través de I2C. Cuenta con un emisor láser y un detector para la emisión y detección precisa de la luz. Su ángulo de medición de 25 grados permite capturar información en un área específica del entorno.

CODIGO DE EJEMPLO: 
      
  
    //
    #include "Adafruit_VL53L0X.h"

    Adafruit_VL53L0X lox = Adafruit_VL53L0X();

    void setup() {
      Serial.begin(9600);

      // Iniciar sensor
      Serial.println("VL53L0X test");
      if (!lox.begin()) {
        Serial.println(F("Error al iniciar VL53L0X"));
        while(1);
      }
    }


    void loop() {
      VL53L0X_RangingMeasurementData_t measure;

      Serial.print("Leyendo sensor... ");
      lox.rangingTest(&measure, false); // si se pasa true como parametro, muestra por puerto serie datos de debug

      if (measure.RangeStatus != 4)
      {
        Serial.print("Distancia (mm): ");
       Serial.println(measure.RangeMilliMeter);
      }
      else
      {
        Serial.println("  Fuera de rango ");
      }

      delay(100);
    }


