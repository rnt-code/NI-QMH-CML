# NI QMH Continuous Measurement and Logging Documentation

## Documentación Oficial de NI

# Continuous Measurement and Logging (CML)

Este proyecto de ejemplo implementa un sistema de **medición y registro continuos** utilizando el patrón **Queued Message Handler (QMH)**. La aplicación adquiere datos en forma continua, los visualiza y los registra en disco, permitiendo además interacción fluida con la interfaz de usuario.

## 🧩 Arquitectura general

El VI principal (`Main.vi`) ejecuta cinco bucles en paralelo, cada uno con responsabilidades específicas:

* **Manejo de eventos** (`Main.vi`)
  Event Handling Loop (EHL) que detecta eventos del panel frontal, como clics en los botones "Start" o "Settings".

* **Mensajería de la interfaz de usuario** (`Main.vi`)
  Message Handling Loop (UI MHL) que recibe mensajes del EHL y los distribuye al resto de los módulos.

* **Adquisición de datos** (`Acquisition.lvlib:Acquisition Message Loop.vi`)
  MHL responsable de adquirir datos de forma continua. En esta plantilla, se simulan los datos por defecto.

* **Registro de datos** (`Logging.lvlib:Logging Message Loop.vi`)
  MHL que registra los datos adquiridos en disco utilizando el formato TDMS.

* **Visualización de datos** (`Main.vi`)
  Un bucle `While` que actualiza el gráfico de forma de onda con los datos más recientes.

> Este proyecto también incluye un diálogo de configuración (`Settings.lvlib`) para definir parámetros de funcionamiento, como la ruta del archivo de log.

---

## 🧰 Requisitos del sistema

* LabVIEW Base, Full o Professional Development System.
* NI-DAQmx o cualquier otro controlador compatible para hardware de adquisición o instrumentación.

---

## 📊 Casos de uso

El ejemplo CML está diseñado para aplicaciones de medición continua que requieren:

* Adquisición y registro ininterrumpidos.
* Interfaz de usuario siempre receptiva, incluso durante operaciones intensivas.

---

## ▶️ Ejecución

1. Abrir y ejecutar `Main.vi` desde el **Project Explorer**.
2. Hacer clic en **Start** para iniciar la simulación de adquisición de datos.
3. Interactuar con los demás botones del panel frontal para explorar las funcionalidades.

---

## 🛠️ Modificación para adquisición real

Para adaptar el proyecto al uso con hardware de adquisición real:

1. **Agregar referencias de hardware** en
   `Acquisition.lvlib:Hardware Configuration.ctl`
   Ejemplos: DAQ tasks, canales DAQ, sesiones VISA.

2. **Inicializar hardware** en
   `Acquisition.lvlib:Initialize Hardware References.vi`
   Ejemplos: `DAQmx Create Virtual Channel`, `Instrument Driver Initialize`.

3. **Configurar hardware** en
   `Acquisition.lvlib:Configure Hardware.vi`
   Ejemplos: `DAQmx Timing`, `DAQmx Trigger`, `Configure Measurement`, `Configure Autozero`.

4. **Leer datos** en
   `Acquisition.lvlib:Acquire.vi`
   Ejemplos: `DAQmx Read`, `Instrument Driver Read`.

5. **Detener adquisición** en
   `Acquisition.lvlib:Stop Acquisition.vi`
   Ejemplos: `DAQmx Clear Task`, `Instrument Driver Close`.

---

## 📝 Personalización del registro de datos

Puede modificar el comportamiento de registro según sus necesidades:

* **Ruta del archivo**
  Desde el diálogo de configuración (Settings), cambiar el campo **Log File Path**. Por defecto:
  `...\LabVIEW Data\Logged Data.tdms`.

* **Mecanismo de registro**
  Modificar `Logging.lvlib:Logging Message Loop.vi` para registrar a disco, red u otro destino.

* **Formato de escritura**
  Modificar `Logging.lvlib:Log Data.vi`. Se puede reemplazar el formato TDMS por funciones como:
  `Export Waveforms to Spreadsheet File`, `Write to Spreadsheet File`.

* **Configuración de archivo/log**
  Modificar `Logging.lvlib:Logging Configuration.ctl` para ajustar rutas o referencias necesarias para el log.

---
Fin documentación oficial

