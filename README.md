# 📊 Instagram Followers Analyzer

Script en Python para analizar tus relaciones de seguimiento en Instagram a partir
de los datos exportados oficialmente por la plataforma. Identifica quiénes no te
siguen de vuelta, a quiénes no seguís de vuelta y qué solicitudes de seguimiento
tenés pendientes (perfiles privados que aún no te aceptaron).

## 🎯 ¿Qué hace?

A partir de los archivos JSON que Instagram te permite descargar, el script genera
tres análisis:

1. **No te siguen de vuelta** — cuentas que vos seguís pero que no te siguen a vos.
2. **No los seguís de vuelta** — cuentas que te siguen pero que vos no seguís.
3. **Solicitudes pendientes** — perfiles privados a los que enviaste una solicitud
   de seguimiento y todavía no la aceptaron, mostrando tanto el nombre de usuario
   como el nombre real del perfil.

Al final imprime un resumen con los totales de cada categoría.

## 📥 Cómo obtener los datos de Instagram

1. Abrí Instagram → **Configuración** → **Centro de cuentas** → **Tu información y permisos**.
2. Elegí **Descargar tu información**.
3. Seleccioná el formato **JSON** (importante, no HTML).
4. Una vez que Instagram te envíe el archivo, descomprimilo.
5. Vas a necesitar estos archivos:
   - `followers_1.json`
   - `following.json`
   - `pending_follow_requests.json`

## 🚀 Uso

### En Google Colab
1. Subí los archivos JSON al entorno (por defecto en `/content`).
2. Pegá y ejecutá el script.
3. Si subiste los archivos a otra carpeta, cambiá la variable `CARPETA` al inicio del código.

### En local
1. Colocá los archivos JSON en la misma carpeta que el script (o ajustá `CARPETA`).
2. Ejecutá:
```bash
   python instagram_analyzer.py
```

## ⚙️ Características técnicas

- **Detección automática de estructura**: maneja tanto archivos que son una lista
  directa de objetos como archivos que son un diccionario con la lista anidada
  (por ejemplo, `following.json` usa la clave `relationships_following`).
- **Corrección de codificación (mojibake)**: los nombres exportados por Instagram
  vienen con doble codificación, lo que produce caracteres ilegibles en emojis y
  acentos. El script los corrige con `encode('latin-1').decode('utf-8')`.
- **Manejo de errores robusto**: si falta algún archivo, avisa con un mensaje claro
  en lugar de detenerse con una excepción.
- **Salida ordenada**: todos los listados se imprimen ordenados alfabéticamente y
  con el enlace directo a cada perfil.

## 📋 Requisitos

- Python 3.x
- Solo usa módulos de la biblioteca estándar (`json`, `os`). No requiere instalar nada.

## 📂 Estructura esperada de los archivos

| Archivo                          | Estructura                                  | Contenido                          |
|----------------------------------|---------------------------------------------|------------------------------------|
| `followers_1.json`               | Lista de objetos con `string_list_data`     | Quiénes te siguen                  |
| `following.json`                 | Dict con clave `relationships_following`    | A quiénes seguís                   |
| `pending_follow_requests.json`   | Lista de objetos con `label_values`         | Solicitudes que enviaste pendientes|

## 🖥️ Ejemplo de salida

=======================================================
NO TE SIGUEN DE VUELTA  (3)
=======================================================
  - usuario_ejemplo1  → https://www.instagram.com/usuario_ejemplo1
  - usuario_ejemplo2  → https://www.instagram.com/usuario_ejemplo2
  - usuario_ejemplo3  → https://www.instagram.com/usuario_ejemplo3

=======================================================
RESUMEN
=======================================================
  Seguidores:            443
  Seguidos:              380
  No te siguen:          3

## ⚠️ Notas

- Los archivos son **privados**: no los subas a un repositorio público. Agregá un
  `.gitignore` para excluir los `.json`.
- Instagram puede cambiar el nombre o la estructura de los archivos en futuras
  exportaciones; si algo falla, revisá la estructura con un bloque de depuración.

## 📄 Licencia

MIT — usalo y modificalo libremente.
