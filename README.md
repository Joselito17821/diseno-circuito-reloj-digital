# ⏰ Diseño de Sistemas Digitales – Reloj Digital Síncrono

Este proyecto implementa un **reloj digital síncrono de 24 horas** (00:00:00 a 23:59:59) desarrollado en **Logisim Evolution**. Está construido con **flip-flops tipo T**, **contadores BCD diseñados manualmente** y **decodificadores de 7 segmentos**, e incluye una **alarma programable** hecha únicamente con compuertas lógicas (sin comparadores dedicados).

---

## ▶ Ejecución

Este diseño está pensado para ejecutarse en **Logisim Evolution**.

1. Abre el archivo `relojDigital.circ` en Logisim Evolution.
2. Activa la simulación (`Simulate > Ticks Enabled`) y configura la frecuencia a **1 Hz** (`Simulate > Tick Frequency`).
3. Para programar la alarma, usa el pulsador de clock manual de cada contador del subcircuito `Alarma`.
4. Cuando la hora del reloj coincide con la de la alarma, se enciende el LED de alarma durante todo el minuto.

---

## 🧪 Lógica del sistema

### Contadores (flip-flops tipo T)

| Contador | Estados | Flip-flops | Uso |
|----------|---------|------------|-----|
| 0 a 9 | 10 | 4 | Unidades de segundos, minutos y horas |
| 0 a 5 | 6 | 3 | Decenas de segundos y minutos |
| 0 a 2 | 3 | 2 | Decenas de horas |

Para cada contador se desarrolló el diagrama de estados, la tabla de estados y excitación, los mapas de Karnaugh y las funciones minimizadas.

### Carry Out en cascada

Cada contador genera una señal **Carry Out** al alcanzar su valor máximo, que funciona como pulso de reloj del contador de mayor jerarquía (unidades de segundos → decenas de segundos → unidades de minutos → ...).

### Decodificador de 7 segmentos (BCD)

Se reutiliza un único diseño de decodificador BCD a 7 segmentos para todos los displays. Las entradas que sobran en los contadores de menos de 4 bits se fijan en `0` mediante una constante `1` y una compuerta NOT.

### Reset a las 24:00

Una lógica combinacional con compuertas AND detecta la hora 24:00 (decenas = `10`, unidades = `0100`) y reinicia el reloj a 00:00:00. También cuenta con reset manual.

### Alarma

- Compara con compuertas **XOR + NOT + AND** las decenas y unidades de horas y minutos del reloj contra la hora programada.
- La salida permanece activa **durante un minuto completo** mientras ambas horas coincidan.
- La hora de la alarma se configura manualmente mediante el subcircuito `Alarma`, con visualización en displays de 7 segmentos.

---

## 🎨 Decisiones de diseño

- LEDs sincronizados al clock principal para simular los segundos y separar visualmente horas, minutos y segundos.
- Un único decodificador BCD reutilizado en todos los displays.
- Reutilización de los contadores existentes para las 24 horas, en lugar de crear un contador exclusivo.
- Displays con fondo negro para una apariencia más realista.
- Alarma activa durante un minuto para garantizar que sea perceptible.

---

## 📚 Archivos del repositorio

- `Informe_de_laboratorio_grupo_3.pdf`: Informe completo con diagramas de estados, tablas de verdad, funciones minimizadas y esquemáticos.
- `relojDigital.circ`: Archivo del reloj digital construido en Logisim Evolution.

---

## 🎥 Videos

- [Simulación del sistema completo](https://www.youtube.com/watch?v=C1QJbwZlDqg&list=PLrGN7l0QK2mvRItoYN1Lw7o2j2cik36NV)
- [Video explicativo del circuito](https://www.youtube.com/watch?v=EFTlMM4Th28&list=PLrGN7l0QK2mvDmdw9AFLpEggMzP-RArW)

---

## 📚 Requisitos técnicos

- [Logisim Evolution](https://github.com/logisim-evolution/logisim-evolution)

---

## ✍ Autores

- [@Joselito17821](https://github.com/Joselito17821) – Jose Manuel Londoño Castaño
- [@dipper319-dev](https://github.com/dipper319-dev) – Juan José Gómez Castaño

Universidad de Antioquia

Arquitectura de Computadores y Laboratorio

Fredy Alexander Rivera Vélez

Semestre 2025-1
