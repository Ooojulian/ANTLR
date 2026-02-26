# Implementación de Calculadora con ANTLR4 (Capítulo 4)

Este repositorio contiene la implementación y ejecución del evaluador de expresiones matemáticas (calculadora) descrito en el Capítulo 4 del libro *The Definitive ANTLR 4 Reference*, utilizando Java como lenguaje objetivo.

📄 **Documentación Completa:** Para una explicación profunda sobre la definición de la gramática, la lógica implementada mediante el patrón *Visitor*, la matriz de validación (batería de pruebas) y la visualización gráfica de los árboles de derivación, por favor consulta el documento oficial del proyecto: **[`LP_ANTLR.pdf`](./LP_ANTLR.pdf)**.

---

## 🛠️ Entorno y Herramientas
* **Sistema Operativo:** Ubuntu Linux (o compatible)
* **Lenguaje Objetivo:** Java (JDK)
* **Herramienta:** ANTLR 4.13.1

---

## 🚀 Guía de Ejecución Rápida

Si deseas clonar y probar este proyecto localmente, sigue estos pasos desde tu terminal:

### 1. Generar el compilador y compilar el código
Asegúrate de indicarle a ANTLR que genere la infraestructura basada en el patrón *Visitor*:
```bash
# Generar Lexer, Parser y Visitor base
antlr4 -visitor LabeledExpr.g4

# Compilar todos los archivos .java
javac *.java
