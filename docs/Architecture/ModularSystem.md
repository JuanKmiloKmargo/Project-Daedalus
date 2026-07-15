# Sistema de Arquitectura Monolítica Modular
## ¿Qué es una Arquitectura Monolítica Modular?
La arquitectura de monolito modular organiza una única base de código en módulos funcionales independientes y con reglas de negocio estrictas. Cada módulo actúa como un micorservicio lógico, comunicándose con otros solo a través de interfaces o eventos, lo que facilita la escalabilidad del desarrollo sin la complejidad de la infraestructura distribuida.
## Reglas de Clasificación Modular (Modular Classification Rules o MCRs)
### Clasificación de Capas (Layer MCR)
### 1. Capa de Aplicación (App Layer)
Es la capa superior del diagrama, sus Módulos poseen la funcionalidad más completa y compleja del sistema. Sus Módulos son quienes interactuan directamente con la interfaz alojada en el Core de Daedalus.
### 2. Capa de Acceso (Access Layer)
Es la capa inferior del diagrama, generalmente sus Módulos poseen un conjunto pequeño de funcionalidades relacionadas con el Acceso de Datos del Sistema.
### 3. Capas de Funcionalidad (Functional Layers)
Son todas las capas intermedias, no existe un número determinado de estas capas pues su cantidad aumenta con la complejidad del Sistema.
### Clasificación por Lookdown Functionality (LDF MCR)
Esta clasificación se da bajo un módulo de referencia, clasificando los módulos de capas inferiores. Si se cambia la referencia la clasificación cambia también, así que el diagrama no es único pero las categorías están bien definidas.
### 1. Módulos Dependencias (D-Modules o DMods)
Su funcionamiento SIEMPRE debe estar ligado al del módulo de referencia, es decir, son fundamentales para la funcionalidad de su Referencia. Un DMod de un DMod es también un DMod para la Referecia.
### 2. Módulos Elegibles (E-Modules o EMods)
Su funcionamiento NO SIEMPRE está ligado al de la referencia, es decir, son complementarios para la funcionalidad de su Referencia. Un EMod de un EMod es también un EMod para la Referecia.
### 3. Módulos Nulos (N-Modules o NMods)
Su funcionamiento NUNCA está ligado al de la referencia, es decir, no existen desde la perspectiva de la Referencia. Estos pueden incluir los demás módulos en la capa donde se encuentra la Referencia.
### 4. Módulos Subelegibles (SE-Modules o SE.Mods)
Es una clafificación combinada útil para capas de varios niveles abajo del de la referencia. Para explicar su clasificación se van a definir genéricamente los Módulos Mod1 y Mod2, ambos EMods de la referencia inicialmente, pero luego resulta que Mod1 es un DMod de Mod2, en este caso Mod1 se vuelve un SE.Mod de la Referencia. Esta clasificación implica que, efectivamente Mod1 es EMod de la referencia, pero también que su vínculo con la Referencia no depende únicamente de Mod1
### 5. Módulos Dependencias Volátiles (VD-Modules o VD.Mods)
Es una clafificación combinada útil para capas de varios niveles abajo del de la referencia. Para explicar su clasificación se van a definir genéricamente los Módulos Mod1 y Mod2, ambos DMods de la referencia inicialmente, pero luego resulta que Mod1 es un EMod de Mod2, en este caso Mod1 se vuelve un VD.Mod de la Referencia.

Posteriormente será necesario hacer una clasificación cambiando el módulo de referencia por otro módulo en alguna capa superior a la referencia anterior, por lo que a esta antigua referencia ahora se llamará Mod3. Existen entonces 2 posibilidades:
- **Mod3 es DMod de la Referencia**, entonces Mod1 es ED.Mod de la nueva referencia
- **Mod3 es EMod de la Referencia**, entonces Mod1 es EMod de la nueva referencia
## ¿Cómo es la comuniación entre módulos?
En el modelo por capas los módulos solo se pueden comunicar verticalmente, es decir, dos módulos en la misma capa no pueden enviarse información entre ellos, necesitan de un módulo superior para poder comunicarse. Por lo general, los módulos **Dependencias** tienen una funcionamiento que requiere compartir datos con más módulos, y los módulos **Elegibles** pueden trabajar solo con la información y funcionalidades de submódulos inferiores, propios y del módulo **Programa** para el cuál son Elegibles.
## ¿Cómo se comunican los módulos con el Core?
Debido a al planteamiento del modelo los módulos Programa son los únicos que se pueden comunicar con el Core, y entre ellos no es posible comunicarse pues todos los módulos programas se encuentran en la misma capa. Así pues, el Core cumple una función de **canal de comunicación** entre módulos Programa. Ver [Daedalus Core](docs/Architecture/DaedalusCore.md)
## Insersión de Módulos y Creación de nuevas Capas
