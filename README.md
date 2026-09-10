# Arduino Security Project

## Proyecto Final — Arquitectura del Computador

Este repositorio contiene el proyecto base para el desarrollo del **Proyecto Final del curso de Arquitectura del Computador**.

El objetivo es construir progresivamente un **Mini Sistema Computacional de Control y Seguridad utilizando Arduino Uno**, integrando los conceptos estudiados durante el curso: entrada y salida de datos, memoria, procesamiento, buses, periféricos, sensores y actuadores.

El proyecto será desarrollado de forma incremental durante los laboratorios.

---

## Objetivo del proyecto

Construir un sistema de control de acceso capaz de identificar a un usuario, solicitar autenticación y controlar físicamente el acceso mediante diferentes periféricos conectados al Arduino.

El sistema final integrará componentes como:

* Arduino Uno
* RFID RC522
* Teclado matricial 4×4
* Pantalla LCD 16×2
* Servo motor
* LED y buzzer
* Registro de desplazamiento 74HC595

Durante el desarrollo podrán incorporarse otros sensores o dispositivos dependiendo de los requerimientos de cada etapa.

---

## Funcionamiento general

El sistema deberá implementar progresivamente un flujo similar al siguiente:

```text
Usuario
   │
   ▼
Tarjeta RFID
   │
   ▼
Identificación
   │
   ▼
Ingreso de PIN
   │
   ▼
Validación
   │
   ├──── Acceso incorrecto
   │
   ▼
Acceso autorizado
   │
   ▼
Servo / mecanismo de apertura
```

Cada laboratorio agregará nuevas capacidades al sistema.

---

## Estructura del repositorio

```text
arduino-security-project/
│
├── base/
│   └── base.ino
│
├── diagnostics/
│   └── diagnostics.ino
│
├── 3d-printing/
│   └── archivos STL
│
├── pinout.pdf
│
└── README.md
```

### `base/`

Contiene el programa base del proyecto.

Este será el punto de partida para integrar progresivamente las funcionalidades desarrolladas durante los laboratorios.

### `diagnostics/`

Contiene código destinado a realizar pruebas y diagnósticos de los componentes del sistema.

Puede utilizarse para comprobar conexiones y funcionamiento de los dispositivos antes de integrarlos al programa principal.

### `3d-printing/`

Contiene los modelos STL utilizados para construir la estructura física del proyecto.

Incluye piezas para la carcasa, puerta, soportes y mecanismo asociado al servo.

### `pinout.pdf`

Diagrama de referencia para las conexiones utilizadas en el proyecto.

---

# Forma de trabajo con Git

El proyecto utilizará un flujo de trabajo simplificado inspirado en **GitFlow**.

La rama:

```text
main
```

representará siempre la versión estable del proyecto.

**No se debe desarrollar directamente sobre `main`.**

Para cada laboratorio se deberá crear una nueva rama utilizando el prefijo:

```text
feature/
```

Por ejemplo:

```text
feature/rfid
feature/keypad
feature/eeprom
feature/servo
feature/lcd
```

---

## Antes de iniciar cada laboratorio

Primero asegurarse de estar trabajando sobre la versión más reciente del proyecto:

```bash
git checkout main
git pull
```

Crear posteriormente la rama correspondiente al laboratorio:

```bash
git checkout -b feature/nombre-del-laboratorio
```

Por ejemplo:

```bash
git checkout -b feature/rfid
```

A partir de este momento todo el trabajo del laboratorio deberá realizarse dentro de esta rama.

---

## Guardar avances

No es necesario esperar hasta terminar el laboratorio para realizar un commit.

Es recomendable guardar avances importantes:

```bash
git add .
git commit -m "Implementa lectura inicial del RFID"
```

Continuar trabajando y realizar nuevos commits cuando sea necesario.

Por ejemplo:

```bash
git commit -m "Agrega validacion del UID"
```

Los mensajes de commit deben describir brevemente el cambio realizado.

Evitar mensajes como:

```text
cambios
prueba
final
ahora si
version buena
```

---

## Subir la rama a GitHub

Cuando exista un avance que se desee respaldar:

```bash
git push -u origin feature/rfid
```

Después del primer `push`, normalmente será suficiente utilizar:

```bash
git push
```

---

# Integrar el laboratorio al proyecto

Cuando el laboratorio funcione correctamente y el equipo considere que está listo, deberá integrarse nuevamente a `main`.

Primero regresar a:

```bash
git checkout main
```

Actualizar:

```bash
git pull
```

Luego integrar la rama:

```bash
git merge feature/rfid
```

Finalmente subir la nueva versión:

```bash
git push
```

La rama `main` contiene ahora la nueva funcionalidad.

---

# ¿Qué pasa si algo sale mal?

Una de las ventajas de utilizar Git es poder regresar a una versión anterior.

Para revisar el historial:

```bash
git log --oneline
```

Se observará algo similar a:

```text
a82c710 Agrega validacion RFID
f531a20 Implementa lectura RFID
81bd902 Proyecto funcionando
```

Para regresar temporalmente a una versión anterior:

```bash
git checkout ID_DEL_COMMIT
```

Por ejemplo:

```bash
git checkout 81bd902
```

Esto permite revisar cómo estaba el proyecto en ese momento.

Para regresar nuevamente a la versión actual:

```bash
git checkout main
```

**No borrar commits ni utilizar comandos destructivos sin comprender previamente sus consecuencias.**

---

# Regla principal del proyecto

Cada nueva funcionalidad debe desarrollarse en su propia rama.

```text
main
 │
 ├── feature/rfid
 │
 ├── feature/keypad
 │
 ├── feature/eeprom
 │
 ├── feature/servo
 │
 └── feature/lcd
```

Cuando una funcionalidad esté terminada y probada:

```text
feature
   │
   ▼
pruebas
   │
   ▼
merge
   │
   ▼
main
```

De esta manera `main` deberá representar siempre la versión estable del proyecto.

---

# Uso de Inteligencia Artificial

Se permite utilizar herramientas de Inteligencia Artificial como apoyo durante el desarrollo del proyecto.

Sin embargo:

**Todo código incorporado al proyecto es responsabilidad del equipo.**

Los integrantes deberán ser capaces de:

* Explicar cómo funciona el código.
* Identificar las entradas y salidas utilizadas.
* Explicar las librerías utilizadas.
* Comprender las principales variables y funciones.
* Explicar cómo interactúa el programa con el hardware.
* Diagnosticar problemas cuando el sistema no funcione.
* Justificar las decisiones tomadas durante la implementación.

El hecho de que un programa compile o haya sido generado por una herramienta de IA **no garantiza que sea correcto**.

Durante los laboratorios o evaluación del proyecto podrá solicitarse a cualquier integrante explicar o modificar una parte del código.

---

# Recomendaciones

Antes de integrar una funcionalidad a `main`:

1. Verificar que el programa compile correctamente.
2. Probar físicamente el componente.
3. Verificar que las funcionalidades anteriores continúen funcionando.
4. Revisar el código antes de hacer el merge.
5. Realizar un commit descriptivo.
6. Integrar la rama únicamente cuando el equipo considere estable la funcionalidad.

---

## Resultado esperado

Al finalizar el proyecto, el repositorio deberá mostrar no solamente el programa terminado, sino también **la evolución del sistema durante el semestre**.

El historial de Git permitirá observar:

```text
Sistema base
     ↓
RFID
     ↓
Teclado
     ↓
EEPROM
     ↓
LCD
     ↓
Servo
     ↓
Integración
     ↓
Sistema final
```

El objetivo no es únicamente construir un sistema que funcione.

El objetivo es aprender a **diseñar, desarrollar, probar, integrar y mantener un sistema computacional utilizando prácticas similares a las utilizadas en proyectos reales de ingeniería**.
