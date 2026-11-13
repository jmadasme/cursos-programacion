# Datasheet · Cursos de Programación (Java y Lenguaje C)

**Repositorio:** `cursos-programacion`
**Versión documentada:** 1.0 (importación)
**Fecha de documentación:** 2026-11-12
**Licencia:** MIT · `Copyright (c) 2026 jmadasme`
**Estado:** material didáctico archivado; no es un producto de software en producción

---

## 1. Ficha técnica

| Campo | Valor |
|---|---|
| Nombre | Cursos de Programación · Java y Lenguaje C |
| Tipo | Archivo documentado de material de curso |
| Autores | jmadasme (material original); documentación del repositorio |
| Idiomas | Español (documentación y comentarios); código en Java y C |
| Cursos incluidos | 2 |
| Versiones | 2 carpetas inmutables en `versions/` |
| Formato de distribución | ZIP + Markdown |
| Tamaño total de los ZIP | 1.292.626 bytes (≈1,23 MiB) |
| Contenido descomprimido | 1.402.942 bytes (≈1,34 MiB) |
| Archivos de código | 44 `.java`, 129 `.txt` con C, 2 `.h` |
| Documentos | 6 `.doc` (Word 97-2003) |
| Recursos | 1 GIF (tabla ASCII) |
| Tests | No incluidos |
| Build system | Maven en Java (19 proyectos); ninguno en C |
| Dependencias externas | Ninguna declarada; solo JDK/Maven y compilador C |
| Integridad | SHA-256 documentado; `testzip()` sin errores |

### 1.1. Resumen ejecutivo

Este repositorio conserva dos cursos de programación en su formato original. El curso de Java cubre 19 módulos, desde la instalación del JDK hasta el diseño de un sistema de ventas con clases, arreglos y composición. El curso de Lenguaje C reúne 129 laboratorios sobre fundamentos, control de flujo, funciones, arreglos, cadenas, punteros y estructuras, con estilo C89/Turbo C.

El material es **didáctico y histórico**. No está pensado para producción, no incluye tests y algunas prácticas dependen de cabeceras de DOS o de archivos ausentes. La documentación describe el contenido real, los requisitos y las adaptaciones necesarias para usarlo en entornos modernos.

---

## 2. Versiones y procedencia

| Versión | Carpeta | ZIP | Origen declarado | Estado |
|---|---|---|---|---|
| Curso-Java 1.0 | `versions/Curso-Java/` | `CursoJava.zip` | `jmadasme/Curso-Java` | Importada; contenido original |
| Curso-Lenguaje-C-100-Hras 1.0 | `versions/Curso-Lenguaje-C-100-Hras/` | `Laboratorio Curso Lenguaje C.zip` | `jmadasme/Curso-Lenguaje-C-100-Hras` | Importada; contenido original |

Cada carpeta contiene:

- `README.md`: presentación original del curso.
- `VERSION.md`: ficha de importación, origen y advertencias.
- El ZIP con el material.

Los `VERSION.md` indican que se excluyeron credenciales, bases de datos y artefactos de ejecución. La inspección no encontró `.env`, `.key`, `.pem`, keystores ni cadenas de conexión. Los ZIP **no se modifican**; cualquier adaptación se hace sobre una copia extraída.

### 2.1. Cambios respecto de la importación

No hay cambios de contenido. La única intervención es documental: se agregaron `README.md`, `LICENSE`, `docs/` y los tres SVG. Los hashes permiten demostrar que los ZIP siguen intactos.

---

## 3. Inventario del curso de Java

### 3.1. Métricas

| Métrica | Valor |
|---|---:|
| Entradas del ZIP | 476 |
| Directorios | 313 |
| Archivos | 163 |
| `.java` | 44 |
| `.class` | 47 |
| `.xml` (poms) | 20 |
| `.lst` (Maven) | 40 |
| `.doc` | 6 |
| Sin extensión (`.netbeans_automatic_build`) | 6 |
| Módulos | 19 |
| Proyectos Maven efectivos | 19 |
| Bytes sin comprimir | 1.317.620 |
| Bytes del ZIP | 1.216.365 |
| Rango de fechas | 2019-09-19 a 2022-10-22 |

El ZIP apenas reduce tamaño (≈92 %) porque contiene `.class` y metadatos ya poco compresibles. Los `.java` suman 29.374 bytes; la mayor parte del peso son documentos `.doc` y artefactos de compilación.

### 3.2. Módulos

| # | Carpeta | Tema | `.java` | Proyecto |
|---|---|---|---:|---|
| 1 | `1.- Instalacion` | JDK, Java 14, Apache/NetBeans, entorno, hola mundo | 0 | 6 `.doc` |
| 2 | `2.- java clases` | Clases y objetos | 4 | Sin Maven |
| 3 | `3.- java contructores` | Constructores | 7 | 3 proyectos Maven |
| 4 | `4.- Paso por valor` | Paso por valor | 1 | Maven |
| 5 | `5.- Paso por Referencia` | Paso por referencia | 2 | Maven |
| 6 | `6.- Return usando Tipos Primitivos y palabra void` | `return` y `void` | 1 | Maven |
| 7 | `7.- Return usando Tipos Object` | Retorno de objetos | 1 | Maven |
| 8 | `8.- Uso de la palabra this en Java` | `this` | 1 | Maven |
| 9 | `9.- Uso de la palabra null en Java` | `null` | 1 | Maven |
| 10 | `10.- PruebaEncapsulamiento` | Encapsulamiento; copias `(1)` | 4 | Maven |
| 11 | `11.- EjemploEstatico` | `static` | 1 | Maven |
| 12 | `12.- Herencia` | Herencia | 4 | Maven |
| 13 | `13.- SobrecargaContructores` | Constructores sobrecargados | 3 | Maven |
| 14 | `14-. SobrecargaMetodos` | Métodos sobrecargados | 2 | Maven |
| 15 | `15.- Paquetes` | Paquetes e `import` | 2 | Maven |
| 16 | `16.- PalabraFinal` | `final` | 3 | Maven |
| 17 | `17.- Arreglos` | Arreglos de objetos | 2 | Maven |
| 18 | `18.- EjemploMatrices` | Matrices | 2 | Maven |
| 19 | `19.- DiseñoClases` | Producto, Orden, Ventas | 3 | Maven |

### 3.3. Compatibilidad Java

| Elemento | Valor observado |
|---|---|
| `maven.compiler.source` / `target` | 12 y 14 (según el pom) |
| *Major version* de los `.class` incluidos | 57 (Java 13) |
| `groupId` predominante | `cl.com.gm` |
| Paquete del módulo 19 | `com.jm.ventas` |
| Dependencias externas | Ninguna |
| Tests | Carpetas presentes, vacías |
| Codificación de fuentes | UTF-8 (44/44) |
| IDE inferido | Apache NetBeans (`.netbeans_automatic_build`) |

**Recomendación:** JDK 14 o superior para reproducir el curso; JDK 17/21 LTS para uso actual. Si se ejecutan los `.class` incluidos con un JRE anterior a 13, aparece `UnsupportedClassVersionError`; la solución es recompilar las fuentes.

### 3.4. Documentos de instalación

Los seis `.doc` del módulo 1 son binarios de Word 97-2003. No se previsualizan en GitHub. Los títulos y tamaños son:

| Archivo | Tamaño |
|---|---:|
| `1.- Instalando JDK.doc` | 113 KB |
| `2.- Instalando java 14.doc` | 43 KB |
| `3.- Instalando apache.doc` | 139 KB |
| `4.- Configurando apache y hola mundo.doc` | 462 KB |
| `Entorno.doc` | 18 KB |
| `ProyectoHolaMundo.doc` | 439 KB |

Por el contexto y los artefactos `.netbeans_automatic_build`, “apache” se refiere a Apache NetBeans. Los documentos describen el procedimiento, pero no incluyen instaladores.

---

## 4. Inventario del curso de C

### 4.1. Métricas

| Métrica | Valor |
|---|---:|
| Entradas del ZIP | 133 |
| Directorios | 1 |
| Archivos | 132 |
| `.txt` con código C | 129 |
| `.h` | 2 (`chprint.h`, `datadd.h`) |
| `.gif` | 1 (`ascii1.gif`, GIF87a, 22.660 bytes) |
| Archivos numéricos | 34 |
| Archivos con nombre mnemónico | 95 |
| Bytes sin comprimir | 85.322 |
| Bytes del ZIP | 76.261 |
| Rango de fechas | 2005-04-26 a 2022-10-22 |

### 4.2. Bloques temáticos

| Bloque | Tema | Ejemplos |
|---|---|---|
| 1 | Variables, tipos, expresiones | `0.txt`–`23.txt`, `alpha`, `asigd`, `cdig` |
| 2 | Control de flujo | `11.txt`, `may30`, `num30`, `cnumpar`, `vocal`, `goto` |
| 3 | Funciones, alcance, recursión | `23.txt`, `alcancev`, `RECUR`, `fac`, `sumfc` |
| 4 | Arreglos, orden, búsqueda | `arrayf`, `arraym`, `burbuja`, `sacudida`, `seleccio`, `insercio`, `secuenci` |
| 5 | Cadenas | `strcat`, `strcpy`, `strlen`, `strstr`, `strtok`, `strupr`, `string*` |
| 6 | Punteros | `ptsimple`, `ptcambio`, `ptoarray`, `ptofunc*`, `ptfuncio`, `159`–`254` |
| 7 | Estructuras | `struc1`–`struc11`, `proveedo`, `tarea` |
| 8 | Varios | `enum`, `clase`, `diag`, `hora`, `lim`, `pnc`, `ascii1.gif` |

### 4.3. Compatibilidad C

| Elemento | Valor observado |
|---|---|
| Estilo | C89 / Turbo C / DOS |
| `main()` sin tipo de retorno | 93 archivos |
| `void main()` | 8 archivos |
| `gets()` | 11 archivos |
| `#include <conio.h>` | 5 archivos |
| `#include <dos.h>` | 5 archivos |
| `#include <stdio.h>` | 128 de 129 |
| Codificación no UTF-8 | 14 archivos (Latin-1/CP850) |
| Cabeceras ausentes | `reparar.h` (en `ptofunc.txt`), `subs.h` (en `250.txt`) |

**Recomendación:** compilar con `-std=gnu89` para el material histórico; modernizar a `-std=c17` solo después de corregir `main`, `gets`, `conio.h` y `dos.h`.

---

## 5. Requisitos

### 5.1. Comunes

- Sistema operativo Linux, macOS o Windows con terminal (WSL, MSYS2 o Git Bash en Windows).
- 10 MB libres para los ZIP; 50–100 MB si se extraen y compilan todos los proyectos.
- `unzip`, Expand-Archive o Python 3.
- Editor de texto o IDE.
- Lector de `.doc`: LibreOffice Writer, Word, Google Docs, `antiword` o `catdoc`.

### 5.2. Java

| Herramienta | Versión mínima | Versión recomendada |
|---|---|---|
| JDK | 14 | 17 o 21 LTS |
| Maven | 3.6 | 3.9+ |
| IDE | Cualquiera con soporte Java | NetBeans, IntelliJ IDEA, Eclipse o VS Code |

### 5.3. C

| Herramienta | Versión mínima | Versión recomendada |
|---|---|---|
| GCC | 9 | 12+ |
| Clang | 10 | 15+ |
| `make` | Opcional | 4.x |
| `valgrind` / ASan | Opcional | Para prácticas de memoria |

### 5.4. Dependencias del repositorio

El repositorio **no tiene `requirements.txt`** ni ningún otro manifiesto de dependencias. No requiere Python, Node.js, pip ni npm para leerse o navegarse. Las únicas dependencias aparecen al compilar los ejemplos: JDK/Maven para Java y un compilador C para los laboratorios. Si se usa el script de inspección de `docs/developer.md`, solo se necesita Python 3 con la biblioteca estándar (`zipfile`, `hashlib`, `pathlib`).

---

## 6. Instalación y puesta en marcha

### 6.1. Descargar y verificar

```bash
sha256sum versions/Curso-Java/CursoJava.zip
sha256sum "versions/Curso-Lenguaje-C-100-Hras/Laboratorio Curso Lenguaje C.zip"
```

Valores esperados:

| Archivo | SHA-256 |
|---|---|
| `CursoJava.zip` | `c68393c0f78e368b3c3f8be0defac964c438584235584ba2043fb87bc1d2aa14` |
| `Laboratorio Curso Lenguaje C.zip` | `76c67e37ffa5f4f6aa1110eabc85fe73c2f3cbacf06f5f16799d535a191686e8` |

### 6.2. Extraer

```bash
mkdir -p ~/cursos/java ~/cursos/c

unzip -q "versions/Curso-Java/CursoJava.zip" -d ~/cursos/java
unzip -q "versions/Curso-Lenguaje-C-100-Hras/Laboratorio Curso Lenguaje C.zip" -d ~/cursos/c
```

Alternativa sin `unzip`:

```bash
python3 -m zipfile -e versions/Curso-Java/CursoJava.zip ~/cursos/java
python3 -m zipfile -e "versions/Curso-Lenguaje-C-100-Hras/Laboratorio Curso Lenguaje C.zip" ~/cursos/c
```

No extraigas dentro de `versions/`: rompe la separación entre archivo y material de trabajo y llena el repositorio de `target/`.

### 6.3. Primera ejecución Java

```bash
cd ~/cursos/java/cursojava/"2.- java clases"/ProyectoAritmetica
javac Aritmetica.java PruebaAritmetica.java
java PruebaAritmetica
# resultado = 8
```

### 6.4. Primera ejecución C

```bash
mkdir -p ~/cursos/c-build && cd ~/cursos/c-build
cp ~/cursos/c/"Laboratorio Curso Lenguaje C"/0.txt ./00-variables.c
gcc -std=gnu89 -Wall -Wextra 00-variables.c -o 00-variables
./00-variables
# El resultado de la operacion es 9
```

---

## 7. Modo de uso

### 7.1. Java con Maven

```bash
cd ~/cursos/java/cursojava/"12.- Herencia"
mvn -q clean compile
java -cp target/classes EjemploHerencia
```

Si el JDK es más nuevo que el `source`/`target` del pom:

```bash
mvn -q clean compile -Dmaven.compiler.source=17 -Dmaven.compiler.target=17
```

### 7.2. Java sin Maven

```bash
cd ~/cursos/java/cursojava/"19.- DiseñoClases"/DisenoClases
mkdir -p out
javac -d out $(find src/main/java -name "*.java")
java -cp out Ventas.Ventas
```

### 7.3. C

```bash
# Un archivo .txt como C
gcc -x c -std=gnu89 0.txt -o 00-variables
./00-variables

# Un archivo con cabeceras locales
gcc -std=gnu89 -I. 248.txt -o 248
./248
```

### 7.4. Tabla de comandos frecuentes

| Objetivo | Comando |
|---|---|
| Listar un ZIP | `unzip -l archivo.zip` |
| Extraer con Python | `python3 -m zipfile -e archivo.zip destino/` |
| Ver un `.doc` | `antiword archivo.doc` |
| Convertir `.doc` a texto | `libreoffice --headless --convert-to txt archivo.doc` |
| Compilar Java simple | `javac A.java B.java && java B` |
| Compilar con Maven | `mvn -q clean compile` |
| Ejecutar clase con paquete | `java -cp target/classes paquete.Clase` |
| Compilar C histórico | `gcc -std=gnu89 archivo.c -o archivo` |
| Compilar C moderno | `gcc -std=c17 -Wall -Wextra -Wpedantic archivo.c -o archivo` |
| Detectar memoria | `gcc -g -fsanitize=address,undefined archivo.c -o archivo` |

---

## 8. Compatibilidad y rendimiento

| Aspecto | Java | C |
|---|---|---|
| Sistema | Multiplataforma (JVM) | Linux, macOS, Windows (con adaptaciones) |
| Arquitectura | Cualquiera con JDK | x86, ARM, RISC-V, etc. |
| RAM necesaria | 256 MB+ para Maven | < 16 MB para los laboratorios |
| Tiempo de compilación | Segundos por proyecto | < 1 s por archivo |
| Dependencia de red | Primera descarga de plugins Maven | Ninguna |
| Portabilidad del código | Alta | Baja en el material histórico (`conio.h`, `dos.h`, `gets`) |

Los proyectos Maven no tienen dependencias externas, por lo que la primera compilación solo descarga el plugin de compilador si no está en la caché local. Los laboratorios C no requieren bibliotecas de terceros; los que usan `conio.h`/`dos.h` necesitan edición.

---

## 9. Limitaciones conocidas

1. **Sin tests**: no hay JUnit, aserciones ni scripts de verificación. Las salidas se comprueban a mano.
2. **Documentos binarios**: los `.doc` no se leen en GitHub y dependen de un editor compatible.
3. **Artefactos incluidos**: `.class`, `.lst` y `target/` inflan el ZIP y pueden confundir; no son necesarios para estudiar.
4. **Duplicados**: el módulo 10 incluye copias `(1)` de `Persona` y `PruebaPersona`.
5. **Paquetes inconsistentes**: fuentes en `com.jm.ventas`, `target/` con `com/gm/ventas`.
6. **C histórico**: 93 `main()` sin tipo, 8 `void main`, 11 `gets`, 5 `conio.h`, 5 `dos.h`.
7. **Cabeceras ausentes**: `reparar.h` en `ptofunc.txt`; `subs.h` en `250.txt` (además, faltan las definiciones de `datadd1`/`datadd2`).
8. **Erratas**: `RECUR.txt` usa `num + 1` en lugar de `num % 2`; `struc11.txt` omite `<stdio.h>`.
9. **Codificación**: 14 `.txt` en Latin-1/CP850.
10. **Sin enunciados**: la mayoría de los laboratorios C son código, no una guía con preguntas y criterios.

---

## 10. Solución de problemas

| Problema | Causa | Solución |
|---|---|---|
| `UnsupportedClassVersionError` | `.class` de Java 13 con JRE anterior | Recompilar desde fuentes con JDK 14+ |
| `invalid target release: 14` | JDK anterior a 14 | Instalar JDK 14+ o sobrescribir `maven.compiler.*` |
| `Could not find or load main class` | `-cp` o paquete incorrecto | Usar `java -cp target/classes Ventas.Ventas` |
| `package com.jm.ventas does not exist` | Compilación parcial | `javac -d out $(find src/main/java -name "*.java")` |
| `conio.h: No such file` | Cabecera de Turbo C | Eliminar `#include` y llamadas asociadas |
| `undefined reference to gets` | `gets` retirada/no declarada | Reescribir con `fgets` |
| `reparar.h: No such file` | Cabecera inexistente | Eliminar el include; el prototipo está en el archivo |
| `subs.h: No such file` | Cabecera inexistente | Eliminar el include y escribir las funciones |
| `undefined reference to datadd1` | `250.txt` solo tiene prototipos | Implementar `datadd1`/`datadd2` |
| Acentos rotos | Latin-1/CP850 | `iconv -f CP850 -t UTF-8 archivo.txt > salida.txt` |
| `.doc` ilegible | Word 97-2003 | LibreOffice/Word, `antiword` o `catdoc` |
| Nombre `DiseÃ±o` | `unzip` sin UTF-8 | Usar `python3 -m zipfile -e` |
| `mvn: command not found` | Maven ausente | Usar `javac` o instalar Maven con autorización |

---

## 11. Glosario

| Término | Definición |
|---|---|
| **JDK** | Java Development Kit; compilador, JVM y herramientas |
| **JRE** | Java Runtime Environment; solo ejecución |
| **Maven** | Gestor de proyectos Java basado en `pom.xml` |
| **POM** | Project Object Model; configuración de un proyecto Maven |
| **POO** | Programación orientada a objetos |
| **Encapsulamiento** | Ocultar estado y exponer una interfaz controlada |
| **Herencia** | Extensión de una clase a partir de otra |
| **Composición** | Relación “tiene un” entre objetos |
| **`static`** | Miembro compartido por todas las instancias |
| **`final`** | Constante, método no sobrescribible o clase no heredable |
| **C89** | Estándar ANSI/ISO C de 1989/1990 |
| **Turbo C** | Compilador de Borland para DOS, muy usado en enseñanza |
| **`gets`** | Función insegura de lectura de cadenas, retirada de C11 |
| **Puntero** | Variable que almacena una dirección de memoria |
| **Struct** | Tipo compuesto con campos de distintos tipos |
| **Sanitizer** | Instrumentación del compilador para detectar errores en ejecución |

---

## 12. Control de cambios

| Versión | Fecha | Cambio |
|---|---|---|
| 1.0 | 2026-11-12 | Documentación inicial: README, datasheet, developer, REFERENCES, 3 SVG y LICENSE |

Los ZIP no se modificaron. Cualquier cambio futuro en el material debe registrarse como una nueva carpeta de versión, no como una edición del ZIP existente.

---

## 13. Soporte y contacto

Este es un archivo educativo sin soporte comercial. Para dudas sobre el contenido:

1. Consulta el [README](../README.md) y la [guía de desarrollador](developer.md).
2. Revisa las [referencias](REFERENCES.md) para Java, C y herramientas.
3. Abre un issue en el repositorio con la ruta exacta del archivo, el comando ejecutado y el mensaje de error.

No se garantiza soporte para versiones descatalogadas (Java 12/14, NetBeans 2020, Turbo C) ni para adaptaciones de terceros.
