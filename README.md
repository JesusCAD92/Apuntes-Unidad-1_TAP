# 🚀 Tópicos Avanzados de Programación - Unidad 2
## Unidad 2: La Evolución hacia la Modularidad

Tras haber consolidado los fundamentos de la programación en la Unidad 1, donde exploramos los conceptos base de la materia Tópicos Avanzados de Programación, esta segunda unidad representa un salto cualitativo en mi formación como Ingeniero en Sistemas Computacionales en el Instituto Tecnológico de Cuautla (ITC).

Mientras que en la etapa anterior nos enfocamos en la lógica funcional, la Unidad 2: Componentes y Librerías nos sumerge en el paradigma de la reutilización y el encapsulamiento. A través del uso de Python y el framework Flet, he desarrollado la capacidad de diseñar componentes visuales definidos por el usuario, gestionar paquetes externos y optimizar el flujo de datos mediante el uso de Data Classes.

En este repositorio se documenta no solo la teoría, sino la implementación práctica de estos conceptos en proyectos reales: desde la creación de interfaces dinámicas con Matplotlib hasta el despliegue multiplataforma de aplicaciones (Web y APK), demostrando que la ingeniería de software moderna se basa en la construcción de sistemas modulares, escalables y eficientes.
## Tabla de Contenidos
* 2.1 Creación y uso de librerías del programador

* 2.2 Uso de librerías de interfaz gráfica

* 2.3 Jerarquía de componentes y controles

* 2.4 Gestión de eventos y propiedades

* 🌟 Proyectos Destacados

* 📂 Estructura del Repositorio
## Proyectos Destacados
🎮 Piedra, Papel o Tijera (Flet Edition)

Una implementación interactiva del clásico juego, enfocada en la gestión de estados y animaciones.

Web: [Disponible en Netlify](https://inquisitive-raindrop-94c0ea.netlify.app/) 🚀

### 📊 Dashboard de Gráficas
Módulo de visualización que integra Matplotlib dentro del ciclo de vida de una app de Flet, permitiendo la generación de reportes visuales dinámicos.

## 📂 Estructura del Repositorio

```mermaid
Para mantener el orden que manejamos en la Unidad 1, utilizaremos la siguiente jerarquía:
Unidad-2_TAP/
├── 📁 assets/                # Imágenes, iconos y fuentes
│   └── 📁 img/               # Capturas de pantalla y recursos visuales
├── 📁 docs/                  # Apuntes teóricos y diagramas de clase
├── 📁 src/                   # Código fuente organizado por subtema
│   ├── 📝 2.1_librerias/     # Módulos .py personalizados
│   ├── 📝 2.2_gui_basics/    # Primeros pasos con Flet
│   ├── 📝 2.3_componentes/   # Layouts, Rows y Columns
│   └── 📝 2.4_eventos/       # Handlers y lógica de botones
├── 📁 proyectos/             # Aplicaciones completas y funcionales
│   ├── 📁 rps_game/          # Juego Piedra, Papel o Tijera
│   └── 📁 stats_dashboard/   # Dashboard de gráficas
├── 📄 .gitignore             # Archivos excluidos (venv, __pycache__)
├── 📄 requirements.txt       # Dependencias (Flet, Matplotlib, etc.)
└── 📄 README.md              # Documentación principal
```
## 2.1 Definición conceptual de componentes, paquetes y librerías
En el desarrollo de software moderno, y específicamente trabajando con frameworks como Flet, es vital distinguir la jerarquía de los elementos que componen nuestro código. Aunque a menudo se usan como sinónimos, tienen propósitos distintos:
### 🧩 Componentes (Controls)
En el contexto de interfaces gráficas (GUI) con Flet, un componente (o Control) es la unidad básica de la interfaz. Es un objeto encapsulado que tiene una representación visual y un comportamiento definido.
* Ejemplos: ft.ElevatedButton, ft.TextField, ft.Container.

* Características: Poseen propiedades (color, tamaño) y métodos (manejo de eventos como on_click).
### 📦 Paquetes (Packages)
Un paquete es una colección de módulos de Python agrupados bajo un mismo directorio que contiene un archivo especial __init__.py. Es una forma de estructurar jerárquicamente el espacio de nombres (namespaces).
* Ejemplo: El paquete flet contiene submódulos como flet.canvas, flet.buttons, etc.

* Propósito: Organizar archivos .py para que puedan ser importados de forma lógica (ej. import paquete.modulo).
### 📚 Librerías (Libraries)
Una librería es un concepto más amplio. Se refiere a una colección de recursos, paquetes y módulos pre-escritos que los desarrolladores utilizan para realizar tareas comunes sin "reinventar la rueda".
* Diferencia clave: Mientras que un paquete es una estructura de archivos, la librería es el conjunto de funcionalidades que ofrece.

* Contexto Flet: Flet es, en esencia, una librería que nos permite construir apps multiplataforma usando Python.
