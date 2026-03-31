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
## 2.2 Uso de librerías proporcionadas por el lenguaje
Python destaca por su filosofía "Batteries Included", lo que significa que incluye una Librería Estándar muy robusta. En los proyectos de esta unidad (como el juego y el dashboard), optimizamos el desarrollo utilizando los siguientes módulos nativos:
### 🎲 Módulo random
Fundamental para la lógica de juegos. En nuestro proyecto de Piedra, Papel o Tijera, lo utilizamos para que la computadora seleccione una opción de forma aleatoria.

```python
import random
opciones = ["Piedra", "Papel", "Tijera"]
computadora = random.choice(opciones)
```
## 2.3 Creación de componentes (visuales y no visuales) definidos por el usuario
En el desarrollo de interfaces avanzadas, la modularidad es clave. Flet permite crear componentes personalizados heredando de clases existentes, lo que nos permite definir nuestros propios "controles" con diseño y comportamiento específicos.
### 🎨 Componentes Visuales Personalizados
Un componente visual personalizado es una clase que extiende las funcionalidades de un control base (comúnmente ft.Container o ft.UserControl). Al heredar de ft.Container, ganamos acceso a propiedades de diseño como bordes, sombras, alineación y colores, permitiéndonos crear elementos como tarjetas de perfil, botones estilizados o dashboards.
### 💻 Comparativa de Implementación: Acoplamiento vs. Desacoplamiento
Para ilustrar la evolución del código, analizamos dos formas de construir una TarjetaPerfil.

### Opción A: Parámetros Simples (Acoplamiento Fuerte)
En este enfoque, la clase recibe cada dato de forma individual. Si el perfil del usuario crece (añadiendo redes sociales, ID, etc.), el constructor de la clase se vuelve difícil de mantener.

---
```python
import flet as ft

class TarjetaPerfil(ft.Container):
    def __init__(self, nombre: str, ocupacion: str):
        # super().__init__() inicializa las propiedades de la clase padre (Container)
        super().__init__(
            content=ft.Column([
                ft.Text(nombre, weight="bold", size=20),
                ft.Text(ocupacion, italic=True)
            ]),
            padding=10,
            border_radius=10,
            bgcolor=ft.colors.SURFACE_VARIANT
        )
```
### Opción B: Uso de @dataclass (Mejor Práctica y Desacoplamiento)
Aquí definimos un componente no visual (UsuarioData) que actúa como un contenedor de datos puro. La TarjetaPerfil ahora solo se preocupa por cómo mostrar esos datos, no por cuántos son.

---
```python
from dataclasses import dataclass
import flet as ft

# Componente NO VISUAL: Manejo de información puro
@dataclass
class UsuarioData:
    nombre: str
    ocupacion: str
    avatar_url: str = None

class TarjetaPerfilPro(ft.Container):
    def __init__(self, datos: UsuarioData):
        super().__init__(
            padding=20,
            border=ft.border.all(1, ft.colors.OUTLINE),
            border_radius=15,
            content=ft.Row([
                ft.CircleAvatar(foreground_image_url=datos.avatar_url),
                ft.Column([
                    ft.Text(datos.nombre, size=16, weight="bold"),
                    ft.Text(datos.ocupacion, color=ft.colors.SECONDARY)
                ])
            ])
        )
```
### ¿Por qué es mejor la Opción B?
1) Desacoplamiento: La interfaz gráfica no necesita saber cómo se obtienen los datos. Si mañana los datos vienen de una base de datos SQL o una API, solo actualizamos el objeto UsuarioData.

2) Mantenibilidad: El constructor de la tarjeta es limpio. No importa si el usuario tiene 2 o 20 atributos; la firma de la función __init__(self, datos: UsuarioData) no cambia.

3) Legibilidad: Al usar datos.nombre, el código es semánticamente más claro que manejar múltiples variables sueltas.

### 🛠️ Detalles Técnicos de la Herencia
* super().__init__(): Es obligatorio invocarlo. Permite que nuestra clase personalizada se registre correctamente dentro del árbol de componentes de Flet, heredando capacidades como el método .update() y la renderización en el navegador/app.

* Personalización de Atributos: Al definir el contenido dentro del super(), estamos pre-configurando el estado inicial del control. Esto permite que cualquier instancia de TarjetaPerfilPro mantenga la misma identidad visual en toda la aplicación.
## 2.4 Creación y uso de paquetes/librerías definidas por el usuario
En proyectos de ingeniería, la visualización de datos es fundamental. Sin embargo, frameworks de UI como Flet no renderizan directamente objetos complejos de librerías científicas como Matplotlib. Para lograr esta integración, debemos crear un "puente" lógico que transforme datos matemáticos en recursos visuales procesables.
### 🌉 Integración de Librerías Externas: El "Puente" Base64
Dado que Flet se basa en protocolos web/Flutter, la forma más eficiente de mostrar una gráfica de Matplotlib es convirtiéndola en una cadena de texto Base64. Este método permite que la gráfica viva en la memoria RAM del sistema sin necesidad de escribir archivos temporales en el disco duro, mejorando el rendimiento y la limpieza del proyecto.
#### El Proceso Lógico (Pipeline de Renderizado)
1) Generación: Se crea la figura (plt.figure) y los ejes (ax) con Matplotlib.

2) Buffer de Memoria: Usamos la librería nativa io.BytesIO para guardar la imagen en un flujo de bytes en lugar de un archivo .png.

3) Codificación: Transformamos esos bytes a una cadena Base64.

4) Inyección: Se asigna la cadena resultante a la propiedad src_base64 de un componente ft.Image.
### 📊 Ejemplo Práctico: Dashboard de Gráficas Dinámicas
El siguiente código encapsula la lógica de una librería externa en un componente de Flet, demostrando cómo modularizar la visualización de datos.

---
```python
import flet as ft
import matplotlib.pyplot as plt
import io
import base64

class DashboardGraficas(ft.UserControl):
    def build(self):
        # 1. Crear la figura de Matplotlib
        fig, ax = plt.subplots()
        ax.plot([1, 2, 3, 4], [10, 20, 25, 30], marker='o', color='blue')
        ax.set_title("Rendimiento del Sistema")
        ax.set_xlabel("Tiempo (s)")
        ax.set_ylabel("Valor")

        # 2. Guardar en un buffer de memoria (io.BytesIO)
        buf = io.BytesIO()
        fig.savefig(buf, format="png")
        buf.seek(0)

        # 3. Codificar a Base64
        img_str = base64.b64encode(buf.read()).decode("utf-8")
        
        # Limpiar la memoria de Matplotlib para evitar fugas (Memory Leaks)
        plt.close(fig)

        # 4. Retornar el componente visual de Flet
        return ft.Column([
            ft.Text("Visualización de Datos en Tiempo Real", size=20, weight="bold"),
            ft.Image(
                src_base64=img_str,
                width=500,
                height=400,
                fit=ft.ImageFit.CONTAIN,
                tooltip="Gráfica generada con Matplotlib"
            )
        ])

# Uso en la aplicación principal
def main(page: ft.Page):
    page.title = "TAP - Unidad 2: Dashboard"
    page.add(DashboardGraficas())

if __name__ == "__main__":
    ft.app(target=main)
```
