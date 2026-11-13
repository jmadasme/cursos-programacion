# Referencias · Cursos de Programación (Java y Lenguaje C)

**Última revisión:** 2026-11-12
**Alcance:** fuentes internas, estándares, documentación oficial de Java y C, herramientas de archivo y bibliografía de apoyo.

Las referencias externas se incluyen para que el lector pueda ampliar o verificar los conceptos del curso. No implican que el material haya sido validado contra la última versión de cada estándar: los ZIP son de 2005–2022 y se describen como material histórico.

---

## 1. Cómo citar este repositorio

```text
jmadasme. Cursos de Programación: Java y Lenguaje C. Repositorio de material
didáctico, versión 1.0, 2026. Licencia MIT.
```

Para citar un curso concreto:

```text
jmadasme. Curso de Java. Material de curso, 2019–2022.
Disponible en versions/Curso-Java/CursoJava.zip.

jmadasme. Curso de Lenguaje C · 100 horas. Laboratorio, 2005–2022.
Disponible en versions/Curso-Lenguaje-C-100-Hras/Laboratorio Curso Lenguaje C.zip.
```

Si se cita una adaptación, indica el cambio y la versión derivada; no atribuyas el original a otra persona.

---

## 2. Fuentes primarias internas

| Fuente | Ruta | Uso |
|---|---|---|
| Curso de Java (ZIP) | `versions/Curso-Java/CursoJava.zip` | 44 `.java`, 6 `.doc`, 19 proyectos Maven |
| Presentación Java | `versions/Curso-Java/README.md` | Descripción original del curso |
| Ficha Java | `versions/Curso-Java/VERSION.md` | Origen y advertencias de importación |
| Curso de C (ZIP) | `versions/Curso-Lenguaje-C-100-Hras/Laboratorio Curso Lenguaje C.zip` | 129 `.txt`, 2 `.h`, 1 GIF |
| Presentación C | `versions/Curso-Lenguaje-C-100-Hras/README.md` | Descripción original |
| Ficha C | `versions/Curso-Lenguaje-C-100-Hras/VERSION.md` | Origen y advertencias |
| Inventario técnico | `docs/datasheet.md` | Conteos, compatibilidad, límites |
| Guía de mantenimiento | `docs/developer.md` | Inspección, validación, extensión |

Los documentos internos se citan con rutas relativas para que funcionen en GitHub y en un clon local.

---

## 3. Java

### 3.1. Especificación y documentación oficial

| Referencia | URL | Para qué |
|---|---|---|
| Java Language Specification, SE 14 | https://docs.oracle.com/javase/specs/jls/se14/html/index.html | Sintaxis, tipos, clases, herencia, paquetes |
| Java SE 14 Documentation | https://docs.oracle.com/en/java/javase/14/ | API y guías de la versión que declara el curso |
| Dev.java · Learn | https://dev.java/learn/ | Tutoriales oficiales actuales |
| Java SE API (última) | https://docs.oracle.com/en/java/javase/ | Consulta de `String`, `Object`, `Date`, arreglos |
| `java` launcher | https://docs.oracle.com/en/java/javase/14/docs/specs/man/java.html | Ejecutar clases y `-cp` |
| `javac` | https://docs.oracle.com/en/java/javase/14/docs/specs/man/javac.html | Compilación y `-d` |

### 3.2. Maven

| Referencia | URL | Para qué |
|---|---|---|
| Maven · Getting Started | https://maven.apache.org/guides/getting-started/ | Estructura de proyecto y ciclo de vida |
| Maven Compiler Plugin | https://maven.apache.org/plugins/maven-compiler-plugin/ | `source`, `target`, `release` |
| Maven POM Reference | https://maven.apache.org/pom.html | `groupId`, `artifactId`, `packaging` |
| Maven in 5 Minutes | https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html | Primer proyecto |

Los poms del curso son mínimos: no hay dependencias externas, plugins de ejecución ni perfiles. Para reproducirlos basta el compilador de Maven.

### 3.3. IDE

| Referencia | URL | Para qué |
|---|---|---|
| Apache NetBeans | https://netbeans.apache.org/ | IDE inferido por `.netbeans_automatic_build` |
| NetBeans Tutorials | https://netbeans.apache.org/tutorials/ | Importar proyectos Maven |
| IntelliJ IDEA | https://www.jetbrains.com/idea/ | Alternativa de IDE |
| Eclipse | https://www.eclipse.org/ide/ | Alternativa de IDE |
| VS Code Java | https://code.visualstudio.com/docs/languages/java | Alternativa ligera |

### 3.4. Conceptos del curso

| Concepto | Referencia sugerida |
|---|---|
| Clases y objetos | JLS §8 y §12; Dev.java · Objects |
| Constructores | JLS §8.8 |
| Paso por valor | JLS §8.4.1; Dev.java · Passing Information to a Method or Constructor |
| `this` | JLS §15.8.3 |
| `null` | JLS §3.10.7 y §4.1 |
| Encapsulamiento | Dev.java · Classes and Objects; Effective Java, Item 15 |
| `static` | JLS §8.3.1.1 y §8.4.3.2 |
| Herencia | JLS §8.1.4 y §8.4.8 |
| Sobrecarga | JLS §8.4.9 y §15.12 |
| Paquetes | JLS §7 |
| `final` | JLS §4.12.4, §8.1.1.2, §8.4.3.3 |
| Arreglos | JLS §10 |
| Matrices | JLS §10.2 |
| Composición | Effective Java, Item 18 |

---

## 4. Lenguaje C

### 4.1. Estándares

| Referencia | URL | Para qué |
|---|---|---|
| ISO/IEC 9899:2018 (C17) | https://www.iso.org/standard/74528.html | Estándar vigente de C |
| WG14 (ISO C) | https://www.open-std.org/jtc1/sc22/wg14/ | Documentos de trabajo y borradores |
| C23 (ISO/IEC 9899:2024) | https://www.open-std.org/jtc1/sc22/wg14/www/docs/n3096.pdf | Borrador de C23, para comparar |
| cppreference · C | https://en.cppreference.com/w/c | Referencia técnica de la biblioteca y el lenguaje |
| POSIX `gets` | https://pubs.opengroup.org/onlinepubs/9699919799/functions/gets.html | Historia y retirada de `gets` |

### 4.2. Compiladores

| Referencia | URL | Para qué |
|---|---|---|
| GCC · Dialect Options | https://gcc.gnu.org/onlinedocs/gcc/C-Dialect-Options.html | `-std=gnu89`, `-std=c17` |
| GCC · Warning Options | https://gcc.gnu.org/onlinedocs/gcc/Warning-Options.html | `-Wall`, `-Wextra`, `-Wpedantic` |
| GCC · Instrumentation Options | https://gcc.gnu.org/onlinedocs/gcc/Instrumentation-Options.html | `-fsanitize=address,undefined` |
| Clang | https://clang.llvm.org/docs/ | Alternativa a GCC |
| Valgrind | https://valgrind.org/docs/manual/manual.html | Memoria y fugas |

### 4.3. Seguridad y buenas prácticas

| Referencia | URL | Para qué |
|---|---|---|
| SEI CERT C Coding Standard | https://wiki.sei.cmu.edu/confluence/display/c/SEI+CERT+C+Coding+Standard | Reglas de código seguro |
| CWE-242: Use of Inherently Dangerous Function | https://cwe.mitre.org/data/definitions/242.html | `gets` y funciones peligrosas |
| CWE-120: Buffer Copy without Checking Size | https://cwe.mitre.org/data/definitions/120.html | Desbordamientos |
| OWASP · Buffer Overflow | https://owasp.org/www-community/vulnerabilities/Buffer_Overflow | Contexto de seguridad |

### 4.4. Bibliografía clásica

| Libro | Autores | Uso |
|---|---|---|
| *The C Programming Language* (2.ª ed.) | Brian W. Kernighan, Dennis M. Ritchie | Referencia canónica de C89 |
| *C Programming: A Modern Approach* (2.ª ed.) | K. N. King | Didáctica moderna de C |
| *Effective C* | Robert C. Seacord | C moderno y seguridad |
| *Expert C Programming: Deep C Secrets* | Peter van der Linden | Punteros y modelo de memoria |
| *Java: How to Program* | Deitel & Deitel | Didáctica de Java |
| *Effective Java* (3.ª ed.) | Joshua Bloch | Buenas prácticas de Java |

Los libros no están incluidos en el repositorio; se citan como lecturas complementarias.

### 4.5. Herencia Turbo C

| Referencia | URL | Para qué |
|---|---|---|
| Turbo C++ (Wikipedia) | https://en.wikipedia.org/wiki/Turbo_C%2B%2B | Contexto histórico de `conio.h` y DOS |
| `conio.h` (referencia) | https://en.wikipedia.org/wiki/Conio.h | Funciones no portables |
| DOSBox | https://www.dosbox.com/ | Emular el entorno original, si se necesita |

No se recomienda ejecutar el material en DOS real; la guía de portabilidad del README es la vía preferida.

---

## 5. Herramientas de archivo y documentos

| Referencia | URL | Para qué |
|---|---|---|
| PKWARE APPNOTE (ZIP) | https://pkware.cachefly.net/webdocs/casestudies/APPNOTE.TXT | Formato ZIP y banderas UTF-8 |
| Python `zipfile` | https://docs.python.org/3/library/zipfile.html | Inspección sin extracción |
| Info-ZIP `unzip` | https://linux.die.net/man/1/unzip | Extracción en Linux/macOS |
| Microsoft `Expand-Archive` | https://learn.microsoft.com/powershell/module/microsoft.powershell.archive/expand-archive | Extracción en Windows |
| LibreOffice | https://www.libreoffice.org/get-help/documentation/ | Abrir y convertir `.doc` |
| `antiword` | https://linux.die.net/man/1/antiword | Leer `.doc` en terminal |
| `catdoc` | https://www.wagner.pp.ru/~vitus/software/catdoc/ | Alternativa a `antiword` |
| `iconv` | https://www.gnu.org/software/libiconv/ | Convertir Latin-1/CP850 a UTF-8 |

---

## 6. Accesibilidad y documentación

| Referencia | URL | Para qué |
|---|---|---|
| WCAG 2.1 Quick Reference | https://www.w3.org/WAI/WCAG21/quickref/ | Contraste y texto alternativo |
| WAI · Images | https://www.w3.org/WAI/tutorials/images/ | `alt` y SVG accesibles |
| MDN · SVG | https://developer.mozilla.org/en-US/docs/Web/SVG | Sintaxis y `viewBox` |
| GitHub Flavored Markdown | https://github.github.com/gfm/ | Tablas, bloques y enlaces |

Los SVG del repositorio incluyen `<title>` y `<desc>`; si se convierten a HTML, se debe conservar el equivalente textual.

---

## 7. Referencias por tema del curso

### 7.1. Java

| Módulo | Referencia principal |
|---|---|
| Instalación | Java SE 14 Documentation; Apache NetBeans |
| Clases y objetos | JLS §8; Dev.java · Classes |
| Constructores | JLS §8.8 |
| Paso por valor/referencia | JLS §8.4.1; Dev.java · Passing Information |
| `return` y `void` | JLS §14.17 |
| `this` | JLS §15.8.3 |
| `null` | JLS §3.10.7 |
| Encapsulamiento | Effective Java, Item 15 |
| `static` | JLS §8.3.1.1 |
| Herencia | JLS §8.1.4 |
| Sobrecarga | JLS §8.4.9 |
| Paquetes | JLS §7 |
| `final` | JLS §4.12.4 |
| Arreglos y matrices | JLS §10 |
| Diseño de clases | Effective Java, Items 15–18 |

### 7.2. C

| Bloque | Referencia principal |
|---|---|
| Variables y tipos | ISO C17 §6.2; cppreference · Types |
| Control de flujo | ISO C17 §6.8; cppreference · Statements |
| Funciones y alcance | ISO C17 §6.2.2 y §6.9; K&R cap. 4 |
| Recursión | K&R cap. 4; King cap. 9 |
| Arreglos | ISO C17 §6.5.2; K&R cap. 5 |
| Ordenamiento | K&R cap. 5; King cap. 9 |
| Cadenas | ISO C17 §7.24; cppreference · string |
| Punteros | ISO C17 §6.5.3; K&R cap. 5; van der Linden |
| Estructuras | ISO C17 §6.7.2; K&R cap. 6 |
| `gets` y seguridad | CERT C; CWE-242; POSIX `gets` |

---

## 8. Notas de vigencia

- **Java 14** dejó de recibir actualizaciones públicas; para producción usa un LTS. La especificación SE 14 sigue siendo útil para entender el curso.
- **C17** es el estándar estable; **C23** introduce cambios que no aparecen en el material. La guía de portabilidad apunta a C17.
- **Turbo C** y **`conio.h`** son históricos. No se recomienda enseñar su uso como estándar, sino como caso de código heredado.
- **`gets`** fue retirada de C11 por seguridad; el material la usa 11 veces. La referencia de POSIX documenta su retirada.
- **NetBeans 2020** está descatalogado; la versión actual cambia la ubicación de algunos menús descritos en los `.doc`.

---

## 9. Cómo verificar una referencia

Antes de citar una URL en una adaptación:

1. Comprueba que responde y que el contenido corresponde al tema.
2. Prefiere documentación oficial (Oracle, ISO, WG14, GCC) sobre blogs.
3. Anota la fecha de consulta, porque las páginas de “latest” cambian.
4. Para estándares, cita la cláusula o sección, no solo la página.
5. Para código, distingue “compatible con C89” de “recomendado en C17”.

---

## 10. Referencias no utilizadas

Se descartaron deliberadamente:

- enlaces a cursos pagos o plataformas con registro;
- repositorios de terceros con licencias incompatibles;
- tutoriales sin autoría ni fecha;
- contenido generado por IA sin revisión;
- enlaces acortados o con seguimiento.

Si necesitas una referencia que no está aquí, agrégala con URL completa, título, autor y fecha de consulta, y justifica por qué es relevante para el material.
