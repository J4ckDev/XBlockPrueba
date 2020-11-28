# :scroll: Xblock Prueba <!-- omit in toc -->

Guía para comprender como hacer uso de funciones para obtener datos de los usuarios y cursos de la plataforma **OpenEDX**.

## :clipboard: Contenido <!-- omit in toc -->

- [1. Entorno de Trabajo](#1-entorno-de-trabajo)
  - [1.1. Requisitos](#11-requisitos)
  - [1.2. Configuración del Entorno](#12-configuración-del-entorno)
  - [1.3  Configuración de la Plataforma](#13--configuración-de-la-plataforma)
- [2. Funcionamiento del XBlock](#2-funcionamiento-del-xblock)
  - [2.1. Renderizar Vistas](#21-renderizar-vistas)
  - [2.2. Consultar ID de Usuario](#22-consultar-id-de-usuario)

## 1. Entorno de Trabajo

Para modificar este XBlock o instalarlo es necesario tener instalados los requisitos y configurar el entorno de trabajo. Si desean saber como construir un XBlock desde cero, los invito a ver [esta pequeña guía](https://github.com/J4ckDev/MyXblock).

Para realizar las pruebas de instalación del XBlock es necesario tener una versión de la plataforma de **OpenEDX**, en mi caso haré uso de la versión **Ficus**.

### 1.1. Requisitos

Es importante contar con una versión de Ubuntu o Debian, contar con **Python 3.5 o mayor** e instalar las siguientes librerías mediante el *terminal*:

| Librería                               | Comando de Instalación               |
| :------------------------------------- | :----------------------------------- |
| GNOME XML library                      | `sudo apt-get install libxml2-dev`   |
| XSLT 1.0 processing library            | `sudo apt-get install libxslt-dev`   |
| Compression library 32-bit development | `sudo apt-get install lib32z1-dev`   |
| IJG JPEG library                       | `sudo apt-get install libjpeg62-dev` |
| Virtualenv                             | `pip install virtualenv`             |
### 1.2. Configuración del Entorno

Con las librerias necesarias instaladas, es momento de configurar el entorno de trabajo de la siguiente forma:

1. Crear una carpeta con el nombre que deseen, en mi caso la llamé *midirectorio* con el comando `mkdir midirectorio`.
2. Ingresar a la carpeta creada y ejecutar el comando `virtualenv venv`.
3. Iniciar el entorno virtual con el comando `source venv/bin/activate`. En mi caso luego de ejecutar el comando, en el terminal me apareció `(venv) jackdev@J4ckDev:~/midirectorio$`, el `(venv)` me indica que estoy trabajando en mi entorno virtual.
4. Obtener el XBlock SDK mediante el comando `git clone https://github.com/edx/xblock-sdk`.
5. Por último, abrir la carpeta del proyecto clonado con `cd xblock-sdk` y ejecutar el comando `pip install -r requirements/base.txt` 

### 1.3  Configuración de la Plataforma
## 2. Funcionamiento del XBlock

El XBlock sigue teniendo la funcionalidad por defecto que crea el *XBlock SDK*, que consiste en incrementar un contador al darle click a una etiqueta `p`. Como el fin de este XBlock es el de realizar pruebas para comprender como se pueden obtener datos de la plataforma *OpenEDX*, a continuación se irán presentando los datos que se logren consultar tanto usando el *XBlock SDK* y la plataforma de *OpenEDX*.

### 2.1. Renderizar Vistas

Sí se desean consultar datos en la plataforma de OpenEDX y se van a utilizar en cualquiera de las vistas de un XBlock, es necesario realizar los siguientes pasos:

1. Importar las siguientes librerías:
   
  | Librería | Descripción | 
  | :------------------------------------- | :----------------------------------- |
  | Template | En Django esta clase es la encargada de compilar el código plantilla que reciba, normalmente son fragmentos HTML que incluyen propiedades que deben ser procesadas y compiladas. Un ejemplo de los fragmentos que compila es el siguiente `<p>Hola, me llamo {{nombre_usuario}}</p>`.  |
  | Context | Esta clase de Django, es la encargada de procesar las plantillas compiladas por la clase Template y mapear la información contenida en un diccionario, luego usando `Template.render(context)` se renderiza todo para generar una vista estática. Siguiendo el ejemplo anterior sería algo así:<img src="./images/example.png" alt="Ejemplo de código"> |
  | Fragment | Es la librería que nos permite controlar todos los archivos asociados a la vista de un XBlock y mostrarlo en la página web, este incluye el contenido HTML, CSS y Javascript.|

  Fragmento de código resultante:

  ```python
  from xblock.fragment import Fragment
  from django.template import Context, Template
  ```

2. Declarar la variable o variables que contendrán los diferentes valores que se van a consultar en el archivo python del XBlock, en este caso `prueba.py`.

### 2.2. Consultar ID de Usuario