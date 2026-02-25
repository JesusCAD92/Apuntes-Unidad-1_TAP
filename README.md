# Reporte Técnico: Formulario de Registro de Estudiantes
**Proyecto Integrador - Unidad I** **Materia:** Tópicos Avanzados de Programación (TAP)  
**Herramientas:** Python, Flet, Git Bash
## 1. Objetivo del Módulo
Desarrollar una interfaz gráfica de usuario (GUI) funcional y responsiva que permita la captura, validación y visualización de datos de estudiantes, aplicando los principios de programación dirigida por eventos y manejo de componentes gráficos en Flet.
## 2. Arquitectura de la Página y Entorno
**Instrucciones:** 
* Definir el título de la ventana para mejorar el branding de la app.

* Configurar el bgcolor y padding para asegurar que la interfaz respire y no se vea saturada.

---
```python
import flet as ft
import re

def main(page: ft.Page):
    page.title = "Registro de Estudiantes - Tópicos Avanzados"
    page.bgcolor = "#FDFBE3"  # Color crema (Hexadecimal)
    page.padding = 30
    page.theme_mode = ft.ThemeMode.LIGHT # Forzamos tema claro para legibilidad
```
## 3. Construcción de Controles de Entrada (Inputs)
El manejo de componentes gráficos implica seleccionar el control adecuado según el tipo de dato que esperamos recibir (Subtema 1.4).<br>
<br>**Guía de Componentes:**

* TextField para Cadenas: Usamos expand=True para que el campo ocupe el ancho disponible en el layout responsivo.

* Validación de Tipo de Teclado: Para el número de control, restringimos el input a nivel de sistema con keyboard_type.

* Dropdown para Selección Cerrada: Evitamos errores de captura permitiendo que el usuario elija entre opciones predefinidas.

---
```python
# Definición de inputs
    txt_nombre = ft.TextField(label="Nombre", expand=True, bgcolor="white")
    txt_control = ft.TextField(
        label="Número de control",
        keyboard_type=ft.KeyboardType.NUMBER, 
        expand=True,
        bgcolor="white"
    )
    
    txt_email = ft.TextField(label="Email", expand=True, bgcolor="white")

    dd_carrera = ft.Dropdown(
        label="Carrera",
        expand=True,
        options=[
            ft.dropdown.Option("Ingeniería en Sistemas"),
            ft.dropdown.Option("Ingeniería Civil"),
            ft.dropdown.Option("Ingeniería Industrial"),
            ft.dropdown.Option("Gestión Empresarial"),
            ft.dropdown.Option("Ingeniería Mecatrónica"),
            ft.dropdown.Option("Ingeniería Electrónica"),
            ft.dropdown.Option("Contabilidad")
        ]
    )
```
## 4. Implementación de Lógica de Validación (Regex)
Como ingenieros, no podemos confiar en que el usuario ingrese datos correctos. Utilizamos Expresiones Regulares (Regex) para validar patrones complejos como el correo electrónico.<br>
<br>**¿Cómo funciona el Regex en este código?** El patrón r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$' verifica:

1) Que existan caracteres antes del @.

2) Que haya un dominio válido.

3) Que la extensión (como .com o .mx) tenga al menos 2 letras.

---
```python
patron_email = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'

def guardar_click(e):
    # Verificación del patrón mediante la librería 're'
    if not re.match(patron_email, txt_email.value):
        txt_email.error_text = "Formato de correo inválido"
        txt_email.border_color = "red"
        page.update()
```
## 5. Gestión de Eventos y Feedback Visual
El Manejo de Eventos (Subtema 1.3) es lo que hace que la app sea interactiva. Cuando el usuario hace clic, el programa debe responder de inmediato.<br>
<br>**El proceso de Feedback:**

* Si hay un error de validación, se modifica la propiedad error_text del componente.

* Si los datos son válidos, se utiliza un AlertDialog para confirmar la acción. El diálogo se agrega al page.overlay ya que es un componente de capa superior.

---
```python
# Creación del componente de alerta (Overlay)
    dialog = ft.AlertDialog(title=ft.Text("Información Guardada"))
    page.overlay.append(dialog)

    def guardar_click(e):
        # Lógica de procesamiento de datos...
        dialog.content = ft.Text(f"Nombre: {txt_nombre.value}")
        dialog.open = True # Mostramos la alerta
        page.update()
```
## 6. Diseño del Layout Responsivo
Para que el formulario se vea ordenado, utilizamos una combinación de Columnas (flujo vertical) y Filas (flujo horizontal), aplicando los conocimientos del Subtema 1.1.<br>
<br>**Instrucciones de Acomodo:**

* Agrupar Carrera y Semestre en una ft.Row para aprovechar el ancho de pantalla.

* Usar spacing=15 para evitar que los campos se vean amontonados.

---
```python
page.add(
        ft.Column([
            txt_nombre,
            txt_control,
            txt_email,
            ft.Row([dd_carrera, dd_semestre], spacing=10),
            ft.Row([ft.Text("Género:", weight="bold"), genero]),
            btn_enviar
        ], spacing=15, scroll=ft.ScrollMode.AUTO)
    )
```
## 7. Código Completo para Implementación
A continuación, se presenta el código fuente íntegro para su ejecución directa:

---
```python
import flet as ft
import re

# Definición del patrón de email (Regex)
patron_email = r'^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$'

def main(page: ft.Page):
    # 1. CONFIGURACIÓN DE PÁGINA
    page.title = "Registro de Estudiantes - Tópicos Avanzados"
    page.bgcolor = "#FDFBE3" 
    page.padding = 30
    page.theme_mode = ft.ThemeMode.LIGHT
    
    # 2. CONTROLES DE ENTRADA
    txt_nombre = ft.TextField(label="Nombre", expand=True, bgcolor="white")
    txt_control = ft.TextField(label="Número de control", keyboard_type=ft.KeyboardType.NUMBER, expand=True, bgcolor="white")
    txt_email = ft.TextField(label="Email", expand=True, bgcolor="white")

    dd_carrera = ft.Dropdown(
        label="Carrera",
        expand=True,
        border_color="#4D2A32",
        bgcolor="white",
        options=[
            ft.dropdown.Option("Ingeniería en Sistemas"),
            ft.dropdown.Option("Ingeniería Civil"),
            ft.dropdown.Option("Ingeniería Industrial"),
            ft.dropdown.Option("Gestión Empresarial"),
            ft.dropdown.Option("Ingeniería Mecatrónica"),
            ft.dropdown.Option("Ingeniería Electrónica"),
            ft.dropdown.Option("Contabilidad")
        ]
    )

    dd_semestre = ft.Dropdown(
        label="Semestre",
        expand=True,
        border_color="#4D2A32",
        bgcolor="white",
        options=[ft.dropdown.Option(str(i)) for i in range(1, 14)]
    )
    
    genero = ft.RadioGroup(
        content=ft.Row([
            ft.Radio(value="Masculino", label="Masculino"),
            ft.Radio(value="Femenino", label="Femenino"),
        ], alignment=ft.MainAxisAlignment.START)
    )

    # 3. COMPONENTES DE SUPERPOSICIÓN (OVERLAY)
    dialog = ft.AlertDialog(title=ft.Text("Información Guardada"))
    page.overlay.append(dialog)
    
    # 4. MANEJO DE EVENTOS
    def guardar_click(e):
        txt_nombre.error_text = None
        txt_control.error_text = None
        txt_email.error_text = None
        formulario_valido = True

        if not txt_nombre.value or not txt_nombre.value.strip():
            txt_nombre.error_text = "El nombre es obligatorio"
            formulario_valido = False
            
        if not txt_control.value or not txt_control.value.strip():
            txt_control.error_text = "El No. de Control es obligatorio"
            formulario_valido = False
        elif not txt_control.value.isdigit():
            txt_control.error_text = "Solo se permiten números"
            formulario_valido = False

        if not txt_email.value or not txt_email.value.strip():
            txt_email.error_text = "El Email es obligatorio"
            formulario_valido = False
        elif not re.match(patron_email, txt_email.value):
            txt_email.error_text = "Formato inválido (ejemplo@gmail.com)"
            formulario_valido = False
        
        if not formulario_valido:
            page.update()
            return  

        dialog.content = ft.Container(
            content=ft.Column([        
                ft.Text(f"Nombre: {txt_nombre.value}"),
                ft.Text(f"No. Control: {txt_control.value}"),
                ft.Text(f"Gmail: {txt_email.value}"),
                ft.Text(f"Carrera: {dd_carrera.value}"),
                ft.Text(f"Semestre: {dd_semestre.value}"),
                ft.Text(f"Género: {genero.value}")
            ], tight=True), width=400, padding=20
        )
        dialog.open = True
        page.update()

    # 5. BOTÓN DE ENVÍO
    btn_enviar = ft.Button(
        content=ft.Text("Enviar Datos", color="black", size=16),
        bgcolor=ft.Colors.GREY_500,
        width=page.width,
        on_click=guardar_click
    )

    page.add(
        ft.Column([
            txt_nombre,
            txt_control,
            txt_email,
            ft.Row([dd_carrera, dd_semestre], spacing=10),
            ft.Row([ft.Text("Género:", weight="bold", color="#4D2A32"), genero]),
            btn_enviar
        ], spacing=15, scroll=ft.ScrollMode.AUTO)
    )

if __name__ == "__main__":
    ft.app(target=main)
```

---
### Ejemplo visual del resultado final: 
<img width="1584" height="875" alt="image" src="https://github.com/user-attachments/assets/31252328-889c-4786-98b7-b7c6912cf0a1" />

## 8. Resolución de Problemas Comunes (Troubleshooting)
**❌ Problema 1: Los cambios en la interfaz no se visualizan * Causa:** Olvidar invocar el método page.update().

* Solución: Siempre llama a page.update() después de modificar el valor de un control en una función.<br>

<br>**❌ Problema 2: El Regex de Email falla con correos válidos * Causa:** Espacios invisibles al inicio o final de la cadena.

* Solución: Usar .strip() en el valor: email_limpio = txt_email.value.strip().<br>

<br>**❌ Problema 3: Error "Port busy" o puerto ocupado * Causa:** Otra instancia del programa está usando el puerto 8550.

* Solución: Cierra el proceso anterior en Git Bash o usa ft.app(target=main, port=8080).<br>
## 9. Glosario de Términos Técnicos Aplicados
* Callback: Función que se ejecuta en respuesta a un evento.

* Event Loop: Ciclo de espera de interacciones del usuario.

* Hexadecimal (#): Código de colores para la interfaz gráfica.

* Regex: Patrones para validar sintaxis de datos.

* Stretching: Ajuste de un componente para ocupar el ancho total disponible.
## Conclusión 
Como estudiante de cuarto semestre, el desarrollo de este proyecto integrador representó un desafío interesante y una transición necesaria de la programación lógica hacia el desarrollo de software centrado en el usuario. A menudo, en las materias de programación iniciales, nos enfocamos tanto en que el algoritmo funcione que olvidamos la importancia de la capa de presentación. Con este formulario, entendí que el diseño de una interfaz no es solo "que se vea bien", sino que debe ser funcional, responsiva y capaz de prevenir errores antes de que lleguen a la base de datos.

El uso de Flet me permitió ver cómo los conceptos de la Programación Orientada a Objetos se aplican en la vida real: cada botón, campo de texto y lista desplegable es un objeto con propiedades y estados que debemos gestionar. Además, implementar validaciones con Expresiones Regulares (Regex) fue una de las partes más satisfactorias, ya que me dio la seguridad de que el sistema solo procesará información íntegra y con el formato correcto.

Este proyecto no solo fortaleció mis habilidades técnicas en Python, sino que también me familiarizó con herramientas esenciales en la industria como Git Bash para el control de versiones. Al final, me llevo la satisfacción de haber construido una aplicación que no es estática, sino que responde de manera dinámica a los eventos del usuario. Este es, sin duda, un paso firme hacia la creación de sistemas más complejos y profesionales en los próximos semestres de la carrera.
