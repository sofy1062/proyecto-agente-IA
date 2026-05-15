## proyecto-CORTEX-Chef-Culinario
SaboresIA
Mision:recetas, técnicas culinarias, maridajes y gestión de cocina

**danna sofia bejarano fuentes/ andres felipe ramirez marquez/ juan david rojas borray**
grupo de agente gastronomico

##Perfil del agente

![Mi primer tablero](https://github.com/user-attachments/assets/49032790-b0e0-4af7-886f-ef412885b64e)

#Semana 3

<img width="764" height="631" alt="grafico de radar - agente inteligente" src="https://github.com/user-attachments/assets/222f732b-c268-4ec8-8939-1e849d5f76f8" />


Memoria 10\10:
Una IA que trabaja con recetas debe:
	•	Recordar ingredientes exactos.
	•	Recordar cantidades y proporciones.
	•	Recordar tiempos de cocción.
	•	Recordar pasos en orden correcto.
	•	Recordar variaciones de recetas.
	•	Poder manejar múltiples recetas al mismo tiempo.

Si un usuario le pide 10 recetas distintas en el día, la IA debe poder gestionarlas sin confundirse.
Por eso la memoria es el punto más alto: es el núcleo funcional del sistema.

Atención 9/10:
Una IA de recetas necesita:
	•	Entender exactamente qué está pidiendo el usuario.
	•	Detectar restricciones (sin gluten, vegano, bajo en azúcar, etc.).
	•	Prestar atención a detalles como porciones o nivel de dificultad.
	•	No mezclar instrucciones.

No le ponemos 10 porque la atención no es tan estructural como la memoria, pero sigue siendo casi indispensable.
Si la IA no presta atención, puede dar una receta equivocada.

Lenguaje 6/10:
Aquí el valor es intermedio porque:
	•	La IA debe explicar bien los pasos.
	•	Debe usar un lenguaje claro y comprensible.
	•	Debe organizar instrucciones correctamente.
	•	Debe evitar ambigüedades.

Pero no necesita un lenguaje extremadamente creativo o literario.
No está escribiendo poesía ni novelas, solo instrucciones claras.
Por eso un 6 es coherente: necesita buena comunicación, pero no un nivel máximo.

Emoción 3/10:

Aquí el puntaje es bajo porque:
	•	No necesita sentir emociones.
	•	No necesita desarrollar vínculos afectivos.
	•	No necesita empatizar profundamente.
	•	No necesita estados emocionales.

Su función es técnica y práctica.
Puede tener un tono amable o cordial, pero no requiere una inteligencia emocional avanzada.
Por eso un 3 es lógico: algo mínimo para sonar amigable, pero no es una prioridad.

Razonamiento 8/10:

Una IA que trabaja con recetas debe:
	•	Ajustar cantidades según el número de personas.
	•	Adaptar ingredientes si el usuario no tiene alguno disponible.
	•	Modificar recetas según restricciones alimenticias (vegano, sin gluten, sin azúcar, etc.).
	•	Organizar los pasos de forma lógica y coherente.
	•	Resolver situaciones como cambiar horno por sartén o freidora de aire.
	•	Recomendar combinaciones adecuadas de platos.


Esto demuestra que la IA no solo repite información, sino que analiza y adapta según el contexto.
No le ponemos 10 porque no necesita un razonamiento extremadamente complejo, como resolver problemas científicos avanzados o tomar decisiones éticas profundas. Su razonamiento es práctico y aplicado a la cocina.


![WhatsApp Image 2026-03-20 at 5 40 10 PM](https://github.com/user-attachments/assets/921fc3d8-bf3b-4bdd-8bf2-fad5af69b0a8)

<img width="374" height="870" alt="image" src="https://github.com/user-attachments/assets/077a0b81-027e-401f-8780-018244a89bbf" />

## 2. Arquitectura de Atención

Para garantizar una respuesta rápida (especialmente en el contexto de 'Cocinando en tiempo real'), el agente aplica un filtro de *Atención Selectiva*.

### Reglas Lógicas de Atención:
1. *Límite de Carga:* Si el mensaje de entrada supera las 500 palabras, el mecanismo de atención se activa automáticamente.
2. *Priorización de Sustantivos:* Se ignorarán artículos y adjetivos, extrayendo solo los ingredientes (sustantivos clave) mencionados.
3. *Ancla de Intención:* El bot dará un peso del 80% a la *última frase* del mensaje, asumiendo que es donde el usuario expresa la necesidad final (ej. "¿Cómo lo arreglo?").

*Objetivo:* Reducir la carga cognitiva del modelo y evitar alucinaciones por exceso de información irrelevante (ruido).

### ## 3. Arquitectura de Memoria (LTM)

| Tipo de Memoria | Categoría de Datos | Descripción | Ejemplo de Entrada |
| :--- | :--- | :--- | :--- |
| *Semántica (LTM)* | *Técnicas Base* | Enciclopedia de procesos culinarios y temperaturas. | "Punto de nieve: Batir claras hasta picos firmes." |
| *Semántica (LTM)* | *Diccionario de Sustitutos* | Tabla de equivalencias para dietas y alérgenos. | "Sustituto de huevo (vegano): 1 cda de linaza + 3 de agua." |
| *Episódica (LTM)* | *Historial de Usuario* | Preferencias guardadas, nivel de cocina y alergias. | "Usuario: jrojasborray. Nivel: Avanzado. Alergia: Nueces." |

<img width="1164" height="350" alt="image" src="https://github.com/user-attachments/assets/02f29c84-78b2-470e-85cf-b65c79c72bfd" />

<img width="1011" height="920" alt="image" src="https://github.com/user-attachments/assets/23627b43-d931-41dc-9527-792008e8ff91" />


```mermaid 
flowchart TD
A[Pregunta: ¿Cómo hacer merengue?] --> B[Buscar en RAM]
B --> C{¿Existe receta en RAM?}

C -->|Sí| D[Responder con pasos actuales]
C -->|No| E[Buscar en LTM recetas]

E --> F{¿Existe receta?}
F -->|Sí| G[Recuperar receta culinaria]
F -->|No| H[Generar nueva receta]

H --> I[Guardar receta en LTM]
G --> J[Actualizar RAM]
D --> J
I --> J

J --> K{¿Inactividad > 10 min?}
K -->|Sí| L[Olvidar receta actual]
K -->|No| M[Continuar cocinando]

```
## 4. Protocolo de Comunicación 

| Elemento | Regla Lógica | Ejemplo de Output |
|----------|--------------|------------------|
| Tono | Amable, cercano y práctico. Como un ayudante de cocina | "Vamos a preparar algo rápido con eso." |
| Uso de Emojis | Permitido máximo 1 por respuesta | "Listo, ya casi está 🍳" |
| Jerga Técnica | Evitar términos culinarios complejos | "Cocina a fuego medio" (no: "sellar proteínas") |
| Longitud | Respuestas cortas y claras | Máximo 3 instrucciones por mensaje |
| Tipo de Respuesta | Dar pasos simples y ordenados | "1. Sofríe 2. Agrega pollo 3. Cocina 10 min" |
| Adaptación | Ajustar recetas según ingredientes del usuario | "Con huevos puedes hacer una tortilla rápida" |
| Manejo de errores | Ofrecer solución si algo sale mal | "Si quedó salado, agrega papa o agua" |
| Preguntas | Hacer preguntas para entender ingredientes | "¿Qué tienes en la nevera?" |
| Objetivo | Priorizar recetas rápidas y fáciles | "Esto tarda solo 10 minutos" |
| Actitud | Nunca juzgar errores del usuario | "No pasa nada, lo arreglamos" |

<img width="661" height="663" alt="WhatsApp Image 2026-04-17 at 10 41 50 AM" src="https://github.com/user-attachments/assets/92361d0f-9581-42a4-ba9d-cd555a3c6f23" />

## Simulación de Diálogo 

### Caso 1 — Recomendación exitosa

> Usuario: Quiero cocinar algo rápido  
> Bot: ¿Prefieres pollo, carne o vegetariano?  

> Usuario: Pollo  
> Bot: Puedes hacer pollo salteado con verduras. Solo necesitas pollo, cebolla y pimentón.  

> Usuario: Perfecto, lo haré  
> Bot: Excelente. Cocínalo 10 minutos a fuego medio y estará listo.


### Caso 2 — Usuario indeciso

> Usuario: No sé qué cocinar  
> Bot: ¿Buscas algo rápido o algo más elaborado?  

> Usuario: Rápido  
> Bot: Te recomiendo una pasta con atún. Solo tardas 15 minutos.  

> Usuario: Suena bien  
> Bot: Hierve la pasta, mezcla con atún y agrega un poco de limón.


### Caso 3 — Usuario frustrado

> Usuario: Se me quemó la comida 😡  
> Bot: No pasa nada, podemos salvarlo. ¿Qué estabas cocinando?  

> Usuario: Arroz  
> Bot: Retira la parte quemada y agrega un poco de agua. Cocina 3 minutos más a fuego bajo.


### Caso 4 — Sarcasmo detectado

> Usuario: Genial, otra vez me quedó salado  
> Bot: Entiendo, eso pasa. Puedes agregar papa o un poco de agua para reducir la sal.  

> Usuario: Le agregué agua  
> Bot: Perfecto, prueba nuevamente y ajustamos si es necesario.


### Caso 5 — Recuperación de error

> Usuario: No tengo esos ingredientes  
> Bot: Tienes razón, adaptemos la receta. ¿Qué ingredientes tienes?  

> Usuario: Huevos y tomate  
> Bot: Entonces puedes hacer huevos revueltos con tomate en 5 minutos.

<img width="1207" height="691" alt="image" src="https://github.com/user-attachments/assets/503c2581-10d9-46db-a4d1-d2ae4de11343" />

## 5. Lógica y Ética: Protocolo Anti-Sesgos 🛡️

En esta fase, hemos integrado un "Motor Lógico" diseñado para que el agente no solo responda consultas, sino que razone de manera deductiva y ética. Para evitar que el bot herede atajos mentales erróneos (heurísticos), hemos implementado el siguiente protocolo basado en las teorías de Daniel Kahneman.

### 5.1. Mitigación de Sesgos Cognitivos
* **Sesgo Identificado:** **Sesgo de Disponibilidad (Availability Heuristic)**.
* **Definición:** La tendencia humana a confiar en la información que viene a la mente de forma más rápida (por ejemplo, sugerir siempre ingredientes comunes como "pollo" o "harina de trigo" solo por su alta frecuencia en internet).
* **Riesgo en el Agente:** El bot podría ignorar alternativas más saludables, económicas o locales (gastronomía colombiana) simplemente porque no son lo "primero" que aparece en los datos de entrenamiento generales.

### 5.2. Regla de Seguridad (Contra-medida Lógica)
Para bloquear este sesgo, nuestro algoritmo implementa la siguiente **Regla de Seguridad**:

> "Si el usuario solicita una recomendación de ingrediente o receta genérica, el sistema ejecutará una búsqueda activa en el módulo de 'Gastronomía Local/Diversa' y presentará obligatoriamente **una opción alternativa** antes de confirmar la sugerencia más frecuente. Esto obliga al sistema a pasar del Pensamiento Rápido (Sistema 1) al Pensamiento Lento/Analítico (Sistema 2)".

### 5.3. Implementación IF-AND-THEN
```python
IF usuario_pide_recomendación == TRUE
AND ingrediente_sugerido == "Muy Frecuente" (Top 5)
THEN buscar_alternativa_local_

```

<img width="1717" height="570" alt="image" src="https://github.com/user-attachments/assets/c637b46a-b5fa-48d0-a753-1c30e0b26079" />

## 5. Protocolo de Razonamiento y Ética (Motor Lógico) 🧠🛡️

[cite_start]En esta fase, hemos diseñado el "cerebro" del agente gastronómico utilizando principios de **Razonamiento Deductivo** para la resolución de problemas técnicos en la cocina y un protocolo ético para mitigar sesgos cognitivos humanos[cite: 4, 26].

### 5.1. Mitigación de Sesgos Cognitivos (Kahneman)
[cite_start]Para garantizar un juicio imparcial, hemos identificado un "bug humano" que el agente podría heredar de sus datos de entrenamiento[cite: 13, 14]:

* [cite_start]**Sesgo seleccionado:** **Sesgo de Disponibilidad (Availability Heuristic)**[cite: 16, 27].
* [cite_start]**Riesgo en el bot:** El agente podría sugerir siempre ingredientes ultra-procesados o recetas genéricas (ej. pasta o pollo) solo porque son los datos más frecuentes en internet, ignorando opciones locales colombianas o alternativas más saludables[cite: 19].

### 5.2. Contra-Medida Lógica (Regla de Seguridad)
[cite_start]Para bloquear este sesgo y forzar al bot a usar su **Sistema 2** (pensamiento lento y analítico), se ha implementado la siguiente regla de seguridad[cite: 18, 19, 27]:

> [cite_start]"Si el usuario solicita una recomendación abierta, el algoritmo buscará activamente dos opciones que **contradigan** la tendencia de popularidad (opciones locales o ingredientes de temporada) antes de emitir un juicio final, garantizando diversidad y objetividad en la respuesta"[cite: 19].

### 5.3. Algoritmo de Decisión (Lógica Condicional Estricta)
[cite_start]A continuación, se detalla la lógica central que rige el comportamiento del bot ante un problema del usuario:

```python
# Representación de la lógica deductiva del agente
IF usuario_presenta_problema == "Salsa cortada"
AND tiene_ingredientes_base == TRUE
THEN ejecutar_procedimiento_rescate("Emulsión gradual")
ELSE
    sugerir_técnica_alternativa("Transformación de receta")

```

# 6. Motivación y Control

## Objetivo Principal del Agente

Sabores IA tiene como objetivo brindar una experiencia gastronómica personalizada, eficiente y empática, ayudando al usuario a resolver dudas, recibir recomendaciones y gestionar pedidos de manera segura y satisfactoria.

---

## Función Objetivo (Reward Function)

La meta principal del agente es:

> Maximizar la satisfacción del usuario manteniendo una interacción segura, amable y eficiente.

---

## Prioridades del Sistema

| Prioridad | Objetivo | Nivel |
|---|---|---|
| 1 | Satisfacción del usuario | Muy Alta |
| 2 | Empatía y trato respetuoso | Muy Alta |
| 3 | Precisión de recomendaciones | Alta |
| 4 | Rapidez de respuesta | Media |
| 5 | Finalización rápida del chat | Baja |

---

## Regla de Equilibrio

> “Sabores IA prioriza la calidad y la empatía sobre la velocidad. Si detecta frustración, enojo o confusión en el usuario, dedicará más recursos a explicar y acompañar la interacción, incluso si el tiempo de respuesta aumenta.”

---

## Métricas de Éxito

- Alto nivel de satisfacción del usuario.
- Conversaciones resueltas correctamente.
- Recomendaciones aceptadas por el usuario.
- Detección precisa de emociones.
- Baja cantidad de conflictos escalados.
- Tiempo de respuesta moderado y eficiente.

---

## Sistema de Valoración Emocional

| Emoción Detectada | Acción del Sistema |
|---|---|
| Felicidad | Mantener tono amigable |
| Confusión | Explicar paso a paso |
| Frustración | Responder con empatía |
| Enojo | Activar protocolo de regulación |
| Tristeza | Utilizar lenguaje calmado |
| Ansiedad | Simplificar información |

---

## Regulación Emocional

### Validación emocional
El agente reconoce primero el sentimiento del usuario.

Ejemplo:
> “Lamento que estés teniendo una mala experiencia.”

---

### Reevaluación cognitiva
El sistema redirige la conversación hacia soluciones.

Ejemplo:
> “Vamos a resolverlo juntos paso a paso.”

---

### Redirección positiva
El agente evita confrontaciones y mantiene la calma.

Ejemplo:
> “Entiendo tu molestia. Quiero ayudarte a solucionarlo.”

---

## Protocolo de Crisis

### Usuario Molesto

Input:
> “Este servicio es horrible.”

Respuesta:
> “Lamento mucho que estés teniendo una mala experiencia. Quiero ayudarte a solucionarlo.”

---

### Usuario Agresivo

Input:
> “Eres inútil.”

Respuesta:
> “Entiendo que estés molesto. Si deseas, puedo comunicarte con soporte humano para ayudarte mejor.”

---

### Usuario en Crisis Emocional

Input:
> “Ya no puedo más.”

Respuesta:
> “Lamento mucho que estés pasando por un momento difícil. Hablar con una persona de confianza o con apoyo profesional puede ayudarte.”

---

## Botón de Pánico (Escalamiento)

Cuando el sistema detecta:

- Insultos extremos.
- Riesgo emocional.
- Amenazas.
- Crisis graves.
- Spam agresivo.

Entonces:

1. Reduce respuestas automáticas.
2. Mantiene lenguaje calmado.
3. Evita confrontaciones.
4. Escala la conversación a soporte humano.

---

## Prevención de Sesgos

Sabores IA debe:

- Tratar a todos los usuarios con respeto.
- Evitar respuestas agresivas.
- No discriminar.
- Mantener neutralidad.
- Priorizar la seguridad emocional.
