# Ágora Sexual

Ágora Sexual es un proyecto de asistencia conversacional orientado a la educación sexual y la salud sexual y reproductiva.

El sistema utiliza un backend desarrollado con **Python + Flask** y se conecta con **Google Gemini** para generar respuestas mediante un asistente denominado **Salia**.

## Descripción del proyecto

El objetivo de Ágora Sexual es ofrecer un espacio digital de orientación educativa sobre temas como:

- Educación sexual.
- Salud sexual y reproductiva.
- Infecciones de transmisión sexual (ITS).
- Métodos anticonceptivos.
- Anatomía sexual y reproductiva.
- Consentimiento y relaciones afectivas.
- Embarazo y prevención.
- Orientación sexual e identidad.
- Bienestar sexual.

El asistente está configurado para limitar sus respuestas al alcance educativo del proyecto y para rechazar consultas que no estén relacionadas con sexualidad, salud sexual o salud reproductiva.

## Tecnologías utilizadas

- Python
- Flask
- Google Gemini API
- Google Gen AI SDK
- python-dotenv
- Tenacity
- HTML/CSS/JavaScript para la interfaz web

## Estructura del proyecto

Una estructura recomendada es:

```text
agorasexual/
│
├── app.py
├── .env
├── .env.example
├── .gitignore
├── requirements.txt
├── README.md
│
└── templates/
    └── index.html
```

Si el proyecto incorpora más archivos de frontend, imágenes, estilos o scripts, pueden añadirse dentro de sus respectivas carpetas.

## Requisitos

Antes de ejecutar el proyecto necesitas:

1. Python 3 instalado.
2. Una clave de API de Google Gemini.
3. Git instalado si deseas trabajar con GitHub.
4. Las dependencias Python del proyecto.

## Instalación

### 1. Clonar el repositorio

Cuando el proyecto ya esté publicado en GitHub:

```bash
git clone https://github.com/TU_USUARIO/agora-sexual.git
cd agora-sexual
```

### 2. Crear un entorno virtual

En Windows:

```bash
python -m venv .venv
```

Activar el entorno:

```bash
.venv\Scripts\activate
```

Si utilizas PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

### 3. Instalar dependencias

```bash
pip install -r requirements.txt
```

Si todavía no existe `requirements.txt`, puedes instalar manualmente las dependencias principales:

```bash
pip install flask google-genai python-dotenv tenacity
```

## Configuración de variables de entorno

Crea un archivo llamado:

```text
.env
```

en la raíz del proyecto.

Ejemplo:

```env
GEMINI_API_KEY=TU_CLAVE_DE_GEMINI
FLASK_SECRET_KEY=UNA_CLAVE_SECRETA_SEGURA
```

### Importante

**No subas `.env` a GitHub.**

El archivo `.env` contiene información privada, especialmente la clave de API de Gemini. GitHub recomienda no subir contraseñas, claves de API ni otra información confidencial a un repositorio remoto.

Para compartir las variables necesarias sin revelar sus valores, utiliza `.env.example`.

Ejemplo:

```env
GEMINI_API_KEY=
FLASK_SECRET_KEY=
```

## Ejecutar el proyecto

Con el entorno virtual activado:

```bash
python app.py
```

El servidor Flask se ejecutará en:

```text
http://127.0.0.1:5000
```

También puedes abrir:

```text
http://localhost:5000
```

## Endpoint de salud

El proyecto incluye un endpoint para verificar que el backend está funcionando:

```text
GET /api/salud
```

Por ejemplo:

```text
http://127.0.0.1:5000/api/salud
```

La respuesta esperada es similar a:

```json
{
  "ok": true,
  "servicio": "Ágora Sexual",
  "estado": "activo"
}
```

## Endpoint del chatbot

El endpoint principal del chatbot es:

```text
POST /api/chat
```

El backend espera un JSON con el siguiente formato:

```json
{
  "message": "¿Qué son las ITS?"
}
```

Y devuelve una respuesta similar a:

```json
{
  "response": "..."
}
```

## Limpiar el historial

El proyecto también incluye:

```text
POST /api/limpiar
```

Este endpoint elimina el historial de conversación almacenado en la sesión del usuario.

## Manejo de errores de Gemini

El backend implementa reintentos automáticos para errores temporales como:

- `503 UNAVAILABLE`
- `429 RESOURCE_EXHAUSTED`
- `500 INTERNAL`
- `TIMEOUT`

Esto permite volver a intentar una solicitud cuando el servicio de Gemini se encuentra temporalmente saturado o no disponible.

Si el servicio continúa sin estar disponible después de los reintentos, el backend devuelve un mensaje controlado al cliente en lugar de mostrar el error interno de Gemini.

## Seguridad

El proyecto incorpora medidas básicas para reducir problemas habituales:

- La API Key se obtiene desde variables de entorno.
- `.env` se excluye mediante `.gitignore`.
- El backend limita el tamaño de los mensajes recibidos.
- Se valida que la solicitud tenga contenido JSON válido.
- Se limita el historial de conversación almacenado en la sesión.
- Las instrucciones internas del sistema no deben exponerse al usuario.
- Las herramientas de function calling no se utilizan en este backend.

## Publicar el proyecto en GitHub

### 1. Crear el repositorio

En GitHub crea un repositorio nuevo, por ejemplo:

```text
agora-sexual
```

Para este flujo, es conveniente crear el repositorio vacío y no generar otro README, `.gitignore` o licencia desde GitHub, ya que esos archivos se añadirán desde tu proyecto local.

### 2. Inicializar Git localmente

Abre una terminal dentro de la carpeta del proyecto:

```bash
cd C:\Users\diego\OneDrive\Documentos\agorasexual
```

Inicializa Git:

```bash
git init
```

### 3. Comprobar qué archivos serán subidos

```bash
git status
```

Antes de continuar, verifica especialmente que **`.env` no aparezca entre los archivos que Git va a incluir**.

### 4. Crear el primer commit

```bash
git add .
git commit -m "Primer commit - proyecto Agora Sexual"
```

### 5. Conectar el repositorio local con GitHub

Copia la URL de tu repositorio de GitHub y ejecuta:

```bash
git remote add origin https://github.com/TU_USUARIO/agora-sexual.git
```

Comprueba que quedó configurado:

```bash
git remote -v
```

### 6. Subir el proyecto

```bash
git branch -M main
git push -u origin main
```

Después de completar el `push`, actualiza la página del repositorio en GitHub y podrás ver los archivos del proyecto.

## Actualizar el proyecto después

Cuando hagas cambios en el código:

```bash
git status
git add .
git commit -m "Descripción de los cambios"
git push
```

Ejemplo:

```bash
git add .
git commit -m "Mejora del chatbot y manejo de errores"
git push
```

## Buenas prácticas

No subas nunca:

```text
.env
venv/
.venv/
__pycache__/
*.pyc
```

Tampoco publiques directamente claves de API, contraseñas, tokens o credenciales.

Si una clave privada fue subida accidentalmente a un repositorio, no basta con borrar el archivo en un commit posterior: la credencial debe considerarse expuesta y debe revocarse o rotarse.

## Estado del proyecto

Proyecto educativo y de desarrollo para la implementación de un asistente conversacional de orientación sobre educación sexual y salud sexual y reproductiva.

## Autor

Diego Alejandro Arias Vargas

## Licencia

Este proyecto puede incluir una licencia propia según las condiciones definidas por el autor o la institución responsable.
