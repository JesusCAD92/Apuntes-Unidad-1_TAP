# 🚀 Tópicos Avanzados de Programación - Unidad 2: Componentes y Librerías
## 🏛️ Introducción: La Evolución hacia la Modularidad y el Encapsulamiento
Tras haber consolidado los fundamentos técnicos y la lógica algorítmica en la Unidad 1, donde exploramos las bases de la programación avanzada, esta segunda etapa representa un salto cualitativo fundamental en mi formación como Ingeniero en Sistemas Computacionales en el Instituto Tecnológico de Cuautla (ITC).

Mientras que en la etapa anterior el foco principal fue la resolución de problemas mediante lógica funcional y estructuras básicas, la Unidad 2: Componentes y Librerías nos sumerge de lleno en el paradigma del software modular. A través del ecosistema de Python y el framework Flet, he desarrollado competencias críticas para diseñar componentes visuales definidos por el usuario, gestionar paquetes externos y optimizar flujos de datos complejos mediante el uso estratégico de Data Classes.

Este repositorio no es solo una colección de archivos; es la documentación técnica de una transición hacia la ingeniería de software profesional, donde se demuestra que los sistemas modernos no son bloques monolíticos, sino conjuntos de módulos escalables, eficientes y altamente reutilizables.
## 📑 Tabla de Contenidos
* 2.1 & 2.2 Arquitectura del Software: Definiciones y Librerías Estándar

* 2.3 Desarrollo de Interfaz: Componentes definidos por el usuario

* 2.4 Integración Avanzada: Gestión de librerías externas y gráficas

* 🌟 Casos de Éxito: Proyectos Destacados y Despliegue

* 📂 Organización: Estructura del Repositorio
## 🏗️ 2.1 & 2.2 Arquitectura del Software: Fundamentos y Librerías
Para construir aplicaciones de alto nivel, es imperativo distinguir la jerarquía de los elementos que estructuran el código. En el entorno de Python/Flet, estos términos definen la robustez del sistema:

### 🧩 Componentes (Controls)
En las GUIs modernas, un componente es la unidad atómica de la interfaz. Es un objeto que encapsula tanto su representación visual como su lógica interna.

* Ejemplos: ft.ElevatedButton, ft.TextField, ft.Container.

* Identidad: Poseen atributos (propiedades) y disparadores de acción (eventos).
### 📦 Paquetes (Packages) y 📚 Librerías (Libraries)
Un Paquete es una carpeta física que organiza módulos mediante un archivo __init__.py, permitiendo jerarquizar el espacio de nombres. Por otro lado, una Librería es el conjunto conceptual de funcionalidades que importamos para no "reinventar la rueda".

### 🎲 El Poder de la Librería Estándar
Python se adhiere a la filosofía "Batteries Included". En esta unidad, hemos explotado módulos nativos para dar vida a los proyectos:

* random: Esencial para la aleatoriedad en el juego "Piedra, Papel o Tijera".

* io & base64: El corazón del manejo de archivos en memoria, permitiendo que las gráficas viajen del motor matemático a la pantalla sin tocar el disco duro.
## 🎨 2.3 Desarrollo de Interfaz: Componentes Personalizados
La verdadera potencia de Flet surge al heredar de clases existentes para crear controles propios. Esto permite definir "widgets" que contienen su propio diseño y comportamiento, facilitando el mantenimiento.

### 💻 Comparativa Técnica: El Camino hacia el Desacoplamiento
Analizamos la evolución de una TarjetaPerfil para entender por qué la arquitectura de datos define la calidad del software:
### ❌ Enfoque A: Parámetros Sueltos (Acoplamiento Fuerte)
Aquí, el componente depende directamente de variables individuales. Si el modelo de datos cambia, debemos modificar cada instancia del constructor manualmente.

---
```python
class TarjetaPerfil(ft.Container):
    def __init__(self, nombre: str, ocupacion: str):
        super().__init__(
            content=ft.Column([
                ft.Text(nombre, weight="bold", size=20),
                ft.Text(ocupacion, italic=True)
            ]),
            padding=10, border_radius=10, bgcolor=ft.colors.SURFACE_VARIANT
        )
```
### ✅ Enfoque B: Implementación con @dataclass (Desacoplamiento)
Definimos un Componente No Visual (UsuarioData) que gestiona la información. El componente visual solo recibe este objeto, permitiendo que la lógica de datos y la visual sean independientes.

---
```python
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
            content=ft.Row([
                ft.CircleAvatar(foreground_image_url=datos.avatar_url),
                ft.Column([
                    ft.Text(datos.nombre, size=16, weight="bold"),
                    ft.Text(datos.ocupacion, color=ft.colors.SECONDARY)
                ])
            ])
        )
```
Nota Técnica sobre super().__init__(): Esta llamada no es opcional; es el mecanismo que registra nuestra clase personalizada en el árbol de renderizado de la aplicación, permitiendo el uso de métodos reactivos como .update().
## 📈 2.4 Integración Avanzada: El "Puente" hacia Librerías Externas
Uno de los mayores retos en ingeniería es integrar herramientas que no hablan el mismo "idioma". En el Dashboard de Gráficas, conectamos el motor matemático de Matplotlib con la interfaz de Flet mediante el protocolo Base64.
### 🌉 Pipeline de Visualización de Datos
Para evitar la latencia de lectura/escritura en disco, implementamos un flujo de datos 100% en memoria RAM:
* Generación: Matplotlib crea la figura matemática.

* Buffer: io.BytesIO captura la imagen en un flujo de bytes.

* Codificación: Convertimos los bytes en una cadena Base64 (texto).

* Inyección: Flet interpreta ese texto como una imagen en tiempo real.

---
```python
# Ejemplo de implementación en Dashboard
class DashboardGraficas(ft.UserControl):
    def build(self):
        fig, ax = plt.subplots()
        ax.plot([1, 2, 3, 4], [10, 20, 25, 30], marker='o')
        
        buf = io.BytesIO()
        fig.savefig(buf, format="png")
        buf.seek(0)
        img_str = base64.b64encode(buf.read()).decode("utf-8")
        plt.close(fig)

        return ft.Image(src_base64=img_str, width=500)
```
## 🌟 Proyectos Destacados
### 🎮 Piedra, Papel o Tijera (Flet Edition)
Un caso de estudio sobre el manejo de Estados y Eventos. Este proyecto demuestra cómo una lógica simple se transforma en una experiencia de usuario fluida mediante page.update() y botones reactivos.
* Web: [Desplegado en Netlify](https://inquisitive-raindrop-94c0ea.netlify.app/) 🚀

* Multiplataforma: Capacidad de exportación a APK para dispositivos Android.
### 📊 Sistema de Reporteo Dinámico
Un dashboard que utiliza el pipeline Base64 para mostrar métricas de rendimiento, demostrando la versatilidad de Python para aplicaciones de análisis de datos.
## Codigos realizados en clase 
### Reutilizacion de componentes con @dataclass

---
```python
import flet as ft
from dataclasses import dataclass

# 1. Definimos la estructura de datos
@dataclass
class UsuarioData:
    nombre: str
    rol: str
    color_borde: str = ft.Colors.BLUE

# 2. Definición del componente personalizado mejorado
class TarjetaPerfil(ft.Container):
    def __init__(self, datos: UsuarioData):
        super().__init__()
        # Guardamos la referencia a los datos por si los necesitamos luego
        self.datos = datos
        
        self.content = ft.Column(
            controls=[
                ft.Text(self.datos.nombre, weight=ft.FontWeight.BOLD, size=20),
                ft.Text(self.datos.rol, italic=True),
                ft.ElevatedButton("Ver Perfil", on_click=self.saludar)
            ],
            tight=True
        )
        
        # Usamos los atributos de la Data Class para el estilo
        self.border = ft.border.all(2, self.datos.color_borde)
        self.padding = 10
        self.border_radius = 10
        self.width = 200

    def saludar(self, e):
        # Ahora el acceso a la información es más directo y limpio
        print(f"Interactuando con el perfil de: {self.datos.nombre}")

def main(page: ft.Page):
    page.title = "Unidad 2: Componentes con Data Classes"
    page.horizontal_alignment = ft.CrossAxisAlignment.CENTER

    # 3. Creamos instancias de nuestros datos
    info_usuario1 = UsuarioData(nombre="Ana García", rol="Desarrolladora Senior", color_borde=ft.Colors.GREEN)
    info_usuario2 = UsuarioData(nombre="Carlos Ruiz", rol="Arquitecto de Software")

    # 4. Pasamos los objetos completos a los componentes
    usuario1 = TarjetaPerfil(info_usuario1)
    usuario2 = TarjetaPerfil(info_usuario2)

    page.add(
        ft.Text("Lista de Usuarios (POO + DataClasses)", size=30, weight="bold"),
        ft.Row(
            controls=[usuario1, usuario2], 
            alignment=ft.MainAxisAlignment.CENTER
        )
    )

ft.app(target=main)
```
### Juego de piedra papel y tijeras con random 

---
```python
import flet as ft
import random

def main(page: ft.Page):
    page.title = "Piedra, Papel o Tijera"
    page.vertical_alignment = ft.MainAxisAlignment.CENTER
    page.horizontal_alignment = ft.CrossAxisAlignment.CENTER
    page.theme_mode = ft.ThemeMode.LIGHT

    opciones = ["Piedra", "Papel", "Tijera"]
    
    # Elementos de texto
    texto_resultado = ft.Text(value="¡Elige uno!", size=35, weight=ft.FontWeight.BOLD)
    texto_detalle = ft.Text(value="Prepárate para ganar", size=20, italic=True)

    def jugar(e):
        # Usamos e.control.data para obtener el valor de forma segura
        usuario = e.control.data
        maquina = random.choice(opciones)
        
        if usuario == maquina:
            res = "Empate 🤝"
        elif (usuario == "Piedra" and maquina == "Tijera") or \
             (usuario == "Papel" and maquina == "Piedra") or \
             (usuario == "Tijera" and maquina == "Papel"):
            res = "¡Ganaste! 🎉"
        else:
            res = "Perdiste 😢"
        
        texto_resultado.value = res
        texto_detalle.value = f"Tú: {usuario} | Máquina: {maquina}"
        page.update()

    # Botones con 'data' asignado explícitamente
# Botones con iconos estándar de Material Design
    btn_piedra = ft.FilledButton(
        "Piedra", 
 # Un icono que parece un puño/piedra
        on_click=jugar, 
        data="Piedra"
    )
    btn_papel = ft.FilledButton(
        "Papel", 
     # Icono de una hoja de papel
        on_click=jugar, 
        data="Papel"
    )
    btn_tijera = ft.FilledButton(
        "Tijera", 
 # Icono de tijeras (este sí es infalible)
        on_click=jugar, 
        data="Tijera"
    )

    page.add(
        ft.Column(
            controls=[
                texto_resultado,
                texto_detalle,
                ft.Row(
                    controls=[btn_piedra, btn_papel, btn_tijera],
                    alignment=ft.MainAxisAlignment.CENTER
                )
            ],
            horizontal_alignment=ft.CrossAxisAlignment.CENTER,
            spacing=40
        )
    )

if __name__ == "__main__":
    ft.app(target=main)
```
### Graficas con libreria matplotlib
---
```python
import matplotlib.pyplot as plt
import flet as ft
import io
import base64

# --- FUNCIÓN PARA CONVERTIR GRÁFICA A IMAGEN (Standard 0.82.0) ---
def figura_a_base64(fig):
    buf = io.BytesIO()
    fig.savefig(buf, format='png', bbox_inches='tight') # bbox_inches ayuda a que no se corten los bordes
    buf.seek(0)
    # Formateamos el string para que Flet lo reconozca como imagen base64
    img_str = base64.b64encode(buf.read()).decode('utf-8')
    plt.close(fig) # Es buena práctica cerrar la figura para liberar memoria
    return f"data:image/png;base64,{img_str}"

# --- FUNCIONES DE GRÁFICO (Matplotlib) ---
def generar_grafica_barras():
    fig, ax = plt.subplots(figsize=(4, 3))
    ax.bar(["A", "B", "C", "D", "E"], [23, 45, 12, 54, 32], color="skyblue")
    ax.set_title("Ventas por Producto", fontsize=10, weight='bold')
    plt.tight_layout()
    return figura_a_base64(fig)

def generar_grafica_lineas():
    fig, ax = plt.subplots(figsize=(4, 3))
    ax.plot(["Ene", "Feb", "Mar", "Abr", "May"], [10, 25, 18, 40, 35], color="orange", marker='o')
    ax.set_title("Tendencia de Rendimiento", fontsize=10, weight='bold')
    plt.tight_layout()
    return figura_a_base64(fig)

def generar_grafica_pastel():
    fig, ax = plt.subplots(figsize=(4, 3))
    etiquetas = ["Norte", "Sur", "Este", "Oeste"]
    valores = [25, 35, 20, 20]
    colores = ['#ff9999','#66b3ff','#99ff99','#ffcc99']
    # autopct muestra el porcentaje en cada rebanada
    ax.pie(valores, labels=etiquetas, autopct='%1.1f%%', startangle=90, colors=colores)
    ax.set_title("Distribución por Región", fontsize=10, weight='bold')
    plt.tight_layout()
    return figura_a_base64(fig)

def generar_grafica_dispersion():
    fig, ax = plt.subplots(figsize=(4, 3))
    # Datos de ejemplo (ej. Inversión en publicidad vs Ventas)
    x = [5, 10, 15, 20, 25, 30, 35]
    y = [12, 18, 24, 22, 35, 38, 45]
    ax.scatter(x, y, color="purple", alpha=0.7, edgecolors="black")
    ax.set_title("Correlación de Variables", fontsize=10, weight='bold')
    plt.tight_layout()
    return figura_a_base64(fig)

# --- APLICACIÓN PRINCIPAL ---
def main(page: ft.Page):
    page.title = "Dashboard Flet - Final"
    page.theme_mode = "light"
    page.horizontal_alignment = "center"
    page.scroll = "auto" # Permitir scroll si las gráficas son grandes
    
    # IMPORTANTE: En Flet 0.82.0 usamos 'src' con el prefijo data:image
    img_barras = ft.Image(src=generar_grafica_barras(), width=400, height=300)
    img_lineas = ft.Image(src=generar_grafica_lineas(), width=400, height=300)
    img_pastel = ft.Image(src=generar_grafica_pastel(), width=400, height=300)
    img_dispersion = ft.Image(src=generar_grafica_dispersion(), width=400, height=300)

    # Estilo reutilizable para los contenedores de las gráficas
  # Estilo reutilizable para los contenedores de las gráficas
    def crear_tarjeta(contenido_imagen):
        return ft.Container(
            content=contenido_imagen, 
            border=ft.border.all(1, "#cccccc"), 
            border_radius=10,
            padding=10,
            bgcolor="white"  # <-- Cambio aquí: usamos un string en lugar de ft.colors.WHITE
        )

    page.add(
        ft.Text("Dashboard de Visualización (Versión 0.82.0)", size=24, weight="bold"),
        ft.Divider(),
        # Usamos un Row con wrap=True para que las gráficas se acomoden como en un grid
        ft.Row(
            controls=[
                crear_tarjeta(img_barras),
                crear_tarjeta(img_lineas),
                crear_tarjeta(img_pastel),
                crear_tarjeta(img_dispersion)
            ],
            alignment=ft.MainAxisAlignment.CENTER,
            wrap=True, # Esto permite que si la pantalla es pequeña, pasen a la siguiente línea
            spacing=20,
            run_spacing=20
        )
    )

if __name__ == "__main__":
    ft.app(target=main)
```
## 📚 Referencias Bibliográficas (Formato APA)
### 🐍 Documentación Oficial y Estándares de Python
* Python Software Foundation. (2026). The Python Standard Library: Data Types, Modules, and Built-in Functions. Recuperado de https://docs.python.org/3/library/

* Python Software Foundation. (2018). PEP 557 – Data Classes. Recuperado de https://peps.python.org/pep-0557/

* Van Rossum, G., Warsaw, B., & Coghlan, N. (2001). PEP 8 – Style Guide for Python Code. Recuperado de https://peps.python.org/pep-0008/
### 🖼️ Frameworks y Visualización (Flet & Matplotlib)
* Flet Team. (2026). Flet: Build Flutter apps in Python. Controls and Architecture Documentation. Recuperado de https://flet.dev/docs/

* Matplotlib Development Team. (2026). Matplotlib: Visualization with Python. API Reference and Tutorials. Recuperado de https://matplotlib.org/stable/contents.html
### 📖 Libros de Ingeniería de Software y Programación
* Deitel, P., & Deitel, H. (2020). Python para Programadores (1.ª ed.). Pearson Educación.

* Pressman, R. S., & Maxim, B. R. (2021). Ingeniería de Software: Un enfoque profesional (9.ª ed.). McGraw-Hill Education.

* Sommerville, I. (2011). Ingeniería de Software (9.ª ed.). Pearson Educación.
