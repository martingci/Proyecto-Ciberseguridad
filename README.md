# Proyecto de ciberseguridad:

## Estudiantes:
- David Baez.
- Martín Carrasco.
- Sabrina López.

## Componentes de la solución:

### Miner:
- Clona el repositorio.
- Ejecuta el análisis de código fuente con CodeQL.
- Genera un SBOM con Syft.
- Detecta vulnerabilidades de los componentes.

### Analyzer:
- Utiliza los datos del miner y se implementa por notebooks.

### Visualizer: 
- Permite la distribución de vulnerabilidades, comparación de repositorios, comunicar diferentes en severidad y tipos.

### Aspectos adicionales
- Replicable por medio de _Dev Containers_.

## Contextualización

En diciembre del año pasado, 2025, [se detectaron varias vulnerabilidades en los componentes de React Server](https://vercel.com/kb/bulletin/react2shell#faq) que utiliza Vercel, cuyas calificaciones de CVSS van desde 7,5 a 10. Tales grados de gravedad generan una gran preocupación por la seguridad de sus usuarios, ya que, Vercel proporciona herramientas para desarrolladores e infraestructura en la nube para diversos proyectos de software de distintas áreas, muchos de los cuales también ofrecen servicios gratuitos en la web a otros usuarios que también pueden verse comprometidos por estas vulnerabilidades.

Es por esto que el análisis realizado busca comprobar si existen otras vulnerabilidades por descubrir dentro de los componentes de la organización. Para esto se realizaron los SBOMs, análisis estático del código fuente con CodeQL, y análisis de vulnerabilidades con Grype de los 25 repositorios de libre acceso más populares (con más estrellas) de Vercel.

## Resultados cuantitativos

Las cifras totales obtenidas se componen de:
- 6470 problemas de código fuente, todos de nivel de severidad “warning”, es decir, medio dentro de la clasificación de SARIF.
- 16971 vulnerabilidades de componentes, todas de nivel de severidad “low”, es decir, bajo dentro de la clasificación CVSS.

## Análisis cualificativo

Aparte de los problemas y vulnerabilidades más recurrentes entre los repositorios que fueron analizados dentro del [notebook](analyzer/analyzer.ipynb), al equipo le llamó la atención las vulnerabilidades del componente Kysely dentro de los repositorio de *chatbot* y *examples*, que contenían dos amenazas de posibles inyecciones SQL calificadas con un CVSS de [8,1](https://github.com/advisories/GHSA-8cpq-38p9-67gx) y de [8,2](https://github.com/advisories/GHSA-wmrf-hv6w-mr66), con Vercel aún manteniendo la versión afectada por ambas, 0.28.11, a pesar de que la primera ya ha sido corregida en la versión siguiente (0.28.12) y la segunda fue corregida en la versión 0.28.14.

Dentro del análisis de vulnerabilidades, las del componente sólo se clasifican como “low”, es decir, por debajo de 3,9, evidenciando que la utilización de diferentes herramientas entrega resultados distintos, por lo que, ahí es donde entra el trabajo del equipo de revisar estas contradicciones y registrarlas para mejorar los análisis posteriores con, probablemente, otras herramientas.

## Conclusiones

Para finalizar, se comprobó que la organización Vercel todavía presenta vulnerabilidades de sus componentes utilizados, sin embargo, se toman en serio estas advertencias y, al ser informados de estas amenazas, probablemente tomarán medidas de protección a sus usuarios como ocurrió en el caso de diciembre de 2025.

Por el lado del trabajo de análisis realizado, el equipo comprueba la importancia de comprobar los resultados obtenidos sobre componentes, problemas de código fuente, y vulnerabilidades de los componentes para contrastar las posibles contradicciones con los registros públicos disponibles.
