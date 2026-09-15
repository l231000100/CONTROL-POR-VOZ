# Control de un Robot por Comandos de Voz 🎤🤖

Práctica de preparatoria que integra reconocimiento de voz, comunicación WiFi y control de motores con Arduino.

**Autores:** Iván Luna, Daniel Bustamante

---

## 📋 Descripción

El sistema permite controlar por voz:
- Un LED individual
- Una matriz de LEDs
- Un motorreductor con rueda, mediante un puente H (L298N)

El flujo es: **celular (voz) → app en App Inventor → WiFi → Arduino → hardware**

---

## 🛠️ Materiales

| Componente | Cantidad |
|---|---|
| Arduino UNO R4 WiFi | 1 |
| Módulo puente H (L298N) | 1 |
| Motorreductor con rueda | 1 |
| LED individual | 1 |
| Matriz de LEDs | 1 |
| Batería LiPo 11.1V / 3S / 450 mAh | 1 |
| Celular Android | 1 |
| Cables y protoboard | — |

---

## 🔌 Conexiones

| Arduino | L298N |
|---|---|
| Pin 4 | IN1 |
| Pin 5 | IN2 |
| Pin 6 | ENA |

| Arduino | Otros |
|---|---|
| Pin 13 | LED |
| Pines 8, 9, 10, 12 | Matriz de LEDs |

> ⚠️ El módulo L298N tiene 3 jumpers: **ENA** y **ENB** se retiran para controlar la velocidad desde el Arduino, pero el jumper del **regulador de 5V** debe quedarse puesto si usas una batería de 7-12V (como la LiPo de 11.1V de este proyecto). Sin él, el chip no tiene alimentación lógica y no responde a ningún comando.

---

## 💻 Código Arduino

Archivo: `control_por_voz_r4wifi.ino`

El Arduino crea su propia red WiFi (`RobotVoz`) y levanta un servidor que recibe comandos como peticiones HTTP:

```
http://192.168.4.1/avanzar
http://192.168.4.1/led-on
```

### Comandos disponibles

| Comando | Acción |
|---|---|
| `led-on` / `led-off` | Enciende / apaga el LED |
| `matriz-on` / `matriz-off` | Enciende / apaga la matriz |
| `avanzar` | Motor gira hacia adelante |
| `retroceder` | Motor gira en reversa |
| `alto` | Detiene el motor |
| `baja` | Velocidad PWM 10 |
| `media` | Velocidad PWM 127 |
| `maxima` | Velocidad PWM 255 |

---

## 📱 App de voz (MIT App Inventor)

Componentes usados:
- **SpeechRecognizer** — convierte la voz en texto
- **Web** — envía el comando por HTTP al Arduino
- **Labels** — muestran el texto reconocido y la respuesta del Arduino

Lógica: al presionar "Hablar", se transcribe la voz → se compara contra palabras clave (`contains`) → se arma la URL con el comando → se envía con `Web1.Get`.

---

## 🚀 Cómo correr la práctica

1. Sube `control_por_voz_r4wifi.ino` al Arduino UNO R4 WiFi.
2. Conecta el hardware según la tabla de conexiones.
3. Conecta el celular a la red WiFi `RobotVoz` (contraseña `12345678`).
4. Abre la app de App Inventor y presiona "Hablar".
5. Di un comando, por ejemplo: *"avanzar"*.

---

## 🐞 Problemas conocidos

- Si el motor gira directo a la batería pero no a través del L298N → revisa el jumper del regulador de 5V.
- Si el reconocimiento de voz falla por frases con palabras extra → usa comparación por `contains` en vez de texto exacto.

---

## 📄 Documentación adicional

Ver `Reporte_Practica_ControlPorVoz.docx` para el reporte completo de la práctica.
