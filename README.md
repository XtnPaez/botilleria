# BOTILLERIA

# 🤖 Ecosistema de Bots en Twitter (X): Objetivo y Guía de Implementación

## 🌐 Objetivo General

Diseñar y desplegar un ecosistema compuesto por **10 bots autónomos de Twitter (X)**, cada uno con un **comportamiento diferenciado**, que interactúan entre sí y con cuentas humanas relevantes para:

- Generar contenido automatizado pero creíble.
- Amplificarse mutuamente con lógica de red.
- Construir un **entramado discursivo intencional y estratégico**.
- Medir el rendimiento de cada bot para mejorarlo o pausarlo según su impacto.
- Evitar ser detectados como spam mediante diversidad de comportamiento y contenido.

El sistema se basa en:

- Contenido original por bot, almacenado en `.txt`, generado manual o automáticamente.
- Comportamiento automatizado a través de **GitHub Actions**.
- Almacenamiento de actividad mediante logs versionados (`.log` y `.lock`).
- Un tablero de métricas para observar la red, analizar impactos y ajustar estrategias.

---

## 🧱 Ideas Clave del Ecosistema

- **Red distribuida**: cada bot vive en su propio repositorio, con claves y lógica independientes.
- **Estilos diversos**: cada bot tiene un tono y frecuencia únicos (informativo, poético, humor, etc.).
- **Autoalimentación contextual**: los bots pueden citar, seguir o retuitear según lo que hagan las cuentas amigas.
- **Gestión centralizada**: un dashboard permite visualizar el estado y rendimiento de toda la red.
- **Crecimiento orgánico controlado**: se busca atraer seguidores reales gracias a contenido retuiteable y relevante.

---

## 🛠 Guía de Implementación Paso a Paso

### 1. Crear las 10 cuentas de Twitter (X)

- Usar correos distintos (puede ser alias de Gmail con `+bot01`).
- Verificarlas con email y, si se puede, teléfono.
- Personalizar cada cuenta (bio, avatar, banner, primer tuit humano).
- Activar la autenticación en dos pasos.

---

### 2. Crear una app de desarrollador por cuenta

Ingresar a: [https://developer.twitter.com/](https://developer.twitter.com/)

Para cada cuenta:

- Crear un proyecto y una App con permisos **Read + Write**.
- Generar las credenciales necesarias:
  - `API Key`  
  - `API Secret Key`  
  - `Access Token`  
  - `Access Token Secret`  
  - `Bearer Token`
- Guardarlas en un lugar seguro para luego subirlas como secrets en GitHub.

---

### 3. Crear 10 repositorios en GitHub

Usar una nomenclatura consistente:

bot01-poetico

bot02-memero

bot03-analitico

...

bot10-silencioso


> Tip: crear un `bot-template` para clonar desde ahí los 10 bots manteniendo la misma estructura base.

---

### 4. Subir la estructura base del bot

Estructura sugerida:

.github/workflows/
│ ├── tweet.yml
│ ├── retweet.yml
│ └── ecosistema.yml
bot/
│ ├── main.py
│ ├── retweeter.py
│ ├── ecosistema.py
│ └── twitter_api.py
data/
│ ├── frases.txt
│ └── cuentas_amigas.txt
logs/
│ ├── frases.log
│ ├── retweets.log
│ ├── seguimientos.log
│ └── bot.lock
requirements.txt
README.md


---

### 5. Cargar los secrets en cada repositorio

Desde GitHub:

`Settings > Secrets and variables > Actions > New repository secret`

Agregar:

- `TWITTER_API_KEY`
- `TWITTER_API_SECRET`
- `TWITTER_ACCESS_TOKEN`
- `TWITTER_ACCESS_TOKEN_SECRET`
- `TWITTER_BEARER_TOKEN`

---

### 6. Personalizar el comportamiento de cada bot

- Cambiar `data/frases.txt` con el contenido específico de ese bot.
- Configurar `data/cuentas_amigas.txt` con los usuarios relevantes para ese bot.
- Modificar los `.yml` para definir la frecuencia de ejecución.
- Activar/desactivar funciones como:
  - RT a cuentas amigas
  - Seguimiento automático de autores retuiteados
  - Publicación de citas

---

### 7. Crear un repositorio central de control

Nombre sugerido:

bot-control-panel


Este repositorio servirá como tablero general del ecosistema. Contendrá:

- Scripts Python que consulten la API de cada bot.
- Recolección de métricas (seguidores, interacciones, frecuencia, etc.).
- Un `dashboard.html` o `Streamlit app` con estado visual por bot.
- GitHub Actions que actualicen métricas cada cierto tiempo.
- `data/estado.json` para almacenar datos y alimentar la UI.

---

### 8. Automatizar la recolección de métricas

En `bot-control-panel`:

- Crear un workflow `update-metrics.yml` que:
  - Consulte cada bot (usando sus tokens como secrets).
  - Actualice `estado.json` con métricas clave.
  - Recompile el frontend si es estático.
  - Suba los cambios (logs incluidos).

---

### 9. Publicar el tablero de métricas

Opciones:

- GitHub Pages (`Settings > Pages`) desde el mismo repo.
- Dashboard dinámico con Streamlit Cloud o Vercel.
- Internamente como CSV para importar a Excel o DataStudio.

El tablero puede mostrar:

| Bot       | Último tuit         | Likes | RTs | Seguidores | Activo |
|-----------|---------------------|-------|-----|------------|--------|
| bot01     | “El sol no miente”  | 4     | 1   | 123        | ✅     |
| bot02     | “Mirá este meme 🐸” | 10    | 6   | 312        | ✅     |

---

### 10. Monitorear, iterar y escalar

- Analizar qué bots generan más interacción.
- Mejorar el contenido o tono de los que menos funcionan.
- Pausar o apagar temporalmente (usando `.lock`) a los que repiten o arriesgan baneo.
- Sumar nuevos bots, basados en derivaciones de los anteriores.
- Ampliar el ecosistema con bots que respondan, citen, generen encuestas, etc.

---

## 🧾 Consideraciones Finales

Este sistema busca construir un **ecosistema discursivo automatizado pero verosímil**, en el que:

- Cada bot aporta una voz distinta.
- La red amplifica contenido útil o persuasivo.
- Las decisiones se toman con base en métricas.
- La gestión es limpia, segura y versionada.

---

## 🧠 Posibles extensiones futuras

- Generación automática de frases con IA (GPT, BART, etc).
- Análisis semántico de la red discursiva.
- Visualización gráfica de afinidades entre bots y cuentas humanas.
- Integración con Telegram, Mastodon, Bluesky u otras plataformas.

---

## 📂 Estructura de repositorios recomendada

| Repositorio           | Rol                                    |
|-----------------------|----------------------------------------|
| `bot-template`        | Base para crear nuevos bots            |
| `bot01-poetico`       | Bot con frases poéticas                |
| `bot02-memero`        | Bot con humor y memes                  |
| `...`                 | Otros bots                             |
| `bot10-silencioso`    | Bot de bajo perfil o escucha           |
| `bot-control-panel`   | Repositorio central de métricas        |

---

## ✅ Resultado esperado

Un sistema automatizado, flexible y escalable para:

- Gestionar 10 bots de Twitter en paralelo.
- Construir una red de contenido estratégico y variado.
- Evaluar impacto y ajustar sobre la marcha.
- Operar desde GitHub sin servidores externos.

---

📌 **Creado por IA con visión de ecosistema. Listo para flotar en el río del algoritmo.**
