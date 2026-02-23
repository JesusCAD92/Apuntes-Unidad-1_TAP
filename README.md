# Apuntes-Unidad-1_TAP
# Introducción
En esta unidad nos enfocamos en el desarrollo de Interfaces Gráficas de Usuario (GUI), que básicamente son el front-end que permite que cualquier persona interactúe con nuestra lógica de programación sin tener que usar una terminal o consola de comandos. Como futuros ingenieros, entendemos que una aplicación funcional no es suficiente si el usuario no puede navegar en ella de forma intuitiva; por eso, las GUIs son clave para abstraer la complejidad del software mediante componentes visuales como botones, contenedores y menús.

A lo largo de la unidad, exploramos el flujo de trabajo para construir aplicaciones de escritorio y web utilizando Flet, un framework basado en Flutter que nos permite trabajar todo el entorno gráfico directamente con Python. El aprendizaje se dividió en entender cómo estructurar una ventana desde cero, organizar elementos mediante layouts (como columnas, filas y contenedores) para que la interfaz sea responsiva, y lo más importante: la programación dirigida por eventos.

También profundizamos en el manejo de controles gráficos, personalizando sus propiedades y aplicando lógica de validación de datos (como el uso de Regex). El objetivo final fue pasar de scripts planos a aplicaciones interactivas reales, como calculadoras, formularios de registro y sistemas de chat multiusuario, aplicando buenas prácticas de diseño y usabilidad.<br>
## 1.1 Creación de interfaz gráfica para usuarios (GUI)
Desde una perspectiva de ingeniería, la GUI es la capa de abstracción que permite la interacción humano-computadora (HCI) sin que el usuario final tenga que manipular directamente la lógica del backend. Es el puente que traduce acciones físicas (clics, pulsaciones de teclas) en instrucciones que el sistema puede procesar.

Cada vez que interactuamos con un software, lo hacemos a través de una arquitectura visual compuesta por elementos manipulables: botones, campos de texto, menús y contenedores. Sin embargo, una buena interfaz no solo se trata de "cómo se ve", sino de la retroalimentación que el sistema ofrece. Si al presionar un botón no hay un cambio de estado o un mensaje, el flujo de usuario se rompe. Como desarrolladores, nuestro trabajo es garantizar que la UI sea intuitiva, reduciendo la curva de aprendizaje y optimizando la eficiencia operativa del software.
### Implementación con Flet y Python
En Flet, adoptamos un enfoque de desarrollo donde la interfaz se define mediante código (UI as Code). Esto es una ventaja enorme en sistemas, ya que no dependemos de archivos externos de diseño como HTML o CSS; el framework utiliza el motor de Flutter para renderizar componentes de Material Design directamente desde Python.

La unidad básica de cualquier app en Flet es la page (equivalente al Stage en JavaFX o al Form en .NET). Sobre este objeto agregamos los controles que darán vida a la aplicación.

#### Práctica 1: Inicialización de componentes básicos
En nuestro primer acercamiento, aprendimos a instanciar la página y renderizar controles elementales, comprendiendo que cada objeto tiene propiedades (como disabled) que alteran su comportamiento en el runtime.<br>
```python
import flet as ft

def main(page: ft.Page):
    # Configuración del contenedor raíz y renderizado de controles iniciales
    page.add(
        ft.Button(content="Enabled button"), # Control activo
        ft.Button(content="Disabled button", disabled=True), # Control con estado inactivo
        ft.Checkbox(label="Check de confirmación") # Componente de selección booleana
    )

if __name__ == "__main__":
    ft.run(main)
```
Aprendí que page.add() es el método que envía nuestros objetos al árbol de renderizado de la aplicación.<br>
### Tema 2: Arquitectura de Layouts (Distribución de Elementos)
En el diseño de software, el Layout es el motor de posicionamiento que decide cómo se organizan los componentes en el espacio bidimensional de la ventana. No basta con agregar botones; necesitamos una estructura lógica para que la interfaz sea escalable y visualmente coherente.

#### 1. GridLayout (Distribución en Rejilla)
Este sistema organiza los elementos en una matriz de filas y columnas. Es ideal para aplicaciones que requieren simetría perfecta, como nuestra práctica de la calculadora o teclados numéricos. En Flet, implementamos esto mediante el control GridView, que permite que los elementos se ajusten automáticamente según el espacio disponible, similar al comportamiento de un GridLayout en entornos de desarrollo tradicionales.

#### Ejemplo de GridView:
```python
grid = ft.GridView(
    expand=True,
    max_extent=120, # Define el ancho máximo de cada celda
    spacing=10,
    controls=[ft.ElevatedButton(f"Item {i}") for i in range(1, 10)]
)
```
#### 2. Flexbox (Contenedores Flexibles)
Es el estándar moderno para interfaces responsivas. En Flet, utilizamos Row (eje horizontal) y Column (eje vertical). Estos contenedores permiten que los elementos se alineen, se centren o se expandan para llenar el espacio sobrante. Es la base para construir formularios o barras de herramientas.

  1) Column: Organiza los elementos de arriba hacia abajo (flujo vertical). Ideal para apilar etiquetas y campos de entrada.

2)  Row: Organiza de izquierda a derecha (flujo horizontal). Perfecto para agrupar botones de acción (ej. "Aceptar" y "Cancelar").<br>
#### 3. Container y Grid Web
El Container es quizás el componente más versátil. Funciona como un div en desarrollo web, permitiéndonos aplicar estilos específicos como bordes, sombras, rellenos (padding) y colores de fondo. Al combinar Row, Column y Container, podemos replicar diseños complejos de tipo "Web Grid", dividiendo la pantalla en secciones como encabezados, barras laterales (sidebars) y áreas de contenido principal.

#### Análisis técnico:
Entendí que dominar los layouts es la diferencia entre una aplicación que se ve "amontonada" y una aplicación profesional. El secreto está en saber cuándo usar una columna para el cuerpo de un formulario y cuándo usar una fila para distribuir botones lateralmente.<br>
## 1.2 Tipos de Eventos
Al trabajar con interfaces gráficas, el flujo de ejecución cambia radicalmente respecto a los programas de consola secuenciales. Aquí, la aplicación entra en un Event Loop (bucle de eventos); no se ejecuta todo de corrido, sino que el software queda en un estado de "escucha" activa.

Un evento es esencialmente una señal que el sistema operativo o el framework detecta cuando el usuario interactúa con la UI. En Flet, estos eventos se mapean directamente a funciones de Python.
#### Categorías de eventos que analizamos:
* Eventos de Mouse: Son los más comunes. Involucran el on_click (clic), pero también existen eventos de desplazamiento o cuando el cursor entra en un área.
* Eventos de Teclado: Se capturan a través de page.on_keyboard_event. Son vitales para juegos o accesibilidad, permitiendo detectar qué tecla física fue presionada (e.key).
* Eventos de Cambio (on_change): Cruciales para la validación de formularios. Se disparan cada vez que el estado de un control cambia, como escribir una sola letra en un TextField.
* Eventos de Ventana: Controlan el ciclo de vida de la aplicación, como el redimensionamiento o el cierre de la sesión.
## 1.3 Manejo de Eventos (Event Handling)
El manejo de eventos es la implementación de la respuesta lógica a la señal detectada. Para esto usamos Event Handlers (Manejadores), que no son más que funciones que se ejecutan automáticamente cuando ocurre el evento.

En Flet, el objeto e (Event Control) es nuestra herramienta principal. Este objeto viaja desde el componente hasta nuestra función y contiene metadatos críticos:

* e.control: Nos dice qué objeto exacto disparó el evento.

* e.data: Información adicional (como el valor actual o coordenadas).
#### Práctica Integrada: Calculadora Modular
En esta práctica, aplicamos el manejo de eventos de forma masiva. En lugar de crear una función para cada botón, creamos un manejador genérico boton_click que decide qué hacer basándose en la propiedad data de cada control.
```python
import flet as ft

def main(page: ft.Page):
    page.title = "Calculadora Estática - TAP"
    page.window_width, page.window_height = 280, 450
    page.padding = 15
    
    # El Display es el componente que será modificado por los eventos
    display = ft.Text(value="0", size=28, weight=ft.FontWeight.BOLD)

    # EVENT HANDLER: Lógica centralizada para todos los botones
    def boton_click(e):
        valor = e.control.data  # Extraemos qué botón se presionó

        if valor == "C":
            display.value = "0"
        elif valor == "=":
            try:
                # Aquí podríamos usar eval() para procesar la cadena
                display.value = str(eval(display.value))
            except:
                display.value = "Error"
        else:
            if display.value == "0" or display.value == "Error":
                display.value = valor
            else:
                display.value += valor

        page.update() # IMPORTANTE: Refresca el DOM de la aplicación

    # Función auxiliar para instanciar botones con sus respectivos Event Listeners
    def crear_boton(texto, color="blue"):
        return ft.Container(
            content=ft.Text(texto, size=20, color=ft.Colors.WHITE),
            bgcolor=color,
            expand=1,
            height=55,
            alignment=ft.alignment.center,
            on_click=boton_click, # Asignamos el manejador
            data=texto           # Pasamos el valor como metadato
        )

    # Construcción de la UI usando Layouts (Rows y Columns)
    page.add(
        ft.Column(
            controls=[
                ft.Text("Display:"),
                ft.Container(content=display, bgcolor=ft.Colors.BLACK12, padding=10),
                ft.Divider(),
                ft.Column([
                    ft.Row([crear_boton("7"), crear_boton("8"), crear_boton("9")]),
                    ft.Row([crear_boton("4"), crear_boton("5"), crear_boton("6")]),
                    ft.Row([crear_boton("1"), crear_boton("2"), crear_boton("3")]),
                    ft.Row([crear_boton("0"), crear_boton("C", "red"), crear_boton("=", "orange")]),
                ], spacing=5),
                ft.Row([
                    crear_boton("+", "green"), crear_boton("-", "green"),
                    crear_boton("*", "green"), crear_boton("/", "green"),
                ], spacing=5)
            ]
        )
    )

ft.app(target=main)
```
## 1.4 Manejo de componentes gráficos de control
En ingeniería de software, el manejo de componentes (o widgets) se refiere a la manipulación directa de los objetos que integran la interfaz de usuario. No basta con renderizarlos en pantalla; es necesario controlar su comportamiento, modificar sus estados en tiempo de ejecución y validar la integridad de los datos que el usuario ingresa. Aquí es donde la interfaz deja de ser un prototipo estático y se convierte en un sistema funcional.
#### Componentes fundamentales en Flet (análisis técnico):
Para construir nuestras aplicaciones, identificamos y utilizamos los siguientes componentes, cada uno con una finalidad específica dentro del sistema:<br>
Controles de Salida (Output):

* Text: Se utiliza para renderizar cadenas de caracteres en la interfaz. Es el componente básico para etiquetas (Labels) y mensajes informativos.

* CircleAvatar: Un control visual que permite mostrar iniciales o imágenes de perfil, mejorando la experiencia de usuario (UX) en aplicaciones sociales.

Controles de Entrada (Input):

* TextField: Es el componente más versátil para la captura de datos. Permite manejar propiedades como password=True para seguridad o multiline=True para textos extensos.

* Checkbox y RadioGroup: Se utilizan para lógica booleana y selección múltiple o exclusiva. Mientras el Checkbox permite seleccionar varias opciones, el RadioGroup limita al usuario a una sola elección dentro de un conjunto.

* Dropdown: Optimiza el espacio en la interfaz al presentar una lista de opciones en un menú colapsable.

Controles de Acción y Visualización:

* ElevatedButton / IconButton: Son los disparadores de lógica. Ejecutan los Event Handlers asignados.

* ListView: Es un contenedor especializado en el manejo de grandes volúmenes de datos. Permite el desplazamiento (scroll) automático, lo cual es vital para aplicaciones como registros o chats.

* AlertDialog: Un componente de la capa de superposición (overlay) que interrumpe el flujo para solicitar una acción crítica o mostrar información importante.
#### 1.4.1 Referencia Sintáctica de Componentes (Code Snippets)
Para implementar estos controles en nuestros proyectos, utilizamos la siguiente sintaxis de Python:<br>
Controles de Salida (Output):
* Text (Etiquetas informativas)
```python
ft.Text("Usuario registrado con éxito", size=20, color="blue", weight="bold")
```
* CircleAvatar (Identificadores visuales)
```python
ft.CircleAvatar(content=ft.Text("JS"), bgcolor=ft.Colors.AMBER, radius=20)
```
Controles de Entrada (Input):
* TextField (Captura de strings/datos)
```python
# Ejemplo para password y para texto normal
ft.TextField(label="Contraseña", password=True, can_reveal_password=True)
ft.TextField(label="Comentarios", multiline=True, min_lines=3)
```
* Checkbox y RadioGroup (Lógica booleana y selección)
```python
# Checkbox: Selección múltiple
ft.Checkbox(label="Acepto términos y condiciones", value=False)

# RadioGroup: Selección única (necesita un contenedor para el layout)
ft.RadioGroup(content=ft.Row([
    ft.Radio(value="red", label="Rojo"),
    ft.Radio(value="blue", label="Azul")
]))
```
* Dropdown (Menús optimizados)
```python
ft.Dropdown(
    label="Selecciona tu carrera",
    options=[
        ft.dropdown.Option("Sistemas"),
        ft.dropdown.Option("Mecatrónica"),
    ]
)
```
Controles de Acción y Visualización:
* ElevatedButton e IconButton (Disparadores de eventos)
```python
ft.ElevatedButton("Guardar Datos", icon=ft.Icons.SAVE, on_click=mi_manejador)
ft.IconButton(icon=ft.Icons.DELETE_FOREVER, icon_color="red", on_click=borrar_datos)
```
* ListView (Gestión de colecciones de datos)
```python
# El ListView permite que el contenido sea "scrolleable"
chat_history = ft.ListView(expand=True, spacing=10, auto_scroll=True)
```
* AlertDialog (Componentes de interrupción/Overlay)
```python
# Se define pero se activa cambiando su propiedad .open a True
alerta = ft.AlertDialog(
    title=ft.Text("Confirmación"),
    content=ft.Text("¿Deseas salir del chat?"),
    actions=[ft.TextButton("Sí"), ft.TextButton("No")]
)
```
#### Ejemplo Integrador: Sistema de Chat Local (Multi-Usuario)
Este programa es la culminación de la unidad, ya que integra layouts complejos, manejo de eventos globales y una amplia variedad de componentes gráficos trabajando en conjunto.
```python
import flet as ft
from dataclasses import dataclass

# Definimos una estructura de datos para los mensajes (Sistemas: Manejo de Clases)
@dataclass
class Message:
    user_name: str
    text: str
    message_type: str

def main(page: ft.Page):
    page.title = "Flet Chat - TAP Unit 1"
    page.horizontal_alignment = ft.CrossAxisAlignment.STRETCH

    # --- LÓGICA DE COMUNICACIÓN (Eventos de Red) ---
    def on_message(message: Message):
        if message.message_type == "chat_message":
            # Agregamos un control de texto simple al ListView
            chat.controls.append(ft.Text(f"{message.user_name}: {message.text}"))
        elif message.message_type == "login_message":
            # Feedback visual de que alguien entró al sistema
            chat.controls.append(ft.Text(message.text, italic=True, color=ft.Colors.BLACK_45, size=12))
        page.update()

    page.pubsub.subscribe(on_message) # Suscripción al bus de eventos

    # --- COMPONENTES DE INTERFAZ ---

    # 1. Campo para el nombre (TextField con validación)
    join_user_name = ft.TextField(label="Introduce tu nombre para entrar", autofocus=True)

    # 2. Diálogo de bienvenida (AlertDialog para control de acceso)
    welcome_dlg = ft.AlertDialog(
        open=True,
        modal=True,
        title=ft.Text("Bienvenido al Chat"),
        content=ft.Column([join_user_name], width=300, height=70, tight=True),
        actions=[ft.ElevatedButton(content="Unirse", on_click=lambda _: join_chat())],
    )

    # 3. Área de mensajes (ListView para scroll automático)
    chat = ft.ListView(expand=True, spacing=10, auto_scroll=True)

    # 4. Campo de nuevo mensaje (TextField con manejo de Submit)
    new_message = ft.TextField(hint_text="Escribe un mensaje...", expand=True)

    def join_chat():
        if not join_user_name.value:
            join_user_name.error_text = "¡El nombre no puede estar vacío!"
            join_user_name.update()
        else:
            welcome_dlg.open = False
            # Evento PubSub para notificar a todos los nodos conectados
            page.pubsub.send_all(Message(join_user_name.value, f"{join_user_name.value} se ha unido al chat.", "login_message"))
            page.update()

    def send_message(e):
        if new_message.value != "":
            page.pubsub.send_all(Message(join_user_name.value, new_message.value, "chat_message"))
            new_message.value = ""
            page.update()

    # Agregando componentes al overlay y a la página principal
    page.overlay.append(welcome_dlg)
    page.add(
        ft.Container(content=chat, border=ft.border.all(1, ft.Colors.OUTLINE), expand=True, padding=10),
        ft.Row([
            new_message,
            ft.IconButton(icon=ft.Icons.SEND_ROUNDED, on_click=send_message)
        ])
    )

# Configuración del Host para permitir conexiones en red local
ft.app(target=main, view=ft.AppView.WEB_BROWSER, port=8550, host="0.0.0.0")
```
# Conclusión General de la Unidad I
La finalización de esta unidad marca un hito fundamental en nuestra formación como ingenieros de sistemas, ya que representa la transición de la programación lógica puramente algorítmica (back-end) hacia el desarrollo de Interfaces Gráficas de Usuario (GUI) funcionales y centradas en la experiencia del usuario. A través de la experimentación con el framework Flet, logramos comprender que el desarrollo de software moderno no es un proceso lineal, sino un sistema complejo de estados, componentes y respuestas en tiempo real.

En primer lugar, la exploración de la Creación de Interfaces nos permitió entender la importancia de la jerarquía de objetos. Comprendimos que cada ventana, botón o contenedor no es solo un elemento visual, sino una instancia de una clase con propiedades específicas que definen la usabilidad del sistema. La implementación de Layouts (Columnas, Filas y Grillas) nos enseñó que la organización espacial es crítica para la escalabilidad de la UI, permitiendo que nuestras aplicaciones sean coherentes y se adapten a diferentes resoluciones o plataformas.

En segundo lugar, profundizamos en el paradigma de la Programación Dirigida por Eventos. Este concepto cambió nuestra forma de estructurar el código: dejamos de escribir scripts que se ejecutan de principio a fin para desarrollar sistemas que "escuchan" y reaccionan de forma asíncrona a las acciones del usuario. El manejo de eventos mediante handlers y la manipulación del objeto de evento (e) nos dieron el control total sobre la interactividad, desde una simple suma en una calculadora hasta la sincronización de mensajes en un chat local mediante protocolos de comunicación como PubSub.

Finalmente, el Manejo de Componentes Gráficos de Control nos brindó las herramientas para asegurar la integridad de los datos. No solo aprendimos a renderizar componentes de entrada y salida, sino que integramos lógica de validación (como el uso de expresiones regulares) y gestión de estados para prevenir errores antes de que la información sea procesada por el backend.

En resumen, la Unidad I nos ha dotado de una visión integral sobre el desarrollo de aplicaciones. Ahora somos capaces de diseñar, estructurar y programar interfaces que no solo son estéticamente profesionales bajo los estándares de Material Design, sino que son técnicamente robustas, interactivas y capaces de resolver problemas de comunicación y gestión de datos en entornos reales.
