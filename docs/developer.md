# Guía de desarrollador · Cursos de Programación

Esta guía explica cómo está organizado el repositorio, cómo inspeccionarlo sin extraer los ZIP, cómo agregar una versión y cómo mantener la documentación y los recursos gráficos.

**Público:** mantenedores del repositorio, docentes que quieran adaptar el material y revisores técnicos.
**Alcance:** estructura, convenciones, validación y deuda técnica conocida.
**Licencia:** MIT · `Copyright (c) 2026 jmadasme`.

---

## 1. Arquitectura del repositorio

El repositorio es un **archivo estático** con tres capas:

```text
cursos-programacion/
├── README.md            # capa de presentación
├── LICENSE              # capa legal
├── docs/                # capa documental
│   ├── datasheet.md
│   ├── developer.md
│   ├── REFERENCES.md
│   └── assets/*.svg
└── versions/            # capa de material original
    ├── Curso-Java/
    │   ├── CursoJava.zip
    │   ├── README.md
    │   └── VERSION.md
    └── Curso-Lenguaje-C-100-Hras/
        ├── Laboratorio Curso Lenguaje C.zip
        ├── README.md
        └── VERSION.md
```

### 1.1. Principios de diseño

1. **Inmutabilidad del material.** Los ZIP son la fuente de verdad y no se editan. Toda adaptación se hace en una copia extraída fuera del repositorio.
2. **Separación de capas.** `versions/` conserva el material; `docs/` lo describe; el `README.md` lo presenta. Ninguna capa replica el contenido de otra.
3. **Inspección sin extracción.** La documentación se basa en `zipfile`, no en copias de trabajo. Así se evita contaminar el repositorio con `target/`, `.class` o duplicados.
4. **Trazabilidad.** Cada ZIP tiene hash SHA-256, ficha de versión y origen declarado.
5. **Documentación en Markdown.** Se lee en GitHub, en un editor y en cualquier visor de texto. No se genera `docs/index.html` ni un sitio estático.
6. **Paleta única.** Los SVG usan los mismos tokens de color para que la documentación se vea coherente.

### 1.2. Por qué no hay código ejecutable

El repositorio no tiene un `src/` propio ni un `pom.xml` raíz. El código vive dentro de los ZIP, y el repositorio solo lo describe. Esa decisión evita:

- duplicar el material y crear dos fuentes de verdad;
- incluir artefactos de compilación en el control de versiones;
- que un cambio accidental en una copia extraída se confunda con el original.

Si se quiere ejecutar el material, se extrae en `~/cursos/` o `/tmp/cursos/`, se compila allí y se documenta cualquier parche en un issue o en una nueva versión.

---

## 2. Modelo de datos

### 2.1. Carpeta de versión

Cada carpeta de `versions/` representa una **versión inmutable** de un curso. Su nombre coincide con el del repositorio de origen y contiene:

| Archivo | Obligatorio | Propósito |
|---|---|---|
| `*.zip` | Sí | Material original |
| `README.md` | Sí | Presentación heredada del curso |
| `VERSION.md` | Sí | Ficha de importación y advertencias |

No se permiten archivos sueltos de código, credenciales, bases de datos ni artefactos de ejecución.

### 2.2. `VERSION.md`

Debe incluir, como mínimo:

- nombre del curso;
- repositorio de origen;
- formato de importación (ZIP + README);
- advertencia sobre credenciales y artefactos excluidos;
- fecha o referencia de importación, si se conoce.

Plantilla:

```markdown
# Nombre-del-Curso

Versión importada desde `usuario/repositorio`.

Descripción breve del contenido y del formato.

Esta carpeta conserva el contenido original de la versión. Las credenciales,
bases de datos y artefactos de ejecución se excluyeron del portfolio; usá los
archivos `.example` cuando existan.
```

### 2.3. Convención de nombres

- Carpetas de versión: el nombre del repositorio de origen, con guiones (`Curso-Java`, `Curso-Lenguaje-C-100-Hras`).
- ZIP: nombre descriptivo, con espacios solo si el origen los tenía (`Laboratorio Curso Lenguaje C.zip`).
- Documentos: `README.md`, `VERSION.md`, `datasheet.md`, `developer.md`, `REFERENCES.md`.
- Assets: `NN-nombre-en-kebab-case.svg` (`01-arquitectura.svg`).

No se renombran los ZIP: el nombre forma parte de la trazabilidad y aparece en los comandos de la documentación.

---

## 3. Inspección con `zipfile`

La herramienta de referencia es la biblioteca estándar de Python. No requiere instalación y respeta la bandera UTF-8 del ZIP.

### 3.1. Inventario básico

```python
import zipfile
from pathlib import Path

def inventario(path: str) -> dict:
    with zipfile.ZipFile(path) as z:
        infos = z.infolist()
        files = [i for i in infos if not i.is_dir()]
        return {
            "entradas": len(infos),
            "directorios": len(infos) - len(files),
            "archivos": len(files),
            "sin_comprimir": sum(i.file_size for i in infos),
            "comprimido": sum(i.compress_size for i in infos),
            "integro": z.testzip() is None,
        }

for p in Path("versions").rglob("*.zip"):
    print(p.name, inventario(p))
```

### 3.2. Conteo por extensión

```python
import collections, os, zipfile

with zipfile.ZipFile("versions/Curso-Java/CursoJava.zip") as z:
    ext = collections.Counter(
        os.path.splitext(i.filename)[1].lower()
        for i in z.infolist() if not i.is_dir()
    )
print(ext.most_common())
```

### 3.3. Lectura de una fuente sin extraer

```python
import zipfile

with zipfile.ZipFile("versions/Curso-Java/CursoJava.zip") as z:
    print(z.read("cursojava/2.- java clases/ProyectoAritmetica/Aritmetica.java").decode("utf-8"))
```

Para archivos C con codificación mixta:

```python
with zipfile.ZipFile("versions/Curso-Lenguaje-C-100-Hras/Laboratorio Curso Lenguaje C.zip") as z:
    data = z.read("Laboratorio Curso Lenguaje C/0.txt")
    print(data.decode("latin-1"))
```

### 3.4. Hash

```python
import hashlib
from pathlib import Path

for p in Path("versions").rglob("*.zip"):
    print(p.name, hashlib.sha256(p.read_bytes()).hexdigest())
```

### 3.5. Reglas de inspección

- No escribir dentro de `versions/`.
- No extraer para contar: `zipfile` basta.
- No confiar en la extensión: los `.txt` del curso de C son código C.
- No asumir UTF-8: 14 archivos C son Latin-1/CP850.
- No ejecutar `.class` incluidos: compilar desde fuentes.

---

## 4. Cómo agregar una versión

### Paso 1: crear la carpeta

```bash
mkdir -p versions/Nombre-Del-Curso
```

### Paso 2: copiar el material original

Copia el ZIP sin modificarlo y el README heredado. Si no hay README, crea uno breve que describa el curso y su origen.

### Paso 3: escribir `VERSION.md`

Usa la plantilla de la sección 2.2 e indica el repositorio de origen. Si el material se importó desde GitHub, conserva la URL y la fecha.

### Paso 4: calcular hash y métricas

```bash
sha256sum versions/Nombre-Del-Curso/*.zip
python3 - <<'PY'
import zipfile
from pathlib import Path
p = next(Path("versions/Nombre-Del-Curso").glob("*.zip"))
with zipfile.ZipFile(p) as z:
    print(p.name, len(z.infolist()), z.testzip())
PY
```

### Paso 5: actualizar la documentación

| Documento | Qué actualizar |
|---|---|
| `README.md` | Tabla de vista rápida, mapa, cursos, verificación y plan si aplica |
| `docs/datasheet.md` | Ficha técnica, inventario, requisitos y compatibilidad |
| `docs/developer.md` | Esta guía, si cambia la arquitectura o la convención |
| `docs/REFERENCES.md` | Fuente de origen y referencias nuevas |

### Paso 6: validar

Ejecuta el checklist de la sección 5 y revisa que los enlaces relativos funcionen.

---

## 5. Checklist de validación

Antes de publicar un cambio:

- [ ] Los ZIP existen y `ZipFile.testzip()` devuelve `None`.
- [ ] Los hashes del README y del datasheet coinciden con `sha256sum`.
- [ ] No se agregaron `.env`, `.key`, `.pem`, keystores, bases de datos ni credenciales.
- [ ] No se agregó `docs/index.html`.
- [ ] No se modificó ningún ZIP ni se extrajo material dentro de `versions/`.
- [ ] Los conteos de archivos y extensiones coinciden con la realidad.
- [ ] Los enlaces Markdown a `docs/` y `versions/` resuelven.
- [ ] Los SVG son XML válido y tienen `<title>` y `<desc>`.
- [ ] La paleta se mantiene: `#06141b`, `#2A9D8F`, `#457B9D`, `#5B7C99`.
- [ ] El README sigue en el rango de 25.000–40.000 caracteres.
- [ ] Las afirmaciones sobre compilación están marcadas como análisis estático si no se ejecutó el código.

### 5.1. Validación de SVG

Sin instalar herramientas, se puede comprobar que un SVG es XML válido con Python:

```python
import xml.etree.ElementTree as ET
for f in ["docs/assets/01-arquitectura.svg",
          "docs/assets/02-ruta-java.svg",
          "docs/assets/03-ruta-c.svg"]:
    ET.parse(f)
    print("OK", f)
```

Para revisar que no haya verdes neón, busca códigos como `#39FF14`, `#00FF00` o `lime`:

```bash
grep -RniE "#(39ff14|00ff00)|lime" docs/assets || echo "sin verdes neón"
```

---

## 6. Convenciones de documentación

### 6.1. Tono

- Español neutro, directo, sin marketing.
- Explicar los límites con honestidad: es material de curso, no un producto.
- No prometer que el código compila si no se verificó.
- Distinguir siempre “observado en el ZIP” de “recomendación”.

### 6.2. Estructura

- `README.md`: presentación, contenido, requisitos, uso, ejemplos, límites, licencia.
- `datasheet.md`: ficha técnica, inventario, instalación, compatibilidad, soporte.
- `developer.md`: arquitectura, mantenimiento, validación, deuda técnica.
- `REFERENCES.md`: estándares, documentación oficial, bibliografía.

### 6.3. Enlaces

Usa rutas relativas:

```markdown
[datasheet](docs/datasheet.md)
[references](REFERENCES.md)
![Arquitectura](docs/assets/01-arquitectura.svg)
```

No uses enlaces absolutos a `file://` ni a rutas personales.

### 6.4. Tablas

Prefiere tablas para inventarios, requisitos y comparaciones. Evita tablas de más de seis columnas: se vuelven ilegibles en móvil. Si el contenido es narrativo, usa párrafos y listas.

---

## 7. Recursos gráficos

### 7.1. Paleta

| Token | Hex | Uso |
|---|---|---|
| Fondo | `#06141b` | Lienzo de los SVG |
| Acento | `#2A9D8F` | Elementos destacados, rutas principales |
| Azul medio | `#457B9D` | Tarjetas y bloques secundarios |
| Azul grisáceo | `#5B7C99` | Conectores, texto secundario |
| Texto | `#D7E3E8` | Texto principal |
| Texto tenue | `#8FA6B2` | Etiquetas y pies |

No se usa verde neón. El acento `#2A9D8F` es un verde azulado sobrio, no un neón.

### 7.2. Estructura de un SVG

```xml
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1200 720" width="1200" height="720" role="img" aria-labelledby="titulo desc">
  <title id="titulo">Título del diagrama</title>
  <desc id="desc">Descripción para lectores de pantalla.</desc>
  <!-- fondo, tarjetas, conectores, texto -->
</svg>
```

### 7.3. Reglas

- `viewBox` explícito y dimensiones en píxeles.
- Texto con `font-family="Inter, 'Segoe UI', system-ui, sans-serif"`.
- Contraste mínimo 4.5:1 para texto normal.
- No usar imágenes rasterizadas embebidas.
- No usar animaciones ni scripts.
- Mantener los nombres `01-`, `02-`, `03-` para ordenar.

---

## 8. Deuda técnica y análisis del material

### 8.1. Curso de Java

**Fortalezas**

- Progresión clara de 19 módulos.
- Proyectos Maven pequeños y fáciles de importar.
- Ejemplos de encapsulamiento, herencia, `static`, `final` y composición.
- Código legible y comentado en español.

**Deuda**

| Problema | Impacto | Acción sugerida |
|---|---|---|
| `.doc` binarios | No se leen en GitHub | Convertir a Markdown/PDF en una versión nueva |
| Sin tests | No hay verificación automática | Agregar JUnit en una adaptación, no en el ZIP |
| `target/` incluido | Peso y confusión | Ignorar en la copia; no borrar del ZIP |
| Copias `(1)` | Duplicados | Excluir al compilar; documentar |
| `com/gm` vs `com/jm` | `target/` obsoleto | Recompilar desde fuentes |
| Java 12/14 | Descatalogado | Migrar a LTS en una adaptación |
| Sin colecciones | Alcance limitado | Agregar un módulo nuevo, no editar el existente |

### 8.2. Curso de C

**Fortalezas**

- Cobertura amplia de fundamentos, punteros y estructuras.
- Ejemplos breves, probados en clase, con comentarios.
- Casos integradores (`tarea.txt`, `proveedo.txt`) que combinan varios temas.

**Deuda**

| Problema | Impacto | Acción sugerida |
|---|---|---|
| Estilo Turbo C | No compila en Linux/macOS sin edición | Guía de portabilidad en README/datasheet |
| `gets` | Insegura | Reemplazar por `fgets` en adaptaciones |
| `conio.h`/`dos.h` | No portables | Eliminar o aislar con macros |
| Cabeceras ausentes | `ptofunc.txt`, `250.txt` no compilan | Documentar y corregir en copia |
| Erratas | `RECUR.txt`, `struc11.txt` | Corregir en adaptación, mantener original |
| Codificación mixta | Acentos rotos | Convertir con `iconv` |
| Nombres 8.3 | Poco descriptivos | Mapear en un índice si se reutiliza |
| Sin build system | Compilación manual | Agregar Makefile en una adaptación |

### 8.3. Criterio de intervención

No se corrige el material original. Si un docente necesita una versión arreglada:

1. crea una carpeta nueva (`versions/Curso-C-Modernizado/`) con su propio ZIP y `VERSION.md`;
2. documenta los cambios respecto del original;
3. mantiene el original accesible para comparar.

Ese enfoque preserva la trazabilidad y evita que una corrección silenciosa se confunda con el material histórico.

---

## 9. Extensión: generar una guía de laboratorio

Una extensión útil es convertir los 129 `.txt` en una guía con enunciados. Un flujo posible:

1. **Inventariar** nombres, tamaño y primeras líneas.
2. **Clasificar** por bloque temático (ver datasheet).
3. **Extraer** el código a Markdown con bloques ` ```c `.
4. **Escribir** un objetivo, una entrada de ejemplo y una salida esperada por laboratorio.
5. **Validar** que cada ejemplo compile con `gcc -std=gnu89`.
6. **Publicar** la guía en `docs/` sin modificar los ZIP.

No automatices la extracción sin revisar: muchos archivos tienen erratas o dependencias de DOS.

---

## 10. Publicación y control de versiones

- El repositorio no incluye `docs/index.html`; no agregues generadores de sitio sin discutirlo.
- No subas los ZIP extraídos ni binarios compilados.
- No subas credenciales, rutas personales ni datos de alumnos.
- Si el repositorio se publica en GitHub, los `.doc` se descargan, pero no se previsualizan; indícalo en el README.
- Los SVG se renderizan en GitHub si son XML válido y no usan recursos externos.

### 10.1. Mensajes de commit sugeridos

```text
docs: agrega datasheet del curso de Java
docs: corrige conteo de archivos del ZIP de C
assets: agrega diagrama de ruta de C
chore: actualiza hash tras reimportar versión
```

### 10.2. Versionado

Usa versiones de carpeta (`1.0`, `1.1`) solo si cambia el material. Los cambios de documentación no requieren una nueva carpeta de versión; se registran en el historial del repositorio.

---

## 11. Preguntas frecuentes del mantenedor

**¿Puedo borrar los `.class` del ZIP?**
No. El ZIP es inmutable. Puedes borrarlos en la copia extraída; el original se conserva.

**¿Puedo convertir los `.doc` a Markdown?**
Sí, en una versión nueva. Documenta la conversión y conserva el `.doc` original.

**¿Dónde pongo un `Makefile` para C?**
En una adaptación fuera de `versions/` o en una nueva carpeta de versión. No dentro del ZIP original.

**¿Cómo verifico que no cambié un ZIP?**
Compara el SHA-256 con el documentado. Si cambió, restaura el original.

**¿Los SVG necesitan fuentes externas?**
No. Usan una pila de fuentes del sistema; no cargan webfonts.

**¿Por qué no hay `requirements.txt`?**
Porque no hay código Python en el repositorio. El único Python es opcional, para inspeccionar los ZIP con la biblioteca estándar.

---

## 12. Referencias internas

- [README](../README.md) — presentación y uso.
- [Datasheet](datasheet.md) — ficha técnica e inventario.
- [REFERENCES](REFERENCES.md) — estándares y bibliografía.
- [LICENSE](../LICENSE) — texto de la licencia MIT.

Para detalles de Java, C y herramientas, consulta `REFERENCES.md`. Para el inventario exacto, consulta el datasheet; para la narrativa del curso, el README.
