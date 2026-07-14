# Sistema de Módulos por capas
## ¿Qué es un módulo?
Es una unidad funcional alojada en el Core de Daedalus, es decir, busca cumplir una serie de funciones definidas. Los módulos se pueden conectar entre ellos en una estructura por capas, en el que los módulos superiores pueden acceder a funciones de módulos inferiores, pero no a las de módulos en la misma capa o en módulos superiores.
## Clasificación de los Módulos según su gerarquía
### 1. Módulos Programa
Son los módulos que ocupan la primera capa de la gereaquía, quien puede acceder a las funciones de todos los demás Módulos.
### 2. Módulos Escenciales
Están en la capa inferior del diagrama, no tienen módulos inferiores y por lo general cumplen con un conjunto compacto de funciones
## Clasificación por Lookdown Functionality (LDFC)
Esta clasificación se da según la perspectiva de un solo módulo de referencia, clasificando a todos los módulos de capas inferiores así:
### 1. Módulos Dependencias
Su funcionamiento siempre debe estar ligado al del módulo superior, sin los módulos dependencia el módulo superior no puede funcionar
### 2. Módulos Elegibles
Es posible desligar su funcionamiento del funcionamiento del módulo superior, entonces dicho módulo superior puede funcionar sin necesidad del funcionamiento del módulo Elegible. Aún así, el funcionamiento del módulo Elegible puede complementar el del módulo superior
### 3. Módulos Subelegibles o Dependencias de alto nivel
Dado un esquema de capas 3 > 2 > 1 que no son necesariamente consecutivas, un módulo en 1 es subelegible para un módulo dado en 3 si se cumple que:
- El módulo en 1 es **Dependencia** del módulo dado en 3
- Un módulo dado en 2 es **Dependencia** del módulo dado en 3
- El módulo en 1 es **Elegible** para el mismo módulo dado en 2

Estos módulos subelegibles son interesantes para el analisis con LDFC, pues si el módulo de referencia sube, digamos a un módulo en la capa 4, tenemos que:
- Si el módulo dado en 3 es **Dependencia** del módulo dado en 4, entonces el módulo dado en 1 es **Subelegible** para el módulo en 4.
- Si el módulo dado en 3 es **Elegible** para el módulo dado en 4, entonces el módulo dado en 1 es **Elegible** para el módulo en 4.
### 4. Módulos Inconexos
Su funcionamiento no se puede ligar al del módulo superior, por lo que son funcionalmente inexistentes para el módulo superior.
