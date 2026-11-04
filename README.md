# 🤖 Pepper Robot Choreography (Python + NAOqi)

> **EN:** Python script that makes SoftBank's **Pepper** humanoid robot perform a choreography: base movement, arm and head joint interpolation, a bow and a 360° turn, with synchronized speech. It uses the **NAOqi** SDK (ALMotion, ALRobotPosture, ALTextToSpeech). Demo videos are included.

Script en **Python** que controla al robot humanoide **Pepper** (SoftBank Robotics) para ejecutar una coreografía con movimiento de la base, articulaciones de brazos y cabeza, reverencia y giro completo, mientras habla en cada paso. Usa los módulos de **NAOqi**.

![Python](https://img.shields.io/badge/Python-2.7-3776AB?logo=python&logoColor=white)
![NAOqi](https://img.shields.io/badge/SDK-NAOqi-00A0DC)
![Robot](https://img.shields.io/badge/Robot-Pepper-lightgrey)

---

## 🎥 Demo

Los videos [`1.mp4`](1.mp4) y [`2.mp4`](2.mp4) muestran a Pepper ejecutando la coreografía.

## Secuencia de la coreografía

| # | Movimiento | API NAOqi |
|---|---|---|
| 0 | Despertar y postura inicial *"Hola, estoy listo para bailar"* | `wakeUp()`, `goToPosture("StandInit")` |
| 1 | Avanza 30 cm y levanta el brazo derecho | `moveTo(0.3, 0, 0)`, `angleInterpolationWithSpeed("RShoulderPitch", …)` |
| 2 | Retrocede y cambia al brazo izquierdo | `moveTo(-0.3, 0, 0)`, `LShoulderPitch`, `LElbowYaw` |
| 3–4 | Desplazamiento lateral derecha e izquierda | `moveTo(0, ±y, 0)` |
| 5 | Giro de cabeza ±45° | `angleInterpolation("HeadYaw", …)` |
| 6 | Reverencia (cadera y rodilla) | `HipPitch`, `KneePitch` |
| 7 | Giro completo de 360° y descanso | `moveTo(0, 0, 2π)`, `rest()` |

## Cómo ejecutarlo

Requisitos: un robot Pepper en la misma red, **Python 2.7** y el SDK **NAOqi**. Choregraphe es opcional.

```bash
# 1. Copiar el script al robot
scp robot.py nao@<IP_DEL_ROBOT>:~/

# 2. Conectarse y ejecutarlo dentro del robot (robotIP = 127.0.0.1 en el script)
ssh nao@<IP_DEL_ROBOT>
python robot.py
```

> Para ejecutarlo desde un PC en vez del robot, cambia `robotIP` en `robot.py` por la IP de Pepper.

## Archivos

| Archivo | Contenido |
|---|---|
| `robot.py` | Script de la coreografía |
| `Proyecto Pepper.pdf` / `Pepper.tex` | Informe técnico (LaTeX) |
| `1.mp4`, `2.mp4` | Videos de demostración |

## Conceptos aplicados

- Control de un robot humanoide con proxies remotos (`ALProxy`) sobre la red.
- Interpolación de ángulos articulares con control de velocidad.
- Locomoción omnidireccional de la base (`moveTo` en x, y, θ).
- Sincronización de voz y movimiento.

---

Autores: **Miguel Ángel Jiménez Morales** y **Dikersson Alexis Cañón Vanegas**. Ingeniería de Telecomunicaciones, Universidad Santo Tomás, abril de 2025.
