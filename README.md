# Reducción Polinómica de TSP a SAT en Java

Proyecto académico desarrollado para la implementación y resolución del Problema del Viajante (TSP) mediante su reducción polinómica a un problema de satisfacibilidad booleana (SAT), utilizando la librería Sat4j y el estándar de exportación DIMACS CNF.
## Requisitos del Sistema
- **Java Development Kit (JDK):** Versión 11 o superior.
- **Entorno de Desarrollo:** Apache NetBeans IDE (recomendado) o terminal con Apache Ant.
- **Librería Externa:** Sat4j Core (Versión 2.3.6 - archivo `org.ow2.sat4j.core-2.3.6.jar`).
## ️ Configuración de Dependencias
1. Descarga el archivo `.jar` de la librería **Sat4j** (versión 2.3.6).
2. En tu proyecto de NetBeans, haz clic derecho sobre la carpeta **Libraries** (Bibliotecas) de tu proyecto.
3. Selecciona **Add JAR/Folder** y añade el archivo `org.ow2.sat4j.core-2.3.6.jar` para habilitar el motor de resolución SAT y los lectores DIMACS.
## Instrucciones de Ejecución
El proyecto está estructurado modularmente siguiendo las siguientes fases: 
### Fase 1: Generación de la Instancia CNF
Ejecuta la clase generadora para construir el archivo de restricciones lógicas a partir de la matriz de costos y el umbral $K$:
- **Clase:** `TspDimacsGenerator.java`
- **Resultado:** Genera el archivo plano `tsp_instancia.cnf` en la raíz del proyecto bajo el formato estándar DIMACS CNF.
### Fase 2: Integración con el SAT-Solver
Ejecuta la clase de integración para deserializar el archivo CNF e inyectarlo en el motor CDCL de Sat4j:
- **Clase:** `TspSolverIntegration.java`
- **Resultado:** Evalúa la satisfacibilidad del sistema lógico y muestra en consola el veredicto de decisión (`SATISFIABLE` o `UNSATISFIABLE`).
### Fase 3: Reconstrucción de la Solución y Costo Real
Ejecuta la clase final para procesar el modelo booleano certificado:
- **Clase:** `TspSolutionReconstruction.java`
- **Resultado:** Si es `SAT`, decodifica las variables verdaderas para trazar la ruta exacta y calcular su costo real total. Si es `UNSAT`, emite el mensaje reglamentario de inexistencia de recorrido.
## Estructura del Código Fuente
- `TspDimacsGenerator.java`: Modelado de variables $X_{i,t}$, restricciones de visita única, ocupación única y umbral de costo.
- `TspSolverIntegration.java`: Interfaz con la API de Sat4j para el análisis de satisfacibilidad.
- `TspSolutionReconstruction.java`: Decodificación del certificado booleano y cálculo de la ruta óptima.
