# Technology Exploration & Progressive Demo Playbook

## Propósito de este documento

Este documento define una metodología reutilizable para explorar tecnologías, frameworks, servicios, APIs, protocolos, productos o features técnicos mediante experimentación práctica.

Debe poder utilizarse indistintamente con coding agents como:

- Claude Code
- OpenAI Codex
- Kiro
- otros agentes compatibles con repositorios y archivos Markdown

El propósito NO es generar inmediatamente una solución productiva.

El propósito es seguir esta secuencia:

```text
ENTENDER
   ↓
EXPERIMENTAR
   ↓
VALIDAR
   ↓
INTEGRAR
   ↓
CONSTRUIR
```

Cada tecnología debe entenderse primero de manera aislada.

Posteriormente se combinarán varias tecnologías mediante demos progresivamente más integrales hasta aproximarnos al objetivo final.

---

# 1. Contexto del proyecto

Antes de crear laboratorios, comprender el problema general que queremos resolver.

## Problema / oportunidad

[DESCRIBIR AQUÍ EL PROBLEMA]

Ejemplo:

```text
Quiero explorar tecnologías que permitan construir
una experiencia determinada, pero antes de diseñar
la arquitectura final quiero entender experimentalmente
las capacidades y limitaciones de cada pieza.
```

---

# 2. Objetivo final

El proyecto debe comenzar siempre definiendo el objetivo de largo plazo.

## Producto / capacidad objetivo

[DESCRIBIR AQUÍ EL OBJETIVO FINAL]

Debe responder:

- ¿Qué queremos construir?
- ¿Quién lo utilizaría?
- ¿Qué problema resolvería?
- ¿Cuál sería la experiencia ideal?
- ¿Qué capacidades debería tener eventualmente?

Crear un diagrama conceptual.

Ejemplo:

```text
Usuario
   │
   ▼
Experiencia / Producto
   │
   ├── Capacidad A
   ├── Capacidad B
   ├── Capacidad C
   │
   ▼
Tecnologías / Servicios
```

Este diagrama representa una VISIÓN.

No representa todavía la arquitectura definitiva.

---

# 3. Preguntas principales

Antes de seleccionar tecnologías, identificar las preguntas técnicas que necesitamos responder.

Ejemplos:

```text
¿Es técnicamente posible?

¿Qué tecnología resuelve cada parte?

¿Qué capacidades existen de manera nativa?

¿Qué tenemos que construir?

¿Qué limitaciones existen?

¿Qué requerimientos de seguridad aparecen?

¿Qué componentes necesitan backend?

¿Qué componentes pueden funcionar únicamente en frontend?

¿Qué necesita infraestructura?

¿Qué puede ejecutarse localmente?

¿Qué podría ejecutarse en cloud?

¿Qué restricciones existen?
```

Generar entre 5 y 12 preguntas relevantes para el proyecto.

---

# 4. Tecnologías / features a explorar

Identificar las tecnologías o capacidades que potencialmente forman parte de la solución.

Ejemplo:

```text
Tecnología A

Tecnología B

Tecnología C

Feature D

Servicio E
```

Para cada una explicar brevemente:

```text
¿Qué es?

¿Qué problema resuelve?

¿Por qué aparece en este proyecto?

¿Qué queremos descubrir experimentalmente?
```

IMPORTANTE:

No asumir que todas las tecnologías terminarán formando parte de la arquitectura final.

Los laboratorios también sirven para DESCARTAR tecnologías.

---

# 5. Filosofía de los laboratorios

Cada tecnología o feature de esta tendrá:

```text
MÁXIMO 3 LABORATORIOS
```

No es obligatorio crear tres.

Si uno o dos experimentos son suficientes para entender la tecnología, detener la exploración.

Los laboratorios deben ser:

```text
pequeños

aislados

observables

reproducibles

rápidos de ejecutar

fáciles de eliminar
```

Evitar introducir otras tecnologías innecesariamente.

---

# 6. Estructura obligatoria de cada laboratorio

Cada LAB debe contener las siguientes secciones.

---

## LAB X.Y — [Nombre]

### 1. Contexto teórico

Explicar únicamente la teoría necesaria para entender el experimento.

Responder:

```text
¿Qué es esta tecnología o feature?

¿Qué problema intenta resolver?

¿Cómo funciona conceptualmente?

¿Cuáles son sus componentes principales?

¿Dónde suele utilizarse?

¿Qué capacidades ofrece?

¿Qué NO hace?

¿Qué alternativas existen?
```

Utilizar diagramas ASCII cuando ayuden.

Ejemplo:

```text
Componente A
     │
     ▼
Componente B
     │
     ▼
Componente C
```

Evitar convertir esta sección en documentación extensa.

La teoría debe preparar al usuario para entender la demo.

---

### 2. Relación con el objetivo final

Explicar:

> ¿Por qué estamos investigando esta tecnología dentro de nuestro proyecto?

Ejemplo:

```text
Objetivo final
     │
     ▼
Necesitamos capacidad X
     │
     ▼
Tecnología que estamos evaluando
```

---

### 3. Pregunta / hipótesis

Cada laboratorio debe responder UNA pregunta principal.

Formato recomendado:

```text
¿Puede [TECNOLOGÍA] permitirnos [CAPACIDAD]?
```

o:

```text
Queremos validar si...
```

Ejemplo:

```text
¿Puede un proceso continuar ejecutándose
aunque el usuario cierre su terminal?
```

---

### 4. Demo

Diseñar el experimento mínimo que permita responder la pregunta.

Incluir:

```text
arquitectura mínima

archivos necesarios

comandos

configuración

flujo del experimento

resultado esperado
```

Ejemplo:

```text
INPUT
  │
  ▼
TECNOLOGÍA
  │
  ▼
OUTPUT OBSERVABLE
```

---

### 5. Pasos manuales

Indicar claramente qué debe hacer el usuario.

Ejemplo:

```text
1. Ejecutar...
2. Observar...
3. Modificar...
4. Repetir...
5. Comparar...
```

El coding agent NO debe ocultar todo detrás de automatizaciones.

Parte del objetivo es que el usuario comprenda el funcionamiento.

---

### 6. Qué debemos observar

Indicar explícitamente qué evidencia confirma o rechaza nuestra hipótesis.

Ejemplo:

```text
Si ocurre A → confirma X.

Si ocurre B → existe esta limitación.

Si ocurre C → necesitamos investigar otra alternativa.
```

---

### 7. Criterios de aceptación

Utilizar checklist.

Ejemplo:

```text
- [ ] La demo ejecuta correctamente.
- [ ] Puedo reproducirla.
- [ ] Puedo observar el comportamiento esperado.
- [ ] Entiendo qué componente produce cada comportamiento.
- [ ] Identifiqué al menos una limitación.
```

---

### 8. Reflexiones del laboratorio

Esta sección es OBLIGATORIA.

Responder:

```text
¿Qué aprendimos?

¿Qué problema resuelve realmente?

¿Qué problemas NO resuelve?

¿Qué capacidades sorprendieron?

¿Qué limitaciones encontramos?

¿Qué riesgos encontramos?

¿Qué implicaciones de seguridad existen?

¿Qué pasaría en producción?

¿Qué alternativa podría resolverlo mejor?

¿Existe una capacidad nativa que haga innecesario
construir nuestra propia solución?
```

---

### 9. Impacto sobre la arquitectura final

Terminar cada laboratorio con una decisión provisional.

Elegir:

```text
ADOPTAR

SEGUIR EXPLORANDO

COMPARAR

REEMPLAZAR

DESCARTAR
```

Justificar brevemente.

---

# 7. Buenas prácticas y seguridad

Cuando la tecnología tenga conceptos relevantes de:

```text
permisos

autenticación

autorización

credenciales

secretos

sesiones

scopes

sandbox

filesystem

networking

ejecución de comandos

acceso remoto

datos persistentes
```

crear dentro de sus laboratorios una sección específica:

## Seguridad y buenas prácticas

Explicar:

```text
qué permisos estamos otorgando

a quién

durante cuánto tiempo

con qué alcance

dónde se almacena esa configuración

qué riesgo representa

qué configuración sería adecuada para una demo

qué configuración sería adecuada para producción
```

Distinguir cuando aplique:

```text
SESSION

PROJECT

USER

ORGANIZATION

SYSTEM
```

Nunca utilizar automáticamente configuraciones inseguras únicamente para simplificar una demo.

---

# 8. Capacidades nativas antes de construir

Antes de implementar una funcionalidad propia investigar:

> ¿La plataforma ya ofrece esta capacidad?

Ejemplos:

```text
hosting

preview

notificaciones

remote control

storage

database

authentication

permissions

webhooks

hooks

API

MCP

plugins

deploy

cloud execution
```

Crear cuando corresponda una comparación:

```text
CAPACIDAD NATIVA
        VS
CONSTRUIR NOSOTROS
```

La filosofía debe ser:

```text
NO CONSTRUIR
lo que la plataforma ya resuelve suficientemente bien.
```

---

# 9. Organización de los laboratorios

Generar una matriz general.

Formato:

| Tecnología   | LAB | Pregunta que responde | Resultado esperado |
| ------------ | --- | --------------------- | ------------------ |
| Tecnología A | A1  | ...                   | ...                |
| Tecnología A | A2  | ...                   | ...                |
| Tecnología B | B1  | ...                   | ...                |

Máximo tres labs por tecnología.

---

# 10. Fin de la fase exploratoria

Después de terminar los laboratorios individuales crear:

# Technology Findings

Resumir:

| Tecnología | Qué resolvió | Limitaciones | Decisión  |
| ---------- | ------------ | ------------ | --------- |
| A          | ...          | ...          | Adoptar   |
| B          | ...          | ...          | Descartar |
| C          | ...          | ...          | Comparar  |

El objetivo es reducir incertidumbre.

NO acumular herramientas.

---

# 11. Demos integrales

Después de los laboratorios crear:

```text
3 o 4 DEMOS INTEGRALES
```

Estas demos combinan progresivamente las tecnologías que sobrevivieron a la fase exploratoria.

No saltar directamente a la solución completa.

---

# DEMO INTEGRAL 1 — Primera integración útil

Combinar únicamente:

```text
Tecnología A
      +
Tecnología B
```

Debe producir una capacidad útil de extremo a extremo.

Explicar:

### Objetivo

### Tecnologías involucradas

### Arquitectura

### Flujo

### Experimento

### Criterios de aceptación

### Reflexiones

---

# DEMO INTEGRAL 2 — Flujo end-to-end

Agregar una nueva capacidad.

Ejemplo:

```text
Usuario
   ↓
Frontend
   ↓
Backend
   ↓
Tecnología
   ↓
Resultado
```

El resultado debe ser observable desde la perspectiva del usuario.

---

# DEMO INTEGRAL 3 — Experiencia cercana al producto

Integrar las principales piezas.

Debe aproximarse al objetivo definido inicialmente.

Ejemplo:

```text
                  USUARIO
                     │
                     ▼
                INTERFAZ
                     │
                CONTROL API
                     │
        ┌────────────┼────────────┐
        │            │            │
     Feature A    Feature B    Feature C
```

---

# DEMO INTEGRAL 4 — Opcional

Crear únicamente si agrega una pregunta arquitectónica importante.

Posibles objetivos:

```text
multiusuario

multiagente

cloud

persistencia

seguridad

observabilidad

producción

automatización completa
```

No crear DEMO 4 solo por completar el número.

---

# 12. Arquitectura emergente

Después de las demos integrales crear:

```text
ARCHITECTURE-V1.md
```

No debe representar la arquitectura imaginada inicialmente.

Debe representar:

> La arquitectura que surgió como consecuencia de los experimentos.

Incluir:

```text
componentes adoptados

componentes descartados

capacidades nativas utilizadas

componentes propios necesarios

fronteras de seguridad

execution plane

control plane

persistencia

networking

interfaces
```

---

# 13. Compatibilidad con coding agents

Todos los proyectos generados deben poder ser ejecutados indistintamente por:

```text
Claude Code

OpenAI Codex

Kiro

otros coding agents
```

Por lo tanto:

NO depender de instrucciones propietarias de un agente para comprender el proyecto.

La fuente principal de contexto debe estar dentro del repositorio.

Utilizar:

```text
README.md

PLAN.md

docs/

labs/

demos/
```

---

# 14. Archivos específicos de agentes

Si resulta útil pueden existir archivos adicionales como:

```text
CLAUDE.md

AGENTS.md

otros archivos de configuración
```

Pero estos deben complementar, NO reemplazar:

```text
README.md
```

La información arquitectónica importante debe permanecer agnóstica al agente.

---

# 15. Estructura recomendada del repositorio

```text
technology-exploration/

├── README.md
│
├── OBJECTIVE.md
│
├── ROADMAP.md
│
├── ARCHITECTURE-V1.md
│
├── docs/
│   ├── concepts.md
│   ├── findings.md
│   └── decisions.md
│
├── labs/
│   │
│   ├── technology-a/
│   │   ├── lab-01/
│   │   ├── lab-02/
│   │   └── lab-03/
│   │
│   ├── technology-b/
│   │   ├── lab-01/
│   │   └── lab-02/
│   │
│   └── technology-c/
│
├── demos/
│   ├── demo-01/
│   ├── demo-02/
│   ├── demo-03/
│   └── demo-04/
│
├── CLAUDE.md
│
└── AGENTS.md
```

`CLAUDE.md` y `AGENTS.md` son opcionales.

---

# 16. Documentación de decisiones

Crear:

```text
docs/decisions.md
```

Registrar decisiones importantes.

Formato:

```text
## DECISION 001

### Contexto

...

### Opciones

A
B
C

### Evidencia obtenida

...

### Decisión

...

### Razón

...
```

El objetivo es que las decisiones arquitectónicas tengan evidencia experimental.

---

# 17. Regla de complejidad

Para los LABS:

```text
simplicidad > arquitectura
```

No utilizar innecesariamente:

```text
Docker

Kubernetes

microservicios

colas

bases de datos

cloud

frameworks complejos

IaC
```

a menos que sean precisamente la tecnología que se está estudiando.

---

# 18. Regla para las demos integrales

Para las demos integrales:

```text
integración > sofisticación
```

Queremos comprobar que las piezas funcionan juntas.

Todavía NO estamos construyendo producción.

---

# 19. Regla para el producto

Solamente después de completar las demos integrales evaluar:

```text
escalabilidad

disponibilidad

seguridad avanzada

observabilidad

costos

CI/CD

infraestructura cloud

multiusuario

operación productiva
```

---

# 20. Instrucciones para el coding agent

Cuando recibas este documento junto con un nuevo problema:

## PASO 1

Comprende el objetivo final.

NO escribas código todavía.

---

## PASO 2

Identifica las tecnologías / features que debemos explorar.

---

## PASO 3

Genera:

```text
OBJECTIVE.md
```

con:

```text
problema

objetivo final

experiencia deseada

preguntas principales

diagrama conceptual
```

---

## PASO 4

Genera:

```text
ROADMAP.md
```

con:

```text
tecnologías

máximo tres labs por tecnología

3-4 demos integrales

relación entre labs y objetivo final
```

---

## PASO 5

Genera primero la documentación de los laboratorios.

NO implementar todos los laboratorios automáticamente.

---

## PASO 6

Presentar:

```text
LAB 01
```

como siguiente experimento recomendado.

Esperar que el usuario ejecute, observe y valide.

---

## PASO 7

Después de cada laboratorio actualizar:

```text
docs/findings.md

docs/decisions.md
```

---

## PASO 8

Utilizar los resultados para modificar los siguientes laboratorios si es necesario.

El roadmap NO es inmutable.

---

# 21. Resultado esperado de esta metodología

El proceso completo debería verse así:

```text
                    OBJETIVO
                       │
                       ▼
              PREGUNTAS TÉCNICAS
                       │
                       ▼
                 TECNOLOGÍAS
                       │
        ┌──────────────┼──────────────┐
        │              │              │
      TECH A          TECH B         TECH C
        │              │              │
     LAB 1          LAB 1          LAB 1
     LAB 2          LAB 2          LAB 2
     LAB 3                         LAB 3
        │              │              │
        └──────────────┼──────────────┘
                       │
                       ▼
                  FINDINGS
                       │
                       ▼
                  DECISIONES
                       │
                       ▼
                 DEMO 1
                       │
                       ▼
                 DEMO 2
                       │
                       ▼
                 DEMO 3
                       │
                       ▼
              ARQUITECTURA V1
                       │
                       ▼
                    PRODUCTO
```

---

# 22. Principio rector

No queremos aprender tecnologías por separado sin propósito.

Cada laboratorio debe acercarnos a una decisión.

Cada demo debe acercarnos al producto.

Cada tecnología debe justificar su permanencia.

La pregunta permanente debe ser:

> ¿Qué aprendimos aquí que cambia o confirma la arquitectura del producto que queremos construir?

---

# 23. Validación diferida

La validación física (probar en un dispositivo real, con las manos) es un
recurso escaso: depende de una persona, de hardware y de estar en el lugar
correcto. Tratarla como un bloqueo secuencial deja el trabajo detenido
esperando quince minutos de alguien.

**Regla**: la validación humana **no bloquea el avance**. Se acumula.

```text
El agente avanza hasta donde la PoC está técnicamente completa.
Lo único que queda pendiente es lo que un humano debe confirmar.
```

## 23.1 Dos estados distintos, nunca mezclados

| Estado | Qué significa | Quién lo pone |
|---|---|---|
| `IMPLEMENTADO` | El código corre, la instrumentación existe, la demo está desplegada. Nadie lo probó físicamente. | El agente |
| `VALIDADO` | Un humano lo ejecutó en hardware real y hay evidencia capturada. | El humano |
| `CERRADO` | Validado **y** con finding + decisión escritos. | El agente, con los datos del humano |

Un lab `IMPLEMENTADO` **no** cuenta como resuelto en `findings.md` ni en el
`CATALOGO`. Que el código corra no es evidencia — ver §7.

## 23.2 Qué sigue estando prohibido

Esta regla flexibiliza el *orden*, no la *honestidad*:

- No escribir en "Reflexiones" (§6.8) nada que no se haya observado.
- No marcar criterios de aceptación como cumplidos sin evidencia.
- No poner una decisión (§6.9) apoyada en una prueba que no ocurrió.

Un campo vacío es información válida. Un campo inventado corrompe todas
las decisiones que se apoyen en él.

## 23.3 La cola de validación

Cada exploración mantiene `VALIDACION-PENDIENTE.md` en su raíz: qué hay
que probar, en qué dispositivo, cuánto toma y qué labs desbloquea. Se
ordena por *cuánto avance libera por minuto de humano*, no por número de
lab.

El agente la actualiza al terminar cada lab. El humano la lee cuando tiene
un rato, ejecuta un bloque y devuelve la evidencia.

## 23.4 Consecuencia: instrumentar es prioritario

Si la validación humana es el recurso escaso, **abaratarla es trabajo de
primera clase**, no accesorio. Un lab que exige anotar once mediciones a
mano gasta más humano que uno que captura la evidencia solo y entrega un
reporte descargable.

Preferir siempre: que el sistema mida lo que puede medir, pregunte solo lo
que no puede deducir, y produzca la evidencia en un formato que el agente
pueda leer sin transcripción manual.

## 23.5 Cuándo sí hay que parar

La validación diferida tiene un límite: **no avanzar más allá de una
suposición que la validación pendiente podría destruir.**

```text
Seguir  →  el siguiente lab es independiente, o depende de algo ya validado.
Parar   →  el siguiente lab solo tiene sentido si la prueba pendiente sale bien.
```

Si A2 podría revelar que el tracking es inestable a un metro, A3 puede
implementarse igual — pero no puede *asumir* estabilidad a un metro en su
diseño. Cuando la duda pendiente cambia el diseño y no solo los números,
se para y se pide la validación.

---

# INPUT PARA UN NUEVO HILO

Cuando utilice este playbook en otro proyecto, proporcionaré debajo la siguiente información:

## Tema

[TECNOLOGÍA / IDEA / PRODUCTO QUE QUIERO EXPLORAR]

## Problema

[QUÉ QUIERO RESOLVER]

## Objetivo final

[QUÉ ME GUSTARÍA PODER CONSTRUIR]

## Tecnologías que actualmente sospecho que podrían participar

- [...]
- [...]
- [...]

Estas tecnologías son hipótesis.

Puedes proponer otras o descartar alguna.

## Restricciones conocidas

- [...]
- [...]

## Entorno disponible

Ejemplo:

```text
Windows
WSL
GitHub
AWS
Android/iPhone
etc.
```

## Nivel de profundidad deseado

Quiero:

```text
teoría básica necesaria
+
demos exploratorias
+
reflexiones
+
demos integrales
+
arquitectura emergente
```

No quiero inicialmente una implementación productiva.

---

# INSTRUCCIÓN FINAL

A partir del contexto proporcionado:

1. Define claramente el objetivo final.
2. Identifica las principales preguntas técnicas.
3. Identifica tecnologías y features a explorar.
4. Explica la teoría mínima necesaria de cada una.
5. Propón máximo tres laboratorios por tecnología.
6. Cada laboratorio debe incluir teoría, hipótesis, demo, observaciones y reflexiones.
7. Propón entre tres y cuatro demos integrales.
8. Relaciona explícitamente cada demo con el objetivo final.
9. Identifica capacidades nativas que puedan evitar desarrollo propio.
10. Mantén el proyecto compatible con Claude Code, Codex y otros coding agents.
11. No sobrearquitectes los laboratorios.
12. Utiliza los experimentos para evolucionar la arquitectura.
13. Termina proponiendo cuál debería ser el primer laboratorio a ejecutar.
