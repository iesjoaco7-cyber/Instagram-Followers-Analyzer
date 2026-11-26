# 📊 Instagram Followers Analyzer

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/iesjoaco7-cyber/Instagram-Followers-Analyzer/blob/main/instagram_analyzer.ipynb)
[![Python 3.x](https://img.shields.io/badge/python-3.x-blue.svg)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)
[![Privacy: 100% local](https://img.shields.io/badge/privacy-100%25%20local-brightgreen.svg)](#-ventajas-frente-a-las-herramientas-web)

> **Descubrí quién no te sigue de vuelta en Instagram sin dar acceso a tu cuenta ni subir tus datos a ningún sitio externo.** Todo el análisis corre localmente en Python.

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

## 🧪 Probalo sin tus propios datos

El repositorio incluye una carpeta `ejemplos/` con archivos JSON ficticios que
replican la estructura real de Instagram. Podés ejecutar el script directamente
contra ellos para ver cómo funciona: cambiá la variable `CARPETA` a `'ejemplos'`
al inicio del código y ejecutá. No necesitás descargar nada de Instagram para probarlo.

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
1. Hacé click en el botón **Open in Colab** de arriba.
2. Subí los archivos JSON al entorno (por defecto en `/content`).
3. Ejecutá las celdas.
4. Si subiste los archivos a otra carpeta, cambiá la variable `CARPETA` al inicio del código.

### En local
1. Colocá los archivos JSON en la misma carpeta que el script (o ajustá `CARPETA`).
2. Ejecutá:
   ```bash
   python instagram_analyzer.py
   ```

## 📖 Cómo funciona

Este proyecto identifica qué usuarios de Instagram no corresponden tu seguimiento,
utilizando los datos oficiales que la plataforma permite exportar. A diferencia de
las herramientas web de terceros, todo el análisis se realiza **localmente con
Python**, de modo que tus datos personales nunca salen de tu entorno.

1. **Descarga de datos**: solicitás a Instagram tus listas de seguidores y seguidos en formato JSON.
2. **Carga local**: en lugar de subir tus datos a un sitio externo, los cargás directamente en Python (Colab o tu máquina).
3. **Procesamiento automático**: el código compara las listas, detecta la estructura de cada archivo y corrige la codificación de los nombres.
4. **Resultados**: imprime los tres listados ordenados alfabéticamente, cada uno con el enlace directo al perfil, más un resumen.

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

```
=======================================================
NO TE SIGUEN DE VUELTA  (2)
=======================================================
  - elena_nosigue  → https://www.instagram.com/elena_nosigue
  - fran_nosigue   → https://www.instagram.com/fran_nosigue

=======================================================
RESUMEN
=======================================================
  Seguidores:            443
  Seguidos:              380
  No te siguen:          2
```

## 🔒 Ventajas frente a las herramientas web

A diferencia de los sitios externos que requieren subir tu archivo y revisar los
resultados manualmente por posibles errores de lectura, este script:

- **Mantiene tus datos privados**: nunca abandonan tu computadora o tu sesión de Colab.
- **Es transparente**: podés ver y modificar exactamente cómo se procesa la información.
- **Ofrece más análisis**: no solo quién no te sigue, sino también a quién no seguís
  y tus solicitudes pendientes.
- **Maneja los errores de raíz**: la detección de estructura y la corrección de
  encoding evitan los fallos de lectura que obligan a verificar a mano.

## 🎥 Video tutorial

Hay un tutorial en video que muestra el proceso de descarga de datos:
[Ver en TikTok](https://www.tiktok.com/@etienterzzo/video/7579365375243029768)

## ⚠️ Notas

- Los archivos con tus datos reales son **privados**: el `.gitignore` ya está
  configurado para que nunca se suban por error. Solo los archivos de la carpeta
  `ejemplos/` (ficticios) se versionan.
- Instagram puede cambiar el nombre o la estructura de los archivos en futuras
  exportaciones; si algo falla, revisá la estructura con un bloque de depuración.

## 📄 Licencia

MIT — usalo y modificalo libremente.
