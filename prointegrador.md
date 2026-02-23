# Proyecto Integrador
```python```
>[!CAUTION]
> -Necesario crear un entorno virtual.
> 
> -Git Bash.
> 
> -Python 3.10 en adelante (puedes revisarlo con el comando "python --doctor" en Git Bash)

En este documento de GitHub, presentare como fui realizando mi proyecto integrador de la Unidad 1, el cual consiste en un formulario que sirve para registrar los datos de un estudiante, el cual podria ser usado para registrarse en cursos,reinscripciones, etc.

## Paso 1
Importamos Flet como un el paquete "ft" para que nos sea mas comodo llamarlo, ademas de ejecutar una segunda linea de codigo para ignorar errores molestos relacionados a la version de Flet.
```python
import flet as ft
```
## Paso 2
Definimos en main en el cual vamos a trabajar todo nuestro codigo, y despues damos forma a nuestra ventana, para que se vea bien.
```python
def main(page: ft.Page):
    page.title = "Registro de Estudiantes"
    page.bgcolor = "#FDFBE3"
    page.padding = 30
    page.theme_mode = ft.ThemeMode.LIGHT
```
## Paso 3
Aqui usamos el ```.TextField``` para poder ingresar los datos justo como nosotros queramos, acoplando para cada alumno.
```python
    txt_nombre = ft.TextField(label="Nombre", border_color="#4D2A32", expand=True)
    txt_control = ft.TextField(label="Número de control", border_color="#4D2A32", expand=True)
    txt_email = ft.TextField(label="Email", border_color="#4D2A32")
```
## Paso 4
En esta parte del codigo, creamos un ```ft.Dropdown``` para poder seleccionar la carrera, para que al clickearla despliega las demas opciones, de igual manera usamos un nuevo ```ft.Dropdown``` junto con un ciclo ```for``` para poder seleccionar el semestre.
```python
dd_carrera = ft.Dropdown(
        label="Carrera",
        expand=True,
        border_color="#4D2A32",
        options=[
            ft.dropdown.Option("Ingeniería en Sistemas"),
            ft.dropdown.Option("Ingeniería Civil"),
            ft.dropdown.Option("Ingeniería Industrial"),
        ]
    )

dd_semestre = ft.Dropdown(
        label="Semestre",
        expand=True,
        border_color="#4D2A32",
        options=[ft.dropdown.Option(str(i)) for i in range(1, 10)]
    )
```
## Paso 5
Aqui usamos el ```ft.RadioGroup``` para crear una seccion en donde podamos marcar el genero del alumno.
```python
rg_genero = ft.RadioGroup(
        content=ft.Row([
            ft.Radio(value="Macho", label="Macho"),
            ft.Radio(value="Hembra", label="Hembra"),
            ft.Radio(value="Otro", label="Otro"),
        ])
    )
```
## Paso 6
Aqui definimos lo que sera la ventana que sale al momento de ingresar los datos, solo que por el momento esta vacia.
```python
def cerrar_dialogo(e):
        dlg_datos.open = False
        page.update()
dlg_datos = ft.AlertDialog(
        title=ft.Text("Datos Registrados"),
        content=ft.Text(""),
        actions=[
            ft.TextButton("Aceptar", on_click=cerrar_dialogo),
        ],
    )
```
## Paso 7
Aqui definimos la parte donde si se detecta algun campo vacio en el formulario, en ese caso lanzamos un error.
```python
def enviar_click(e):
        if not txt_nombre.value or not txt_control.value or not txt_email.value or \
           not dd_carrera.value or not dd_semestre.value or not rg_genero.value:
            
            page.snack_bar = ft.SnackBar(
                content=ft.Text("¡Error! Por favor llena todos los campos incluyendo el género."),
                bgcolor=ft.Colors.RED_700
            )
            page.snack_bar.open = True
            page.update()
```
Si no, entonces se prepara el recuadro con toda la informacion ingresada.
```python
else:
            # Si todo está lleno, preparamos el texto para la ventana
            resumen = (
                f"Nombre: {txt_nombre.value}\n"
                f"Control: {txt_control.value}\n"
                f"Email: {txt_email.value}\n"
                f"Carrera: {dd_carrera.value}\n"
                f"Semestre: {dd_semestre.value}\n"
                f"Género: {rg_genero.value}"
            )
```
Enntonces metemos esta informacion a la ventana.
```python
 dlg_datos.content.value = resumen
            page.dialog = dlg_datos
            dlg_datos.open = True
            page.update()
```
## Paso 8
Aqui creamos el boton que sirve para poder enviar la informacio que ya tenemos.
```python
btn_enviar = ft.ElevatedButton(
        content=ft.Text("Enviar Datos", color="white", size=16),
        bgcolor="#4D2A32", # Cambié a un color más oscuro para que resalte
        width=page.width,
        style=ft.ButtonStyle(shape=ft.RoundedRectangleBorder(radius=5)),
        on_click=enviar_click
```
## Paso 9
Y aqui finalmente le damos forma a nuestro programa final, y verlo finalmente ejecutado.
```python
page.add(
        ft.Column([
            txt_nombre,
            txt_control,
            txt_email,
            ft.Row([dd_carrera, dd_semestre], spacing=10),
            
            # Título para el género y los botones
            ft.Column([
                ft.Text("Selecciona tu Género:", color="#4D2A32", weight=ft.FontWeight.BOLD),
                rg_genero
            ], spacing=5),
            
            ft.Divider(height=20, color="transparent"), # Un pequeño espacio
            btn_enviar
        ], spacing=15)
    )

ft.app(target=main, view=ft.AppView.WEB_BROWSER)
```
Finalmente, tenemos el codigo ejecutado.
<img width="900" height="700" alt="image" src="https://github.com/24680262/T.A.P-1/blob/main/flet%201.png"/>
<img width="400" height="400" alt="image" src="https://github.com/24680262/T.A.P-1/blob/main/flet%202.png"/>
