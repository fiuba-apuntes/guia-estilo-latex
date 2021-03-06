# Guía de estilo para LaTeX

A continuación se presenta una guía de estilo para el código LaTeX de los
documentos de FIUBA Apuntes.

## Índice

* [Archivos](#archivos)
  + [Nombre del archivo LaTeX](#nombre-del-archivo-latex)
  + [Codificación](#codificación)
* [General](#general)
  + [Largo de línea](#largo-de-línea)
  + [Indentación](#indentación)
* [Preámbulo](#preámbulo)
  + [Encabezado del documento](#encabezado-del-documento)
  + [Clase del documento](#clase-del-documento)
  + [Paquetes](#paquetes)
* [Cuerpo (documento)](#cuerpo-documento)
  + [Distribución del texto](#distribución-del-texto)
  + [Indentación y separación entre secciones](#indentación-y-separación-entre-secciones)
  + [Etiquetas y referencias](#etiquetas-y-referencias)
* [Fuentes](#fuentes)

## Archivos

### Nombre del archivo LaTeX

Con el fin de que los archivos fuentes sean interoperables entre los distintos
sistemas operativos, los archivos y directorios no deben contener espacios.
El nombre de directorios y archivos puede contener letras sin acentos en
_lowercase_ (minúsculas) [a-z], dígitos [0-9] y las separaciones con guiones (-),
pero sin espacios.
El punto (.) sólo se usa para separar el nombre del archivo con la extensión.
La extensión de todo archivo fuente de documentos LaTeX debe ser `tex`.

<table>
  <tr>
    <th>Recomendable</th>
    <th>NO Recomendable</th>
  </tr>
  <tr>
    <td>
      <code>
      &nbsp;mi-archivo-1.tex
      </code>
    </td>
    <td>
      <code>
      &nbsp;Mi Archivo 1.tex<br>
      &nbsp;mi.archivo.1.tex
      </code>
    </td>
  </tr>
</table>

### Codificación

Usar la codificación UTF-8 para los archivos LaTeX.
De esta manera es posible ingresar directamente la mayoría de los caracteres
extendidos como vocales con acentos, diéresis, etc.

Para que LaTeX interprete adecuadamente al archivo almacenado con codificación
UTF-8, se debe incluir el paquete `inputenc`.
Éste debe ser el primer paquete, luego de definir el `documentclass`.

```latex
\usepackage[utf8]{inputenc}
```

## General

### Largo de línea

Para que el archivo se visualice correctamente en cualquier editor sin necesidad
de ajuste de línea, se recomienda que la longitud de línea sea de entre 80 y 100
caracteres.

En caso de que se ingresen comandos con argumentos y opciones que exceden el
largo de línea sugerido, se recomienda distribuir de la siguiente manera.

```latex
\comando[
  opcion1,
  opcion2,
  opcion 3
]{argumento}

\comando[opciones]{argumento-corto}{
  argumento-largo
}
```

### Indentación

El contenido del archivo fuente de un documento es básicamente el contenido del
documento que se va a generar, por lo tanto, predomina mucho el texto.
Es por ello que hay que encontrar un equilibrio entre no indentar (haciendo
difícil reconocer ciertos elementos) a usar indentación excesiva (el código es
muy legible, pero queda poco espacio para el texto).

El tamaño de la indentación debe ser de 2 espacios.
No usar `Tabs` ya que muchos editores lo interpretan como 8 espacios.

## Preámbulo

### Encabezado del documento

Se recomienda incluir al inicio del archivo, incluso antes del `documentclass`,
un encabezado con información relacionada con el documento, como autor,
versión del documento, fecha de creación, última actualización, descripción
breve del contenido del documento, etc.

El doble `%` es intencional, para indicar que se trata de un encabezado, no de
un comentario normal.

```latex
%% plantilla-apunte.tex
%% V2
%% 2015/08/26
%% por FIUBA Apuntes
%% http://fiuba-apuntes.github.io/
%%
%% Esta es la plantilla a usar para los documentos de FIUBA Apuntes.
%%
%% Licencia Creative Commons Atribución-NoComercial-CompartirIgual 4.0
%%
```

### Clase del documento

Ingresar `documentclass` en una única linea, a excepción de que exceda el largo
de línea, pudiendo separar cada opción en una línea o cuando se crea conveniente
para una mejor legibilidad, por ejemplo, contener más de 3 opciones.

```latex
\documentclass[
  12pt,
  twoside,
  a4paper,
  draft
]{article}
```
### Paquetes

Ingresar un paquete por línea e indicar mediante un comentario que funcionalidad
habilita dicho paquete.

```latex
\usepackage[utf8]{inputenc} % Indica cuál es la codificación de este archivo
\usepackage[spanish]{babel} % Indica el idioma en que está escrito el documento
\usepackage[svgnames]{xcolor} % Permite usar colores en el documento
\usepackage{amssymb} % Fuentes y símbolos adicionales (por AMS)
\usepackage{amsmath} % Mejoras a entornos matemáticos y extras (por AMS)
\usepackage{mathtools} % Correcciones a amsmath y funcionalidades extras
```

En caso de que un paquete permita realizar configuraciones adicionales,
realizarlas inmediatamente después de la inclusión del mismo.
Además, se recomienda la inclusión de un encabezado para reconocer la inclusión
de un paquete que va a ser configurado.

```latex
\usepackage[utf8]{inputenc} % Indica cuál es la codificación de este archivo
\usepackage[spanish]{babel} % Indica el idioma en que está escrito el documento
\usepackage[svgnames]{xcolor} % Permite usar colores en el documento

% *** LISTING PACKAGE ***
% Permite ingresar código fuente de software
%
\usepackage{listings}

\lstset{ % Defino el formato de bloques de código fuente
  inputencoding=utf8, % Indica la codificación de los archivos de entrada
  extendedchars=true, % Extiende los caracteres
  numbers=left, % Posición en que se muestran los números de línea
  backgroundcolor=\color{gray!5}, % Color de fondo
  basicstyle=\ttfamily\footnotesize, % Estilo de base (familia, tamaño, color)
}

\lstdefinestyle{cpp}{
  tabsize=4,
  language=C++,
  keywordstyle=\color{DarkGreen}, % Estilo de las palabras reservadas
  stringstyle=\color{DarkBlue}, % Estilo de los strings
  commentstyle=\color{DarkGray}, % Estilo de los comentarios
}

\lstdefinestyle{ruby}{
  language=Ruby,
  keywordstyle=\color{DarkMagenta}, % Estilo de las palabras reservadas
  stringstyle=\color{DarkBlue}, % Estilo de los strings
  commentstyle=\color{DarkGray} % Estilo de los comentarios
}

\usepackage{amssymb} % Fuentes y símbolos adicionales (por AMS)
\usepackage{amsmath} % Mejoras a entornos matemáticos y extras (por AMS)
```

## Cuerpo (documento)

### Distribución del texto

Se recomienda iniciar cada oración en una línea nueva, ya que LaTeX incluye
en un párrafo todo el texto que se encuentre sin líneas en blanco.

**NO recomendado**
```
Este es mi primer texto en LaTeX. Estoy muy contento.
```

**Recomendado**
```
Este es mi primer texto en LaTeX.
Estoy muy contento.
```

### Indentación y separación entre secciones

Indentar sólo cuando se inicia un nuevo grupo o entorno, a excepción del entorno
`document`, ya que reduciría el espacio para el contenido de todo el documento.
NO indentar cuando se inicia una nueva sección.
Si se hiciera, en cada subsección quedaría cada vez menos espacio para el texto.

**NO recomendado**
```latex
\documentclass{article}
\begin{document}
  \section{Sección 1}
    ¡Hola mundo!
    \begingroup
      Contenido de un grupo
    \endgroup
    \subsection{Subsección 1}
      \begin{itemize}
        \item Item 1
        \item Item 2
      \end{itemize}
\end{document}
```

**Recomendado**

```latex
\documentclass{article}

\begin{document}

\section{Sección 1}

¡Hola mundo!

\begingroup
  Contenido de un grupo
\endgroup

\subsection{Subsección 1}

\begin{itemize}
  \item Item 1
  \item Item 2
\end{itemize}

\end{document}
```

### Etiquetas y referencias

Agregar a las etiquetas (`\label{...}`) el prefijo correspondiente al elemento
etiquetado.
Cuando se asignan etiquetas a multiples elementos, los prefijos permite
distinguirlas fácilmente cuando las mismas son referenciadas.

| Prefijo   | Elemento             |
| --------- | -------------------- |
| `ch:`     | chapter              |
| `sec:`    | section              |
| `subsec:` | subsection           |
| `fig:`    | figure               |
| `tab:`    | table                |
| `eq:`     | equation             |
| `lst:`    | code listing         |
| `fn:`     | footnote             |
| `itm:`    | itemized list item   |
| `enum:`   | enumerated list item |
| `alg:`    | algorithm            |
| `app:`    | appendix subsection  |

Recordar que al ingresar la referencia, sólo se imprimirá el número
correspondiente a la etiqueta referenciada.
Es por eso que es normal anteponer el nombre del elemento a la referencia.
Para evitar que el nombre del elemento y la referencia sean separadas por un
salto de línea, ingresar entre ellas un **espacio de no separación**
(_non-breaking space_).

```latex
Ver la Figura~\ref{fig:mi-figura} en la página~\pageref{fig:mi-figura}.
```

## Fuentes

Las fuentes que han servido de inspiración para el desarrollo de la guía de
estilo (además de la experiencia de cada uno escribiendo documentos en LaTeX).

* [LaTeX Wikibook: Basics](https://en.wikibooks.org/wiki/LaTeX/Basics)
* [LaTeX Wikibook: Labels and Cross-referencing](https://en.wikibooks.org/wiki/LaTeX/Labels_and_Cross-referencing)
* [Towards LaTeX coding standards](https://www.tug.org/TUGboat/tb32-3/tb102verna.pdf)
* [Are there any coding style guidelines for LaTeX?](http://tex.stackexchange.com/questions/40775/are-there-any-coding-style-guidelines-for-latex)
* [Manuscript Templates for Conference Proceedings](http://www.ieee.org/conferences_events/conferences/publishing/templates.html)
