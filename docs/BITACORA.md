# Cursos de Programación — Bitácora

Registro de decisiones, problemas y lecciones al convertir dos cursos históricos en un repositorio documentado y publicable.

---

## 1. Punto de partida

El repositorio reúne dos cursos:

- **Curso-Java**: 19 módulos Maven, 44 archivos `.java`, documentos `.doc` y proyectos con `target/` incluido.
- **Curso-Lenguaje-C-100-Hras**: 129 programas en archivos `.txt`, dos cabeceras y una tabla ASCII en GIF.

Ambos llegaron como ZIP. El objetivo no fue modernizar el contenido, sino **preservarlo, explicarlo y hacerlo navegable**.

## 2. Decisiones

### Conservar los ZIP originales

Los ZIP se mantienen intactos dentro de `versions/` para que el material histórico no se altere. La documentación los inspecciona sin extraerlos en el repositorio.

**Consecuencia:** el visitante debe descargar y descomprimir para compilar. Es el precio de conservar la fidelidad.

### Inspeccionar con `zipfile`, no extrayendo

Se usó `zipfile` de Python para listar y leer entradas sin escribir miles de archivos en el árbol de trabajo.

**Ventaja:** no se contamina `versions/`, no se duplican binarios y se puede auditar el contenido.

### No convertir los `.txt` de C en `.c`

Los 129 programas de C son código real, pero están guardados como `.txt`. Se decidió no renombrarlos ni reescribirlos.

**Motivo:** el material original usa esa convención y cambiarla alteraría el curso. La documentación explica cómo compilarlos con `gcc -x c`.

### Markdown en lugar de un generador de sitio

La documentación base es Markdown y SVG. La landing `docs/index.html` la genera el builder del portfolio por separado.

**Motivo:** Markdown se lee en GitHub, en un editor y en cualquier visor; no añade dependencias.

## 3. Problemas encontrados

### `docs/index.html` preexistente

Al empezar la documentación ya existía una landing generada por el portfolio. El README decía que no había `index.html`.

**Corrección:** se reformularon las dos menciones para aclarar que la landing se genera aparte.

### Documentos `.doc` binarios

Los documentos de instalación de Java están en `.doc`, no en Markdown. No se pudieron convertir sin herramientas externas.

**Decisión:** se inventariaron y se explicó que son binarios heredados.

### `target/` dentro de los ZIP

Los proyectos Maven incluyen `target/` con clases compiladas y artefactos antiguos.

**Decisión:** no se limpian los ZIP; se advierte que ese contenido es residuo y no una entrega oficial.

### Duplicados en Java

Hay 44 `.java` para 19 módulos, con dos copias duplicadas.

**Decisión:** se documentan como parte del material; no se eliminan.

### Enlaces y credenciales

No se encontraron `.env`, tokens, correos ni cadenas de conexión en las fuentes revisadas.

**Decisión:** se mantiene la auditoría y se advierte que los ZIP no se han modificado.

## 4. Enfoques descartados

- **Extraer los ZIP en `versions/`:** duplicaría el contenido y haría el repo mucho más pesado.
- **Modernizar los proyectos Maven:** cambiaría el material didáctico y ocultaría su antigüedad.
- **Convertir los `.txt` a `.c`:** rompería la convención original.
- **Generar un sitio estático propio:** el portfolio ya genera una landing; duplicarla no aporta.
- **Duplicar la licencia dentro de cada ZIP:** no es necesario y complica el mantenimiento.

## 5. Lecciones

- Los `.txt` de C son código real; el visor y la extensión no cambian el contenido.
- Los `.doc` son binarios: no se pueden auditar como texto.
- `target/` infla los ZIP y confunde sobre el estado del proyecto.
- Preservar no es lo mismo que actualizar; documentar la antigüedad es parte del valor.
- Un README honesto evita que el visitante espere una plataforma de e-learning que no existe.

## 6. Deuda técnica

- Convertir los `.doc` a Markdown o PDF legible.
- Añadir un índice de los 129 programas de C por tema.
- Verificar que los 19 `pom.xml` compilan con JDK 14.
- Documentar las dos cabeceras faltantes del curso C.
- Evaluar si los `target/` deben excluirse en una futura copia saneada.

## 7. Licencia

MIT © 2026 jmadasme. Ver [`LICENSE`](../LICENSE).
