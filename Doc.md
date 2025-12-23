# DOCS

## Crea el entorno virtual
Ejecuta el siguiente comando. Esto creará una carpeta nueva (usualmente llamada venv, env o .venv) dentro de tu proyecto con todos los archivos necesarios.

En Windows:

```bash
python -m venv venv
```
## Activa el entorno virtual
Este paso es crucial. Debes "entrar" al entorno para usarlo.

En Windows (CMD):

```cmd
venv\Scripts\activate
```

En Windows (PowerShell):

```powershell
.\venv\Scripts\Activate.ps1
```

(Si recibes un error de permisos en PowerShell, mira la sección de "Solución de problemas" abajo).

## Bloqueo de seguridad en Windows PowerShell.

 Para solucionarlo, debes cambiar la política de ejecución para permitir scripts locales (como el de tu entorno virtual).

El comando más seguro y recomendado es este:

```PowerShell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

### ¿Qué hace exactamente este comando?
    - RemoteSigned: Permite ejecutar scripts que has creado tú mismo en tu ordenador (como el entorno virtual), pero requiere que los scripts descargados de internet estén firmados digitalmente por un editor de confianza. Es un equilibrio seguro.

    - Scope CurrentUser: Aplica este cambio solo a tu usuario, por lo que no necesitas permisos de administrador ni afectas a otros usuarios del sistema.

## Cambio de permisos temporal

solo dura mientras tienes esta ventana abierta (se borrará al cerrarla), el comando es este:

```PowerShell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope Process
```

### ¿Por qué usar este?
-Scope Process: Aplica el permiso solo a la sesión actual de la terminal.

_Seguridad_: En cuanto cierres la ventana de PowerShell, la configuración de seguridad volverá a su estado original (bloqueado). Es la opción menos intrusiva.

## Actualizar el PIP

Asegúrate de tener el entorno activado (verás el (venv) a la izquierda) y ejecuta:

```Bash
python -m pip install --upgrade pip
```

__Nota__: Usamos python -m pip en lugar de solo pip para asegurarnos de que se actualice el gestor del entorno actual y no el de tu sistema global.

## Dos librerías externas en tu entorno virtual.

### Comando de instalación
    
__Asegúrate de tener tu entorno activado (debe decir (venv) a la izquierda) y ejecuta:__

```Bash
pip install selenium python-docx
```

### ¿Para qué sirve cada una?

__selenium__: Es la que permite controlar el navegador (Chrome) automáticamente para entrar a WordPress, hacer clic en botones y llenar los campos.

__python-docx__: Es la librería que usas en from docx import Document. Permite que Python abra, lea y entienda el contenido (títulos, negritas, listas) de tus archivos de Word.

## Adaptación del Codigo a nuestro espacio de trabajo

```python
carpeta_word = r"C:\Users\Pink Stone\Desktop\Virtual-Actual-01"
```

__Esa línea define la carpeta de origen de donde el programa va a sacar los archivos para trabajar.__

__Su función específica en tu código es decirle al robot: "Oye, ve a esta ubicación exacta de mi computadora, busca todos los archivos de Word (.docx) que haya allí y úsalos para crear los posts en WordPress".__

### Un detalle técnico importante: la r

Verás que hay una r pequeña antes de las comillas: r"C:\Users...".

En Windows, las rutas se escriben con barras invertidas `\.`

En programación, la barra invertida a veces significa comandos especiales (como "salto de línea").

La r significa "Raw string" (Texto crudo). Le dice a Python: "Lee esta dirección tal cual está escrita, no intentes interpretar las barras invertidas como comandos especiales".