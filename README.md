# 🅿️ Fisgon Parking: Monitoreo IoT de Parqueaderos  

---

## 1. Introducción y Resumen del Proyecto  
Este repositorio contiene la implementación completa del proyecto de tesis:  

**DISEÑO E IMPLEMENTACIÓN DE UN SISTEMA PROTOTIPO DE MONITOREO PARA LOS PARQUEADEROS DEL EDIFICIO MATRIZ DEL INSTITUTO SUPERIOR TECNOLÓGICO SUDAMERICANO, QUITO.**

**Fisgon Parking** es un sistema prototipo de monitoreo de disponibilidad de parqueaderos que utiliza **hardware de bajo costo** (módulos ESP) y **sensores ultrasónicos** para ofrecer una solución de gestión en tiempo real.  

El proyecto aborda la necesidad de optimizar el **tiempo de búsqueda** y la **eficiencia en el uso de los estacionamientos institucionales**.  
Los datos de disponibilidad se capturan de forma distribuida y se consolidan en un servidor central, que luego expone una **interfaz web** para su visualización remota.  

---

## 2. Arquitectura del Sistema (IoT Distribuido)  
El sistema opera bajo una **arquitectura de Internet de las Cosas (IoT)** con un modelo de comunicación **Cliente-Servidor (Maestro-Esclavo)** y transmisión de datos ligera vía **UDP**.  

### 2.1 Componentes Principales  

| **Componente**       | **Descripción** | **Tecnologías Clave** |
|-----------------------|-----------------|------------------------|
| **ESP Cliente (Esclavo)** | Módulo de adquisición de datos. Captura la distancia con sensores ultrasónicos, formatea la información y la transmite al servidor. | C/C++ (Arduino), Sensores Ultrasónicos, Comunicación UDP |
| **ESP Servidor (Maestro)** | Núcleo del sistema. Recibe, clasifica y procesa los paquetes UDP de todos los clientes, actualizando las variables de estado de las plazas. | C/C++ (Arduino), Comunicación UDP, Servidor Web HTTP |
| **Interfaz de Monitoreo** | Página web levantada directamente por el ESP Servidor, que visualiza el estado de las plazas en tiempo real usando scripts internos. | HTML, CSS, JavaScript |

---

### 2.2 Flujo Lógico de Funcionamiento  

<div align="center">
   <img src=https://github.com/erequena0999123/FisgonParkingMain/blob/main/Imagenes%20del%20proyecto/Diagrama%20de%20flujo%201.png/>
</div>

1. **Captura de Datos:**  
   Los **ESP Clientes** miden constantemente la distancia de las plazas con sensores ultrasónicos.  

2. **Transmisión:**  
   La información formateada (paquetes de datos) se envía al **ESP Servidor** a través de la red **Wi-Fi** usando el protocolo **UDP (User Datagram Protocol)**, asegurando una transmisión rápida y continua.  

3. **Procesamiento:**  
   El **ESP Servidor** clasifica los paquetes recibidos y actualiza variables internas con la disponibilidad de cada plaza.  

4. **Visualización Remota:**  
   El servidor genera y aloja una **página web** que usa **JavaScript** para indexar y actualizar el estado de las plazas en intervalos definidos, ofreciendo la vista en **tiempo real** a través del túnel **Ngrok**.  

---

## 3. Tecnologías y Lenguajes Implementados  

El proyecto combina **programación embebida de bajo nivel** con **desarrollo web** para la interfaz de usuario.  

| **Categoría**            | **Herramienta**            | **Propósito** |
|---------------------------|-----------------------------|---------------|
| **Programación Embebida** | C / C++ (Arduino)           | Firmware de los módulos ESP Cliente y Servidor |
| **Hardware**              | Módulos ESP (ESP8266/ESP32) | Dispositivos principales para conectividad Wi-Fi y procesamiento |
| **Web Frontend**          | HTML, CSS, JavaScript       | Desarrollo de la interfaz de monitoreo web |
| **IDE Principal**         | Visual Studio Code          | Entorno de desarrollo para código y archivos web |
| **Networking / Túnel**    | Ngrok                       | Creación de un túnel público para acceder al portal web local del ESP Servidor desde Internet |

<div align ="center">
   <img src=https://github.com/erequena0999123/FisgonParkingMain/blob/main/Imagenes%20del%20proyecto/Diagrama%20estructural.png/ width=600>
</div>

---

## 4. Estructura del Repositorio  

El código está organizado siguiendo la **separación de roles** de los módulos **ESP Cliente** y **ESP Servidor**, además de incluir toda la **documentación gráfica** y **archivos de apoyo** necesarios para la implementación y pruebas.  

```bash
Fisgon_Parking/
├── esp_cliente/             # Código fuente para los módulos de adquisición de datos (Esclavos)
│   ├── subarchivo_sensores/ # Separación de las acciones de captura y formateo
│   └── ...
├── esp_servidor/            # Código fuente del módulo central (Maestro)
│   ├── paginas_web/         # Archivos .html y .css del portal web (Archivos de apoyo)
│   ├── subarchivo_udp/      # Módulo de recepción y clasificación de paquetes UDP
│   └── ...
├── docs_esquemas/           # Documentación visual del proyecto
│   ├── imagenes/            # Diagramas, capturas y fotografías del prototipo
│   ├── esquema_electrico/   # Archivos del diseño del circuito
│   └── esquema_logico/      # Diagramas de flujo y UML de la lógica del sistema
└── README.md

```
---

## 5. Visualización del Proyecto  

Esta sección contiene los **diagramas clave** para entender el montaje físico y la lógica del sistema.  

### 5.1 Diagrama de Funcionamiento Lógico (Diagrama de Flujo)  
📌 **Descripción:** Diagrama de flujo que ilustra el proceso continuo de adquisición de datos (**Cliente**), transmisión **UDP**, recepción y clasificación (**Servidor**), y la actualización de la interfaz web.  

<div align="center">
   <img src=https://github.com/erequena0999123/FisgonParkingMain/blob/main/Imagenes%20del%20proyecto/Diagrama%20de%20flujo%202.png/>
</div>

---

### 5.2 Esquema Eléctrico  
📌 **Descripción:** Detalle de las conexiones físicas entre el **microcontrolador ESP** y el **sensor ultrasónico** para la captura de datos de distancia.  

<div align="center">
   <img src= https://github.com/erequena0999123/FisgonParkingMain/blob/main/Esquema%20electrico/Esquema%20electrico%20del%20modulo.png/ width= 600>
</div>

---

### 5.3 Captura de Pantalla del Portal Web  
📌 **Descripción:** Interfaz de usuario que visualiza el **estado actual de los parqueaderos**, destacando visualmente las plazas disponibles.  

<div align = "center">
   <img src=https://github.com/erequena0999123/FisgonParkingMain/blob/main/Imagenes%20del%20proyecto/Funcionamiento%20de%20la%20pagina%20en%20tiempo%20real.png/ width = 900>
</div>

---

## 6. Instalación y Puesta en Marcha  

Para replicar el sistema, necesitarás el **IDE de Arduino** y configurar correctamente las **redes**.  

### 6.1 Requisitos de Software y Hardware  

- **Software:**  
  - IDE de Arduino con soporte para placas **ESP8266/ESP32**  
  - Bibliotecas necesarias: **WiFi.h**, **WiFiUdp.h**  

- **Hardware:**  
  - Módulos ESP (Cliente y Servidor)  
  - Sensores Ultrasónicos (ejemplo: **HC-SR04**)  
  - Fuente de alimentación estable (Módulo **MB-102**)

- **Extra:**  
  - [Consultar el manual de uso](https://github.com/erequena0999123/FisgonParkingMain/blob/main/Manual%20de%20Uso.docx)

---

### 6.2 Configuración de Red  

1. Abre el código en las carpetas:  
   - `esp_cliente/`  
   - `esp_servidor/`  

2. Define las credenciales de la red **Wi-Fi** (`SSID` y `PASSWORD`) en ambos módulos.  

3. Configura las **direcciones IP** (estáticas o dentro de la red local) para la comunicación vía **UDP**.  

---

### 6.3 Despliegue del Portal Web (Túnel Ngrok)  

1. Una vez que el **ESP Servidor** esté ejecutándose y levante el servidor **HTTP local**.  
2. Abre una terminal y ejecuta Ngrok:  

```bash
ngrok http [DIRECCION_LOCAL_DEL_ESP_SERVIDOR]
```

<div align= "center">
   <img src=https://github.com/erequena0999123/FisgonParkingMain/blob/main/Imagenes%20del%20proyecto/Tuner%20ngrok.png/ width= 600>
</div>

3. Accede a la URL pública proporcionada por Ngrok para ver el estado del parqueadero desde cualquier lugar con conexión a Internet.

---

## 7. Autoría y Contacto  

Este proyecto de tesis fue desarrollado como requisito para la obtención del título de **3er Nivel** en **Desarrollo de Software**.  

- 👨‍🎓 **Autor:** Emmanuel Alejandro Requena Tonony
- 🏫 **Institución:** Instituto Superior Tecnológico Sudamericano  
- 📧 **Contacto:** [Perfil en Github](https://github.com/erequena0999123)

---

## 8. Licencia  

Este proyecto se encuentra bajo la licencia **MIT**.  
Consulta el archivo [`LICENSE`](LICENSE.md) para más detalles.  


