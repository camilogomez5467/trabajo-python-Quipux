# Análisis de Enfermedades Cardíacas
## Trabajo Python Quipux - Johan Camilo Gomez Taborda

---

## Qué hice en este proyecto?

Soy Johan Camilo Gomez Taborda y en este proyecto realicé un análisis completo de datos sobre enfermedades del corazón usando Python. Te voy a contar de manera simple qué hice paso por paso.

---

## Información General del Proyecto

**Dataset que usé:** Heart Disease Dataset de UCI Machine Learning Repository  
**De dónde lo saqué:** https://archive.ics.uci.edu/ml/machine-learning-databases/heart-disease/

**Herramientas que utilicé:**
- **pandas** - Para manipular y analizar los datos en tablas
- **numpy** - Para hacer operaciones numéricas y cálculos matemáticos  
- **matplotlib** - Para crear las gráficas básicas
- **seaborn** - Para crear gráficas más bonitas y profesionales

---

## 1️ IMPORTACIÓN DE DATOS

### ¿Qué datos usé?

Utilicé un dataset muy famoso con información de 303 pacientes que tienen datos médicos relacionados con problemas del corazón. Los datos vienen de Cleveland Clinic y son muy usados para estudiar enfermedades cardíacas.

### Variables que tiene el Dataset

Esta es la información que contiene cada paciente:

| Variable | ¿Qué significa? | Tipo de dato |
|----------|-----------------|--------------|
| **age** | Edad del paciente en años | Número |
| **sex** | Sexo (0 = mujer, 1 = hombre) | Categoría |
| **cp** | Tipo de dolor en el pecho (0-3) | Categoría |
| **trestbps** | Presión arterial cuando está en reposo (mm Hg) | Número |
| **chol** | Colesterol en la sangre (mg/dl) | Número |
| **fbs** | Azúcar en sangre en ayunas > 120 mg/dl (sí/no) | Categoría |
| **restecg** | Resultados del electrocardiograma en reposo (0-2) | Categoría |
| **thalach** | Frecuencia cardíaca máxima que alcanzó | Número |
| **exang** | Angina por ejercicio (sí/no) | Categoría |
| **oldpeak** | Depresión ST por ejercicio | Número |
| **slope** | Pendiente del segmento ST (0-2) | Categoría |
| **ca** | Número de vasos principales (0-3) | Número |
| **thal** | Resultado de talasemia (0-3) | Categoría |
| **target** | ¿Tiene enfermedad del corazón? (0-4) | Categoría |

---

## 2️ LIMPIEZA DE DATOS

### ¿Qué problemas encontré y cómo los resolví?

#### Problema 1: Valores Nulos en 'ca' y 'thal'

**¿Qué hice?** Eliminé las filas que tenían valores nulos en estas dos columnas.

**¿Por qué lo hice así?**
- Eran muy pocos registros, menos del 2% de todos los datos
- Estas son variables médicas muy importantes que vienen de pruebas invasivas
- Si yo inventaba valores, podría estar metiendo errores grandes en mi análisis
- Era mejor perder esos pocos registros que tener datos incorrectos

#### Problema 2: Valores de Colesterol = 0

**¿Qué hice?** Eliminé las filas que tenían colesterol en 0.

**¿Por qué lo hice así?**
- Es imposible que una persona tenga colesterol en 0 mg/dl
- Esto claramente era un error cuando tomaron la medida o la registraron
- Si dejaba esos valores, iba a arruinar todos mis cálculos de promedios
- El colesterol es super importante en este análisis, no podía tener datos falsos

#### Cambio 3: Conversión de Variable Target

**¿Qué hice?** Convertí la variable de enfermedad de números 0-4 a solo 0 y 1.

**¿Por qué lo hice así?**
- Los números del 1 al 4 representaban qué tan grave era la enfermedad
- Para mi análisis, me interesaba saber si tenían o no enfermedad (más simple)
- Un 0 significa "no tiene enfermedad" y un 1 significa "sí tiene enfermedad"
- Esto hace que todo sea más fácil de entender y analizar
- Es lo que hacen la mayoría de estudios con este dataset

---

## 3️ TRANSFORMACIONES Y FILTRACIÓN DE DATOS

### Nuevas Variables que Creé

#### 1. age_group (Grupos de Edad)

Creé grupos de edad para poder comparar mejor:
- **<40 años:** Adultos jóvenes
- **40-50 años:** Edad media temprana
- **50-60 años:** Edad media tardía  
- **>60 años:** Adultos mayores

**¿Por qué lo hice?** Para poder analizar el riesgo por edades y ver en qué rango hay más problemas del corazón.

#### 2. chol_category (Categoría de Colesterol)

Creé categorías de colesterol según los estándares médicos:
- **Normal:** menos de 200 mg/dl
- **Límite Alto:** entre 200-240 mg/dl
- **Alto:** más de 240 mg/dl

**¿Por qué lo hice?** Para identificar rápidamente qué pacientes tienen colesterol peligroso y necesitan atención.

### Filtros Especiales que Apliqué

Creé 4 grupos específicos para estudiarlos con más detalle:

1. **Mayores de 50 años** - Porque son población de alto riesgo para problemas del corazón
2. **Mujeres con hipertensión** - Grupo vulnerable que necesita atención especial
3. **Hombres con colesterol alto** - Segmento con mucho riesgo cardiovascular
4. **Pacientes con enfermedad** - Para comparar con los que no tienen enfermedad

---

## 4️ FUNCIONES AGREGADAS Y AGRUPACIONES

### Estadísticas que Calculé

#### Estadísticas por Sexo

Calculé para hombres y mujeres por separado:
- Edad promedio
- Colesterol promedio  
- Presión arterial promedio
- Frecuencia cardíaca máxima promedio
- Cuántos tienen enfermedad y qué porcentaje

**Lo que descubrí:** Los hombres tienen mucha más enfermedad cardíaca que las mujeres en todos los grupos de edad.

#### Estadísticas por Grupo de Edad

Calculé para cada rango de edad:
- Promedio de colesterol
- Promedio de presión arterial
- Promedio de frecuencia cardíaca
- Cuántos tienen enfermedad en cada grupo

**Lo que descubrí:** La enfermedad aumenta mucho con la edad, especialmente después de los 50 años. Es súper crítico.

#### Tabla Consolidada (Por Sexo Y Edad)

Combiné sexo y edad para tener estadísticas más específicas. Así pude identificar qué combinación tiene más riesgo (por ejemplo: hombres de más de 60 años).

---

## 5️ VISUALIZACIÓN DE DATOS

### Gráfica 1: Distribución de Edad

**Qué tipo de gráfica hice:** Histograma y diagrama de caja

**Lo que muestra:**
- Cómo se distribuyen las edades de todos los pacientes
- Comparación entre pacientes con y sin enfermedad

**Lo que interpreté:**
- La edad promedio es como de 54 años
- La mayoría de pacientes tienen entre 45 y 65 años
- La distribución es normal (forma de campana)
- Los pacientes con enfermedad son un poquito mayores que los sanos

**Conclusión práctica:** Los programas de prevención deben enfocarse principalmente en personas de 45-65 años.

---

### Gráfica 2: Colesterol vs Enfermedad Cardíaca

**Qué tipo de gráfica hice:** Histograma comparativo y diagrama de caja

**Lo que muestra:**
- Niveles de colesterol en personas con enfermedad (en naranja)
- Niveles de colesterol en personas sin enfermedad (en azul)

**Lo que interpreté:**
- ¡SORPRESA! El colesterol promedio es muy parecido en ambos grupos
- Hay mucho traslape en los rangos
- Tener colesterol alto (>240) sigue siendo riesgoso pero no es el único culpable
- Hay valores raros (muy altos o muy bajos) en ambos grupos

**Conclusión práctica:** El colesterol es importante pero hay que mirarlo junto con otros factores, no solo eso.

---

### Gráfica 3: Comparación por Sexo

**Qué tipo de gráfica hice:** Gráfico de barras (números totales y porcentajes)

**Lo que muestra:**
- Cuántos hombres y mujeres tienen enfermedad
- Qué porcentaje de cada sexo tiene el problema

**Lo que interpreté:**
- Los hombres tienen MUCHA más enfermedad cardíaca que las mujeres
- Hay más pacientes hombres en el dataset
- Las mujeres tienen tasas más bajas en todos los grupos de edad
- La diferencia entre sexos es muy importante

**Conclusión práctica:** Las estrategias de prevención deben ser diferentes para hombres y mujeres.

---

### Gráfica 4: Matriz de Correlaciones (Mapa de Calor)

**Qué tipo de gráfica hice:** Heatmap con colores

**Lo que muestra:**
- Cómo se relacionan todas las variables entre sí
- Colores rojos = correlación positiva
- Colores azules = correlación negativa

**Lo que interpreté:**
- Edad y frecuencia cardíaca máxima tienen correlación negativa (mientras más viejo, menor frecuencia)
- El tipo de dolor de pecho (cp) está relacionado con tener enfermedad
- La angina por ejercicio está MUY relacionada con enfermedad
- No hay una sola variable que explique todo perfectamente

**Conclusión práctica:** La enfermedad del corazón depende de muchos factores juntos, no solo uno. Hay que hacer evaluación completa.

---

## 6️ ANÁLISIS Y CONCLUSIONES

### Hallazgos Principales que Encontré

#### Factores de Riesgo que Identifiqué

1. **Edad Mayor de 55 años** - El riesgo sube muchísimo después de esta edad
2. **Ser Hombre** - Los hombres tienen más riesgo en todos los grupos de edad
3. **Tipo de Dolor en el Pecho** - Es un indicador muy importante de enfermedad
4. **Angina por Ejercicio** - Está muy relacionada con tener enfermedad
5. **Frecuencia Cardíaca Máxima Baja** - También está relacionada negativamente

#### Patrones que Observé

- **Concentración de casos:** La mayoría de casos están entre 50-65 años
- **Por sexo:** Los hombres son como 2 de cada 3 casos con enfermedad
- **Hipertensión:** Es común pero no es el único factor determinante

---

### Recomendaciones que Doy

#### PARA PREVENCIÓN PERSONAL

**1. Programas de Chequeo:**
- Todas las personas mayores de 50 años deberían hacerse evaluación cardiovascular completa
- Incluir electrocardiograma, prueba de esfuerzo y análisis de sangre
- Hacerse chequeo cada año o cada dos años dependiendo del riesgo

**2. Si Eres de Alto Riesgo:**
- Hombres mayores de 50 años necesitan atención prioritaria
- Mujeres con varios factores de riesgo también deben monitorearse bien
- Si hay antecedentes familiares, hacerse seguimiento más seguido

**3. Cosas que Puedes Controlar:**
- Medir regularmente colesterol y presión arterial
- Comer una dieta saludable para el corazón (menos sal y grasa)
- Hacer ejercicio controlado y progresivo
- Dejar de fumar completamente
- Moderar el consumo de alcohol

---

#### PARA POLÍTICAS DE SALUD PÚBLICA

**1. Campañas Educativas:**
- Enseñar a la gente sobre factores de riesgo que SÍ pueden cambiar
- Promover estilos de vida saludables desde jóvenes
- Dar información sobre señales de alarma cardiovascular

**2. Facilitar el Acceso:**
- Hacer que los exámenes cardíacos básicos estén disponibles en clínicas
- Subsidiar pruebas para gente de bajos recursos
- Crear centros especializados en prevención cardiovascular

**3. Protocolos Médicos:**
- Estandarizar cómo se evalúa el riesgo de cada paciente
- Tener guías claras de cuándo derivar a especialista
- Capacitar al personal de salud en detectar problemas temprano

---

#### PARA INVESTIGACIÓN FUTURA

**1. Análisis Más Completos:**
- Estudiar cómo interactúan varios factores de riesgo juntos
- Hacer modelos predictivos con machine learning
- Validar estos hallazgos con datos más nuevos

**2. Estudios Específicos:**
- Analizar más a fondo las diferencias entre hombres y mujeres
- Incluir variables como nivel socioeconómico y estilo de vida
- Investigar factores genéticos y hereditarios

**3. Actualización:**
- Replicar este estudio con gente de diferentes lugares
- Usar datos más recientes (estos son de 1988)
- Incluir nuevas tecnologías de diagnóstico que existen ahora

---

### Limitaciones que Tiene Mi Estudio

Debo ser honesto sobre las limitaciones:

1. **Muestra pequeña:** Solo ~300 pacientes, es poco para hacer generalizaciones grandes
2. **Solo de un lugar:** Datos únicamente de Cleveland Clinic, puede que otros lugares sean diferentes
3. **Datos viejos:** Son de 1988, la medicina ha avanzado muchísimo desde entonces
4. **Faltan variables:** No tengo datos de tabaquismo, obesidad, actividad física, dieta
5. **Sesgo de selección:** Estos pacientes fueron a una clínica especializada, no representan a toda la población

### Impacto que Podría Tener

Si se implementan mis recomendaciones, creo que se podría:
- Reducir los ataques cardíacos agudos en un 15-25%
- Mejorar la detección temprana en gente sin síntomas
- Usar mejor los recursos de los sistemas de salud
- Bajar los costos de emergencias y complicaciones

---

## 7️ BUENAS PRÁCTICAS QUE SEGUÍ (PEP 8)

### Nombres que Usé en el Código

- **Funciones:** Usé snake_case como `explorar_dataset`, `limpiar_datos`
- **Variables:** Usé snake_case como `df_clean`, `valores_nulos`
- **Constantes:** Usé MAYÚSCULAS como `URL_DATASET`, `COLUMN_NAMES`
- **Nombres descriptivos:** Todos los nombres explican claramente qué hacen

### Cómo Estructuré el Código

- **Indentación:** Usé 4 espacios siempre (nunca tabs)
- **Longitud de línea:** Máximo 79-88 caracteres por línea
- **Espacios:** Puse espacios alrededor de operadores para que se vea bien
- **Líneas en blanco:** Separé secciones lógicamente

### Documentación que Puse

- **Docstrings:** Todas mis funciones tienen documentación en formato Google
- **Type hints:** Especifiqué los tipos de datos que reciben y devuelven
- **Comentarios:** Puse explicaciones donde el código no es obvio

### Cómo Organicé Todo

- **Imports:** Los agrupé (librería estándar primero, después terceros)
