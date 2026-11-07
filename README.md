# The Doer Board

Tablón de publicaciones desarrollado con Python y Flask. Los usuarios pueden crear una cuenta, compartir anuncios con imágenes y categorías, comentar y votar publicaciones.

**Estado:** terminado. Este repositorio conserva el proyecto para el portafolio de Javier Guzmán.

## Funciones

- Registro, inicio de sesión y contraseñas almacenadas mediante hash.
- Publicaciones con imágenes y categorías creadas al escribir sus nombres.
- Búsqueda por título o contenido, filtros por categoría y orden por fecha o votos.
- Comentarios y votos individuales que se pueden retirar.
- Cuenta con foto de perfil.
- Panel de administración para eliminar publicaciones, bloquear usuarios y consultar el registro de acciones.

## Tecnologías

Python, Flask, Flask-SQLAlchemy, Flask-Login, SQLite, Jinja2, HTML, CSS y JavaScript.

## Ejecutar localmente

Se recomienda Python 3.13, la versión utilizada en el entorno original.

```powershell
git clone https://github.com/javieraguzman1204-cmd/doer-board.git
cd doer-board
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
$env:SECRET_KEY = (python -c "import secrets; print(secrets.token_hex(32))")
.\.venv\Scripts\python.exe -m flask --app app run
```

Abre <http://127.0.0.1:5000>. La base de datos se crea automáticamente en `instance/data.db` al recibir la primera solicitud. Registra una cuenta desde la pantalla de acceso para empezar a publicar.

En macOS o Linux, utiliza `.venv/bin/python` y configura la variable `SECRET_KEY` con la sintaxis de tu terminal.

`SECRET_KEY` firma las sesiones. Conserva su valor entre ejecuciones si quieres mantenerlas; si no la configuras, se genera una clave temporal al iniciar el proceso.

Las cuentas nuevas no reciben permisos de administración. Para probar el panel, crea una cuenta y abre `.\.venv\Scripts\python.exe -m flask --app app shell`:

```python
from app import db, User
usuario = User.query.filter_by(username="tu_usuario").one()
usuario.is_admin = True
db.session.commit()
```

## Estructura

```text
app.py             Rutas, modelos, autenticación y administración
templates/         Vistas HTML con Jinja2
static/css/        Estilos de la interfaz
static/js/         Conversión de fechas a la zona horaria local
requirements.txt   Dependencias del proyecto
```

Las imágenes subidas se guardan en `static/uploads/`. La base de datos, las imágenes de usuarios y los entornos virtuales quedan fuera de Git.

## Alcance

Proyecto terminado para demostración local. Antes de alojarlo para usuarios reales, requiere una revisión de seguridad y configuración de producción, incluida protección CSRF en formularios y un servidor WSGI. La versión actual no envía correos de confirmación, aunque el modelo reserva campos para ello.
