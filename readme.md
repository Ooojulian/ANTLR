¡Claro que sí, Julián! Tienes todo funcionando a la perfección, así que ahora vamos a estructurar esta documentación para que quede con un nivel técnico impecable, ideal para presentar en un contexto académico de ciencias de la computación o teoría de lenguajes.

Aquí tienes una plantilla completa en formato Markdown. Puedes copiarla y pegarla directamente en tu editor de texto o en un archivo `.md`.

---

# Documentación: Implementación de Calculadora con ANTLR4 (Capítulo 4)

## 1. Objetivo

Implementar y ejecutar el evaluador de expresiones matemáticas (calculadora) descrito en el Capítulo 4 de *The Definitive ANTLR 4 Reference*, utilizando Java como lenguaje objetivo. El proyecto incluye la definición de la gramática, la generación del analizador léxico/sintáctico, la implementación de un recorrido del árbol mediante el patrón *Visitor* y la visualización gráfica del árbol de derivación.

## 2. Entorno y Herramientas

* **Sistema Operativo:** Ubuntu Linux
* **Lenguaje Objetivo:** Java (JDK)
* **Herramienta:** ANTLR 4.13.1
* **Archivos base:** `LabeledExpr.g4` (Gramática), `EvalVisitor.java` (Lógica de evaluación), `Calc.java` (Clase principal).

## 3. Definición de la Gramática (`LabeledExpr.g4`)

Se diseñó una gramática libre de contexto para manejar operaciones matemáticas básicas y asignación de variables.

* **Reglas Léxicas (Tokens):** Se definieron identificadores (`ID`) usando letras `[a-zA-Z]+`, enteros (`INT`) con dígitos `[0-9]+`, y se configuró el descarte de espacios en blanco (`WS -> skip`).
* **Reglas Sintácticas:** Se establecieron reglas para el manejo de precedencia matemática nativa. ANTLR resuelve la precedencia basándose en el orden de las alternativas en la regla `expr`, dando prioridad a la multiplicación/división (`MulDiv`) sobre la suma/resta (`AddSub`), y permitiendo la agrupación mediante paréntesis (`parens`).
* **Etiquetas:** Se utilizaron etiquetas (ej. `# AddSub`, `# assign`) para que ANTLR genere métodos específicos para cada alternativa en el código del *Visitor*.

## 4. Generación y Compilación

Para construir el compilador, se indicó a ANTLR que generara la infraestructura basada en el patrón *Visitor* en lugar del *Listener* por defecto. Los comandos ejecutados fueron:

```bash
# Generación de los archivos Java (Lexer, Parser y Visitor base) a partir de la gramática
antlr4 -visitor LabeledExpr.g4

# Compilación de todos los archivos fuente
javac *.java

```

## 5. Lógica de Evaluación (`EvalVisitor.java`)

El núcleo de la calculadora reside en la clase `EvalVisitor`, la cual hereda de `LabeledExprBaseVisitor<Integer>`.

* **Memoria:** Se implementó un `HashMap<String, Integer>` para actuar como la memoria del entorno, almacenando los pares de clave-valor cuando se realiza una asignación (ej. `a = 10`).
* **Recorrido:** El *Visitor* recorre el árbol de sintaxis abstracta (AST). Al visitar nodos de operaciones matemáticas (como `visitAddSub`), el algoritmo extrae recursivamente los valores de los nodos hijos (operandos izquierdo y derecho) y ejecuta la operación aritmética correspondiente en Java.

## 6. Pruebas y Ejecución (`Calc.java`)

Se creó un archivo de prueba llamado `prueba.txt` con las siguientes instrucciones:

```text
100
a = 10
b = 20
a + b * 2
(a + b) * 2

```

Se ejecutó el programa principal, el cual inicializa el flujo de entrada (`ANTLRInputStream`), el analizador léxico (`LabeledExprLexer`), el flujo de tokens (`CommonTokenStream`) y finalmente el analizador sintáctico (`LabeledExprParser`).

**Comando de ejecución:**

```bash
java Calc prueba.txt

```

**Salida en consola:**

```text
100
50
60

```

*Análisis de la salida:* El programa evalúa correctamente las asignaciones en memoria sin imprimirlas, respeta la precedencia de operadores (evaluando `10 + 40 = 50`) y altera correctamente la precedencia cuando se usan paréntesis (evaluando `30 * 2 = 60`).

## 7. Visualización del Árbol de Derivación (Parse Tree)

Para validar la correcta construcción sintáctica y descartar ambigüedades en la gramática, se utilizó la herramienta `TestRig` (mediante el alias `grun`) para generar la interfaz gráfica del árbol de derivación.

**Comando ejecutado:**

```bash
grun LabeledExpr prog -gui prueba.txt

```

*(Nota: Aquí puedes adjuntar una captura de pantalla de la ventana de Java que se abrió mostrando el arbolito para darle un toque más profesional a tu entrega).*

---

¿Te gustaría que te ayude a pasar este texto a un formato PDF o necesitas añadir alguna conclusión adicional sobre la teoría de lenguajes detrás de este ejercicio?
