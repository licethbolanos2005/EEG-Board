# Implementación de un Electroencefalógrafo

Este repositorio contiene los archivos necesarios para la fabricación de una placa de circuito impreso (PCB) para un sistema de adquisición de señales EEG (electroencefalográficas). El proyecto tiene como objetivo el desarrollo de un electroencefalógrafo de bajo costo y tamaño compacto, con componentes de montaje superficial (SMD), orientado a aplicaciones educativas, de investigación y prototipado de interfaces cerebro-computador (BCI).

## Esquemático del Sistema

A continuación se muestra el esquemático general del sistema:

![Esquemático](https://github.com/user-attachments/assets/4d9724cc-cd09-4b98-9f4d-6cce8367407a)

El diseño está organizado en los siguientes bloques funcionales:

### USB Power Circuit
Circuito de entrada de alimentación desde USB, con etapa de carga y protección. Permite alimentar el sistema mediante una batería recargable Li-Po.

### 3V3 Regulator
Regulador de voltaje a 3.3V utilizado por múltiples componentes del sistema, incluyendo el microcontrolador.

### Reference Circuit
Generador de voltaje de referencia común (a través del REF2033) utilizado tanto por el amplificador de instrumentación como por los filtros activos. Este voltaje proporciona una referencia estable de 1.65V para el correcto procesamiento de señales en sistemas de un solo riel.

### EEG Signal Acquisition
Etapa principal de adquisición de señal bioeléctrica. Utiliza un amplificador de instrumentación **AD8226ARZ**, ideal para aplicaciones biomédicas debido a su bajo ruido y alta CMRR. La señal EEG se obtiene a través de un conector jack TRS de 3.5 mm.

### Active Filters

- **Filtro Pasa Bajo de 70 Hz**: Elimina componentes de alta frecuencia.
- **Filtro Pasa Alto de 0.5 Hz**: Elimina componentes de muy baja frecuencia.
  
Ambos filtros están referenciados al voltaje generado por el circuito REF2033.

### Non-Inverting Amplifier
Etapa de ganancia adicional con referencia a 1.65V para adaptar la señal EEG a un rango óptimo de entrada analógica del microcontrolador.

### Embedded System: ESP32-S3
Microcontrolador principal encargado del muestreo y procesamiento digital de las señales EEG. También permite transmitir los datos mediante Wi-Fi o Bluetooth. Se utilizan sus entradas analógicas para leer la señal final procesada.

### ESP32 Connectors
Pines I2C disponibles para la conexión con una pantalla OLED externa, permitiendo visualización local de datos o estado del sistema.

## Componentes

Todos los componentes utilizados son de montaje superficial (SMD), lo que permite una construcción compacta y apta para procesos automatizados de soldadura. Esto es especialmente útil en prototipos de investigación que requieren repetibilidad, bajo consumo y mínima interferencia electromagnética.

## Estructura del Repositorio

Este repositorio contiene los archivos Gerber necesarios para la fabricación de la PCB. Se divide en dos carpetas principales:

### DemonstrationVideo

Esta carpeta contiene un video demostrativo del sistema electroencefalográfico implementado. En la prueba se utilizaron electrodos de cloruro de plata colocados en la frente (dos canales) y en la mano (referencia). La señal adquirida se visualiza en tiempo real, evidenciando el funcionamiento del sistema.

### DrillFiles

- `drill_1_16.xln`: Archivo de perforado (formato Excellon) que define los agujeros en la PCB, utilizados para conexiones internas, stitching y enrutamiento entre capas.

### GerberFiles

| Archivo                    | Descripción                                 |
|---------------------------|---------------------------------------------|
| `copper_bottom.gbr`       | Capa de cobre inferior                      |
| `copper_top.gbr`          | Capa de cobre superior                      |
| `gerber_job.gbrjob`       | Archivo de configuración del trabajo Gerber|
| `profile.gbr`             | Contorno o borde mecánico de la placa      |
| `silkscreen_top.gbr`      | Serigrafía superior (etiquetado)           |
| `soldermask_bottom.gbr`   | Máscara de soldadura inferior              |
| `soldermask_top.gbr`      | Máscara de soldadura superior              |

Estos archivos pueden ser enviados directamente a un fabricante de PCBs (como JLCPCB, PCBWay, etc.).

## Aplicaciones

- Captura y análisis de señales EEG para entornos educativos.
- Estudios básicos de neurociencia.
- Prototipos de interfaces cerebro-computador (BCI).
- Dispositivos portátiles de investigación biomédica.

## Observaciones

- La señal EEG procesada es analógica y puede visualizarse o digitalizarse mediante el ADC del ESP32-S3.
- El diseño considera una referencia virtual de 1.65V para operar correctamente con alimentación unipolar (3.3V).
- Se sugiere utilizar electrodos pasivos con conexión TRS para una mejor compatibilidad con el sistema.

## Autores

- Santiago Albarracín (https://github.com/Inconig9-hub)
- Liceth Bolaños      (https://github.com/licethbolanos2005)
- Arlyn Cardozo       (https://github.com/ArlynCardozo)
- Samuel Guevara      (https://github.com/samueldavid123-gif)
