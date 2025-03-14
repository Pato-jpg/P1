*SANDRA COTS. P1*

**INFORME PRÁCTICA 1**

**Blink con ESP32**

**2. Introducción**

El objetivo de esta práctica es implementar un programa que permita el parpadeo periódico de un LED utilizando el microcontrolador **ESP32**. Además, se utilizará el **puerto serie** para depurar el programa y se explorará el **acceso directo a los registros** de entrada/salida.

**3. Código**

**Código básico**

#define LED\_BUILTIN 2

#define DELAY 500

void setup() {

`    `pinMode(LED\_BUILTIN, OUTPUT);

}

void loop() {

`    `digitalWrite(LED\_BUILTIN, HIGH);

`    `delay(DELAY);

`    `digitalWrite(LED\_BUILTIN, LOW);

`    `delay(DELAY);

}

**Código con envío de datos por puerto serie**

#define LED\_BUILTIN 2

#define DELAY 1000

void setup() {

`    `pinMode(LED\_BUILTIN, OUTPUT);

`    `Serial.begin(115200);

}

void loop() {

`    `digitalWrite(LED\_BUILTIN, HIGH);

`    `Serial.println("ON");

`    `delay(DELAY);

`    `digitalWrite(LED\_BUILTIN, LOW);

`    `Serial.println("OFF");

`    `delay(DELAY);

}

**Código con acceso directo a registros**

#define LED\_BUILTIN 2

#define DELAY 1000

void setup() {

`    `pinMode(LED\_BUILTIN, OUTPUT);

`    `Serial.begin(115200);

}

void loop() {

`    `uint32\_t \*gpio\_out = (uint32\_t \*)GPIO\_OUT\_REG;

`    `\*gpio\_out |= (1 << LED\_BUILTIN);  // Encender LED

`    `Serial.println("ON");

`    `delay(DELAY);

`    `\*gpio\_out ^= (1 << LED\_BUILTIN);  // Apagar LED

`    `Serial.println("OFF");

`    `delay(DELAY);

}

**4. Diagrama de Flujo**

\## Diagrama de Flujo

![Diagrama de Flujo](diagrama\_flujo.png)

**5. Diagrama de Tiempos**

\## Diagrama de Tiempos

![Diagrama de Tiempos](diagrama\_tiempos.png)

**6. Respuesta a la Pregunta 6**

**Tiempo Libre del Procesador**

En el programa básico con delay(500), el procesador pasa la mayor parte del tiempo en estado de espera, ya que la función delay() **bloquea la ejecución del código** durante el tiempo especificado. Durante este tiempo, el procesador **no realiza ninguna tarea útil**, por lo que el tiempo libre es de aproximadamente **500 ms** en cada ciclo de encendido y apagado del LED.

Cuando se eliminan los delay() y se accede directamente a los registros, el procesador puede **realizar otras tareas** en el tiempo que antes se dedicaba a la espera, lo que **aumenta la eficiencia** del programa.

**Conclusión**

En esta práctica se ha aprendido a **controlar un LED** utilizando el microcontrolador **ESP32**, tanto con funciones de **Arduino** como con **acceso directo a los registros**. Además, se ha explorado el **uso del puerto serie** para depurar el programa y se ha analizado el **tiempo libre del procesador** en diferentes configuraciones.
