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

##4. Protocolo de Comunicación 

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
