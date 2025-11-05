Para organizar correctamente el proyecto de Django con la estructura que mencionas, aquí te dejo la guía de cómo deberías crear las carpetas y archivos necesarios, paso a paso, siguiendo tu plan.

### 1. Crear carpeta del Proyecto: `UIII_Videojuegos_0358`

```bash
mkdir UIII_Videojuegos_0358
cd UIII_Videojuegos_0358
```

---

### 2. Abrir VS Code sobre la carpeta `UIII_Videojuegos_0358`

En la terminal (en la carpeta del proyecto):

```bash
code .
```

---

### 3. Abrir terminal en VS Code

* Abre VS Code y en el menú superior ve a `Terminal` > `Nuevo Terminal`.

---

### 4. Crear carpeta del entorno virtual `.venv` desde la terminal de VS Code

```bash
python -m venv .venv
```

---

### 5. Activar el entorno virtual

#### Para Windows:

```bash
.venv\Scripts\activate
```

#### Para macOS/Linux:

```bash
source .venv/bin/activate
```

---

### 6. Activar intérprete de Python en VS Code

1. En VS Code, presiona `Ctrl+Shift+P` o `Cmd+Shift+P` (en macOS) para abrir la paleta de comandos.
2. Escribe `Python: Select Interpreter` y selecciona el entorno virtual `.venv` creado.

---

### 7. Instalar Django

```bash
pip install django
```

---

### 8. Crear proyecto `backend_Videojuegos` sin duplicar carpeta

Asegúrate de que estás en la carpeta `UIII_Videojuegos_0358` y luego ejecuta:

```bash
django-admin startproject backend_Videojuegos .
```

> Nota: El `.` al final evita que se cree una carpeta extra con el nombre del proyecto.

---

### 9. Ejecutar servidor en el puerto 8035

Dentro de la carpeta `backend_Videojuegos`, ejecuta:

```bash
python manage.py runserver 8035
```

---

### 10. Copiar y pegar el link en el navegador

Abre el navegador y navega a `http://127.0.0.1:8035/` para ver que el servidor está funcionando correctamente.

---

### 11. Crear la aplicación `app_Videojuegos`

Dentro de la carpeta del proyecto, ejecuta:

```bash
python manage.py startapp app_Videojuegos
```

---

### 12. Crear la estructura de carpetas y archivos (según los pasos del proyecto)

#### Estructura básica de carpetas:

```bash
UIII_Videojuegos_0358/
├── backend_Videojuegos/
│   ├── manage.py
│   ├── backend_Videojuegos/
│   ├── app_Videojuegos/
│   │   ├── migrations/
│   │   ├── __init__.py
│   │   ├── admin.py
│   │   ├── apps.py
│   │   ├── models.py
│   │   ├── views.py
│   │   ├── urls.py
│   │   ├── templates/
│   │   │   ├── base.html
│   │   │   ├── footer.html
│   │   │   ├── header.html
│   │   │   ├── navbar.html
│   │   │   ├── inicio.html
│   │   │   └── genero/
│   │   │       ├── agregar_genero.html
│   │   │       ├── ver_generos.html
│   │   │       ├── actualizar_genero.html
│   │   │       └── borrar_genero.html
│   ├── settings.py
│   ├── urls.py
│   ├── wsgi.py
│   └── asgi.py
└── .venv/
```

---

### 13. Primero trabajamos con el **modelo: Género**

No mencionaste el código para el modelo "Género", así que asumo que es un modelo similar a los de Cliente y Empleado. A continuación, lo agrego como ejemplo:

#### `models.py` dentro de `app_Videojuegos`

```python
from django.db import models

class Genero(models.Model):
    nombre = models.CharField(max_length=100)
    descripcion = models.TextField()

    def __str__(self):
        return self.nombre
```

---

### 14. Crear las funciones en `views.py` (CRUD para Género)

En `views.py` dentro de `app_Videojuegos`, implementa las siguientes funciones:

```python
from django.shortcuts import render, redirect
from .models import Genero

# Vista de inicio
def inicio_videojuegos(request):
    return render(request, 'inicio.html')

# Agregar Género
def agregar_genero(request):
    if request.method == 'POST':
        nombre = request.POST['nombre']
        descripcion = request.POST['descripcion']
        Genero.objects.create(nombre=nombre, descripcion=descripcion)
        return redirect('ver_generos')
    return render(request, 'genero/agregar_genero.html')

# Ver Géneros
def ver_generos(request):
    generos = Genero.objects.all()
    return render(request, 'genero/ver_generos.html', {'generos': generos})

# Actualizar Género
def actualizar_genero(request, id):
    genero = Genero.objects.get(id=id)
    if request.method == 'POST':
        genero.nombre = request.POST['nombre']
        genero.descripcion = request.POST['descripcion']
        genero.save()
        return redirect('ver_generos')
    return render(request, 'genero/actualizar_genero.html', {'genero': genero})

# Borrar Género
def borrar_genero(request, id):
    genero = Genero.objects.get(id=id)
    genero.delete()
    return redirect('ver_generos')
```

---

### 15. Crear la carpeta `templates` dentro de `app_Videojuegos`

Ya la has creado anteriormente dentro de la estructura, pero si no la has creado aún:

```bash
mkdir -p app_Videojuegos/templates/genero
```

---

### 16. Crear los archivos `base.html`, `header.html`, `navbar.html`, `footer.html`, `inicio.html`

¡Por supuesto! A continuación te doy todo el código de los archivos HTML y Python necesarios para tu proyecto Django. Esto incluye las plantillas HTML, las vistas, las URLs y todo lo que necesitas para la estructura completa.

### **Estructura de Carpetas**

```plaintext
UIII_Videojuegos_0358/
├── backend_Videojuegos/
│   ├── manage.py
│   ├── backend_Videojuegos/
│   ├── app_Videojuegos/
│   │   ├── migrations/
│   │   ├── __init__.py
│   │   ├── admin.py
│   │   ├── apps.py
│   │   ├── models.py
│   │   ├── views.py
│   │   ├── urls.py
│   │   ├── templates/
│   │   │   ├── base.html
│   │   │   ├── footer.html
│   │   │   ├── header.html
│   │   │   ├── navbar.html
│   │   │   ├── inicio.html
│   │   │   └── genero/
│   │   │       ├── agregar_genero.html
│   │   │       ├── ver_generos.html
│   │   │       ├── actualizar_genero.html
│   │   │       └── borrar_genero.html
│   ├── settings.py
│   ├── urls.py
│   ├── wsgi.py
│   └── asgi.py
└── .venv/
```

---

### **1. Archivos HTML**

#### **`base.html`**

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistema de Administración Videojuegos</title>
    <link href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" rel="stylesheet">
    {% block head %}
    {% endblock %}
</head>
<body>
    {% include 'header.html' %}
    {% include 'navbar.html' %}
    
    <div class="container">
        {% block content %}
        {% endblock %}
    </div>
    
    {% include 'footer.html' %}
    
    <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.5.2/dist/umd/popper.min.js"></script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.min.js"></script>
</body>
</html>
```

---

#### **`header.html`**

```html
<header class="header bg-light text-center py-3">
    <h1>Sistema de Administración Videojuegos</h1>
</header>
```

---

#### **`navbar.html`**

```html
<nav class="navbar navbar-expand-lg navbar-light bg-light">
  <a class="navbar-brand" href="#">Sistema de Administración Videojuegos</a>
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
    <span class="navbar-toggler-icon"></span>
  </button>
  <div class="collapse navbar-collapse" id="navbarNav">
    <ul class="navbar-nav">
      <li class="nav-item active">
        <a class="nav-link" href="{% url 'inicio_videojuegos' %}">Inicio</a>
      </li>
      <li class="nav-item">
        <a class="nav-link" href="#">Géneros</a>
        <ul class="dropdown-menu">
          <li><a class="dropdown-item" href="{% url 'agregar_genero' %}">Agregar Género</a></li>
          <li><a class="dropdown-item" href="{% url 'ver_generos' %}">Ver Géneros</a></li>
          <li><a class="dropdown-item" href="#">Actualizar Género</a></li>
          <li><a class="dropdown-item" href="#">Borrar Género</a></li>
        </ul>
      </li>
      <!-- Agregar más secciones como Plataformas y Videojuegos -->
    </ul>
  </div>
</nav>
```

---

#### **`footer.html`**

```html
<footer class="footer bg-light fixed-bottom text-center py-3">
    <p>&copy; {{ current_year }} - Creado por Andrés Sandova, Cbtis 128</p>
</footer>
```

---

#### **`inicio.html`**

```html
{% extends 'base.html' %}
{% block content %}
    <div class="text-center">
        <h1>Bienvenido al Sistema de Administración Videojuegos</h1>
        <img src="https://example.com/imagen_videojuegos.jpg" alt="Imagen de Videojuegos" class="img-fluid">
    </div>
{% endblock %}
```

---

### **2. Archivos Específicos para Géneros**

#### **`agregar_genero.html`**

```html
{% extends 'base.html' %}
{% block content %}
<h2>Agregar Género</h2>
<form method="POST">
    {% csrf_token %}
    <div class="form-group">
        <label for="nombre">Nombre del Género</label>
        <input type="text" class="form-control" id="nombre" name="nombre" required>
    </div>
    <div class="form-group">
        <label for="descripcion">Descripción</label>
        <textarea class="form-control" id="descripcion" name="descripcion" rows="3" required></textarea>
    </div>
    <button type="submit" class="btn btn-primary">Agregar Género</button>
</form>
{% endblock %}
```

---

#### **`ver_generos.html`**

```html
{% extends 'base.html' %}
{% block content %}
<h2>Géneros Disponibles</h2>
<table class="table">
  <thead>
    <tr>
      <th scope="col">Nombre</th>
      <th scope="col">Descripción</th>
      <th scope="col">Acciones</th>
    </tr>
  </thead>
  <tbody>
    {% for genero in generos %}
      <tr>
        <td>{{ genero.nombre }}</td>
        <td>{{ genero.descripcion }}</td>
        <td>
          <a href="{% url 'actualizar_genero' genero.id %}" class="btn btn-warning btn-sm">Editar</a>
          <a href="{% url 'borrar_genero' genero.id %}" class="btn btn-danger btn-sm">Borrar</a>
        </td>
      </tr>
    {% endfor %}
  </tbody>
</table>
{% endblock %}
```

---

#### **`actualizar_genero.html`**

```html
{% extends 'base.html' %}
{% block content %}
<h2>Actualizar Género: {{ genero.nombre }}</h2>
<form method="POST">
    {% csrf_token %}
    <div class="form-group">
        <label for="nombre">Nombre del Género</label>
        <input type="text" class="form-control" id="nombre" name="nombre" value="{{ genero.nombre }}" required>
    </div>
    <div class="form-group">
        <label for="descripcion">Descripción</label>
        <textarea class="form-control" id="descripcion" name="descripcion" rows="3" required>{{ genero.descripcion }}</textarea>
    </div>
    <button type="submit" class="btn btn-success">Actualizar Género</button>
</form>
{% endblock %}
```

---

#### **`borrar_genero.html`**

```html
{% extends 'base.html' %}
{% block content %}
<h2>¿Estás seguro de que deseas borrar el género: {{ genero.nombre }}?</h2>
<form method="POST">
    {% csrf_token %}
    <button type="submit" class="btn btn-danger">Eliminar</button>
    <a href="{% url 'ver_generos' %}" class="btn btn-secondary">Cancelar</a>
</form>
{% endblock %}
```

---

### **3. Views en `views.py`**

En `app_Videojuegos/views.py`, escribe las funciones para manejar el CRUD de **Géneros**:

```python
from django.shortcuts import render, redirect, get_object_or_404
from .models import Genero
from django.http import HttpResponse

# Vista de inicio
def inicio_videojuegos(request):
    return render(request, 'inicio.html')

# Agregar género
def agregar_genero(request):
    if request.method == 'POST':
        nombre = request.POST.get('nombre')
        descripcion = request.POST.get('descripcion')
        Genero.objects.create(nombre=nombre, descripcion=descripcion)
        return redirect('ver_generos')
    return render(request, 'genero/agregar_genero.html')

# Ver géneros
def ver_generos(request):
    generos = Genero.objects.all()
    return render(request, 'genero/ver_generos.html', {'generos': generos})

# Actualizar género
def actualizar_genero(request, id):
    genero = get_object_or_404(Genero, id=id)
    if request.method == 'POST':
        genero.nombre = request.POST.get('nombre')
        genero.descripcion =
```


request.POST.get('descripcion')
genero.save()
return redirect('ver_generos')
return render(request, 'genero/actualizar_genero.html', {'genero': genero})

# Borrar género

def borrar_genero(request, id):
genero = get_object_or_404(Genero, id=id)
if request.method == 'POST':
genero.delete()
return redirect('ver_generos')
return render(request, 'genero/borrar_genero.html', {'genero': genero})

````

---

### **4. URLs en `urls.py`**

Crea el archivo `urls.py` dentro de la aplicación `app_Videojuegos` con las rutas necesarias:

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.inicio_videojuegos, name='inicio_videojuegos'),
    path('agregar_genero/', views.agregar_genero, name='agregar_genero'),
    path('ver_generos/', views.ver_generos, name='ver_generos'),
    path('actualizar_genero/<int:id>/', views.actualizar_genero, name='actualizar_genero'),
    path('borrar_genero/<int:id>/', views.borrar_genero, name='borrar_genero'),
]
````

---

### **5. Configuraciones en `settings.py` y `urls.py` del Proyecto**

En el archivo `settings.py`, agrega la aplicación `app_Videojuegos` a `INSTALLED_APPS`:

```python
INSTALLED_APPS = [
    ...
    'app_Videojuegos',
]
```

En el archivo `urls.py` del proyecto (backend_Videojuegos/urls.py), agrega la ruta a las URLs de la aplicación:

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('app_Videojuegos.urls')),
]
```

---

Con todo esto, deberías tener la estructura completa para el proyecto. ¡Espero que te sirva! Si tienes alguna pregunta o necesitas algo más, no dudes en pedírmelo.

En la carpeta `app_Videojuegos/templates/`, crea los siguientes archivos.

#### `base.html`

Este archivo será la plantilla base de todas las páginas de tu aplicación.

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistema de Administración Videojuegos</title>
    <link href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" rel="stylesheet">
    {% block head %}
    {% endblock %}
</head>
<body>
    {% include 'header.html' %}
    {% include 'navbar.html' %}
    
    <div class="container">
        {% block content %}
        {% endblock %}
    </div>
    
    {% include 'footer.html' %}
    
    <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.5.2/dist/umd/popper.min.js"></script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.min.js"></script>
</body>
</html>
```

---

### 17. Agregar Bootstrap a `base.html`

Ya lo hemos hecho en el paso anterior.

---

### 18. Crear el archivo `navbar.html`

```html
<nav class="navbar navbar-expand-lg navbar-light bg-light">
  <a class="navbar-brand" href="#">Sistema de Administración Videojuegos</a>
  <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
    <span class="navbar-toggler-icon"></span>
  </button>
  <div class="collapse navbar-collapse" id="navbarNav">
    <ul class="navbar-nav">
      <li class="nav-item active">
        <a class="nav-link" href="{% url 'inicio_videojuegos' %}">Inicio</a>
      </li>
      <li class="nav-item">
        <a class="nav-link" href="#">Géneros</a>
        <ul class="dropdown-menu">
          <li><a href="{% url 'agregar_genero' %}">Agregar Género</a></li>
          <li><a href="{% url 'ver_generos' %}">Ver Géneros</a></li>
          <li><a href="#">Actualizar Género</a></li>
          <li><a href="#">Borrar Género</a></li>
        </ul>
      </li>
      <!-- Agregar más secciones como Plataformas y Videojuegos -->
    </ul>
  </div>
</nav>
```

---

### 19. Crear el archivo `footer.html`

```html
<footer class="footer bg-light fixed-bottom text-center py-3">
    <p>&copy; {{ current_year }} - Creado por Andrés Sandova, Cbtis 128</p>
</footer>
```

---

###


20. Crear el archivo `inicio.html`

```html
{% extends 'base.html' %}
{% block content %}
    <div class="text-center">
        <h1>Bienvenido al Sistema de Administración Videojuegos</h1>
        <img src="https://www.example.com/videojuegos.jpg" alt="Imagen de Videojuegos" width="400">
    </div>
{% endblock %}
```

---

### 21. Crear subcarpeta `genero` dentro de `templates`

Ya hemos creado `app_Videojuegos/templates/genero/`, pero asegúrate de que existan los siguientes archivos:

* `agregar_genero.html`
* `ver_generos.html`
* `actualizar_genero.html`
* `borrar_genero.html`

Cada archivo debe contener el código necesario para las vistas del CRUD.

---

### 22. Crear el archivo `urls.py` en `app_Videojuegos`

Dentro de `app_Videojuegos/`, crea el archivo `urls.py`:

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.inicio_videojuegos, name='inicio_videojuegos'),
    path('agregar-genero/', views.agregar_genero, name='agregar_genero'),
    path('ver-generos/', views.ver_generos, name='ver_generos'),
    path('actualizar-genero/<int:id>/', views.actualizar_genero, name='actualizar_genero'),
    path('borrar-genero/<int:id>/', views.borrar_genero, name='borrar_genero'),
]
```

---

### 23. Agregar la app `app_Videojuegos` en `settings.py` de `backend_Videojuegos`

Abre `backend_Videojuegos/settings.py` y agrega `'app_Videojuegos'` en la lista `INSTALLED_APPS`:

```python
INSTALLED_APPS = [
    ...
    'app_Videojuegos',
]
```

---

### 24. Configurar `urls.py` en `backend_Videojuegos`

En `backend_Videojuegos/urls.py`, agrega el enlace a `app_Videojuegos.urls`:

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('app_Videojuegos.urls')),
]
```

---

### 25. Registrar los modelos en `admin.py` de `app_Videojuegos`

En `app_Videojuegos/admin.py`, registra el modelo `Genero`:

```python
from django.contrib import admin
from .models import Genero

admin.site.register(Genero)
```

---

### 26. Realizar las migraciones

Ejecuta los siguientes comandos:

```bash
python manage.py makemigrations
python manage.py migrate
```

---

### 27. Ejecutar el servidor nuevamente en el puerto 8035

```bash
python manage.py runserver 8035
```

Con esto, el proyecto debería estar listo y funcionando.
