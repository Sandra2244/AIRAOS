# AIRAOS — Documento de Visión y Roadmap Técnico

> Documento de referencia para el equipo (colaboradores + copilotos de IA). Redactado a partir de las notas originales del proyecto, organizado por módulos y fases para que sea ejecutable.

---

## 1. Concepto central

**AIRAOS** es una IA asistente personal, multiplataforma (Android + PC: Windows, Linux, Linux Mint, Debian, KDE Neon), con un avatar visual (**AIRA**), pensada para funcionar offline y online, adaptable a dispositivos de gama baja, media y alta.

No es una app más: sustituye/convive con el sistema operativo como capa de asistencia constante — inspirada en el concepto de un JARVIS/ULTRON personal, pero con un enfoque realista y modular en vez de "hacerlo todo desde el día uno".

**Nombre del sistema:** AIRAOS (reemplaza cualquier branding de los proyectos base).
**Avatar/asistente:** AIRA.
**Frase de activación:** "Activate AIRA" / "Ayúdame AIRA" / "AIRA".

---

## 2. Identidad visual

- **Splash screen** al iniciar: fondo con logo de **4 círculos unidos estilo Yin-Yang**, tonos morado oscuro y gris, texto "AIRAOS".
- **Burbuja flotante** (estilo Siri/Hey Google): aparece con pantalla encendida o apagada, gira/pulsa con colores mientras escucha (paleta morado, gris, azulado por defecto — configurable).
- Paletas de color e interfaz completamente personalizables por el usuario.
- Avatar disponible en **modelo 3D VRM** (con vestuario que cambia según hora, clima, región y país detectado) y **modelo 2D chibi** — ambos ya existen como asset, listos para integrar.

---

## 3. Proyectos de referencia (para inspirarse en arquitectura, NO copiar código literal)

### 3.1 Jenny (flagDiZero) — github.com/flagdizero/jenny-android-ai-agent
- Licencia **AGPL-3.0** → si se reutiliza código, el fork también debería ser AGPL. Recomendado: tomar solo **ideas de arquitectura**, escribir código propio.
- Lo más valioso a inspirar en AIRAOS:
  - Servicio en **foreground** que mantiene al agente vivo con pantalla apagada.
  - Registro como actividad **HOME** opcional (pantalla de inicio = conversación).
  - **Memoria persistente en Markdown** en disco (resúmenes periódicos de la conversación).
  - Sistema de **mini-apps generadas por el propio agente** (UI + acciones + almacenamiento).
  - Conexión a modelos locales (Ollama/LM Studio) para funcionar 100% offline, o a un proveedor con API key propia del usuario.
  - Seguridad: todo el almacenamiento en sandbox de la app, servidor solo en loopback (127.0.0.1), permisos mínimos.

### 3.2 JARVIS-HRZ (PC, Windows/Android gama baja 3GB+ RAM)
- Control total del sistema por comandos (apagar, abrir apps, automatizar).
- Generación de documentos Word/Excel/PPTX por instrucciones.
- Control remoto vía **Telegram** (bot propio).
- Integración con **GitHub** (crear ramas, commits, push por comando de voz/texto).
- Rutinas matutinas (clima, agenda, tareas pendientes).
- Tareas, recordatorios y alarmas con contexto (ubicación/hora).
- Integración con **Google Calendar** y **Gmail** (crear eventos, enviar correos por voz).
- Noticias internacionales en varios formatos.

### 3.3 JARVIS Linux
- Mismo enfoque que JARVIS-HRZ pero pensado para distros Linux (aún sin build oficial — parte pendiente de crear desde cero).

### 3.4 Referencia de arquitectura "estilo Ultron/Jarvis real" (demo mencionada)
- UI construida con herramientas tipo Claude Design (Next.js).
- Seguimiento de manos/gestos vía cámara (tipo "Air Touch").
- Orquestación de herramientas vía un "arnés de agente" (LLM + acceso a herramientas, ej. frameworks tipo Hermes).
- Voz: motor de voz + capa opcional de voces realistas (ej. ElevenLabs) encima.
- **Nota:** esto son demos de investigación/hobby, no productos estables — usar como inspiración de arquitectura, no como dependencia directa.

---

## 4. Módulos funcionales (agrupados por sistema)

### A. Núcleo del agente (IA)
- Motor conversacional por texto y voz.
- Conexión a múltiples proveedores de modelos (Gemini, Qwen, DeepSeek, WAN para imagen/video, etc.), con **API keys cifradas** para que el usuario final no exponga sus llaves.
- Sistema de fallback: si un modelo falla, cambia automáticamente a otro disponible.
- Memoria a largo plazo (perfil del usuario, preferencias, historial, PDFs subidos).
- Personalidad/arquetipo configurable (formal, cercana, predeterminada equilibrada).
- Filtro moral base, ajustable según el nivel de confianza/contexto con el usuario.

### B. Interacción
- Burbuja flotante multiplataforma (Android + multiventana en PC).
- Entrada por voz y texto.
- Reconocimiento de gestos de mano vía cámara (PC y Android) para control sin contacto.
- Desbloqueo por reconocimiento/gestos (evaluar viabilidad real por plataforma — en Android esto requiere permisos especiales).
- Cambio de voces descargables (como el selector de voces de Siri).

### C. Productividad
- Generación/edición de documentos Word, Excel, PowerPoint, PDF.
- Integración con Microsoft Office y (opcional) Canva.
- Apoyo de estudio: aplica métodos (Feynman, Kaizen, Pomodoro, Active Recall/flashcards) según la carrera/tema, con recordatorios y alarmas automáticas en calendario.
- Generación y edición de imágenes (retratos, estilos variados) bajo demanda.
- Historial de conversaciones, "cuadernos" y exportación a PDF.

### D. Multimedia
- Reproductor de música/video con soporte de letras/fotogramas, minimizable en lateral de pantalla (PC) sin interrumpir otras tareas.
- Reproducción en segundo plano con pantalla apagada (Android) manteniendo control visual mínimo.
- Descargador universal de video/audio (estilo Snaptube/Amerigo) activable por burbuja o por comando de voz.
- Organización automática de música en carpetas por estilo/gusto.

### E. Sistema y seguridad
- Optimización de batería, RAM y memoria virtual (especial foco en gama baja).
- Modo juego (rendimiento) para Android/PC.
- Protección tipo antivirus/anti-spyware, cifrado extremo a extremo de datos guardados.
- Auto-diagnóstico y auto-reparación básica ante errores.
- Conocimientos de ciberseguridad aplicada (protección anti-hacking a nivel usuario).

### F. Multiplataforma
- Android: gama baja (3GB RAM) a alta.
- PC: Windows, Linux (Mint, Debian, KDE Neon Plasma).
- Integración con apps ya instaladas en el dispositivo en vez de duplicar funcionalidad cuando sea posible.

---

## 5. Stack tecnológico (decisión del equipo: HTML + JavaScript + C++)

Los colaboradores propusieron **HTML, JavaScript y C++** como base. Es una decisión sólida y usada en la industria — aquí se explica el rol de cada pieza para que el equipo trabaje coordinado:

| Capa | Tecnología | Rol en AIRAOS |
|---|---|---|
| Interfaz (Android + PC) | **HTML + JavaScript**, empaquetado con **Electron** (PC) y **Capacitor** (Android) | Un mismo código de interfaz para ambas plataformas: chat, burbuja flotante, paneles de configuración. Aprovecha directamente el JavaScript que ya estás aprendiendo. |
| Avatar 3D (VRM) | **three-vrm** (librería JavaScript sobre Three.js) | Librería estándar de la industria para cargar y animar modelos VRM en web/JS — encaja de forma directa con el avatar 3D que ya tienes. |
| Avatar 2D chibi | Motor ligero en JS (sprite-based o Live2D Web SDK) | Más simple de integrar primero, antes de pasar al 3D. |
| Módulos de rendimiento e IA local | **C++**, expuesto a JavaScript como módulo nativo (Node native addon en Electron / JNI en Android) | Aquí van las partes pesadas: reconocimiento de gestos por cámara (ej. OpenCV), inferencia de modelos de IA offline (ej. llama.cpp), optimización de batería/RAM a bajo nivel. |
| Backend/IA en la nube | Llamadas a APIs (Gemini, OpenRouter, etc.) desde JavaScript | Empezar con un solo proveedor y añadir fallback automático después. |
| Memoria persistente | Archivos Markdown/JSON locales | Igual que Jenny — simple, portable, fácil de respaldar. |

**Reparto de roles sugerido para el equipo:**
- **JavaScript/HTML** → interfaz, lógica de la app, integración del avatar (three-vrm), conexión a las APIs de IA.
- **C++** → módulo de rendimiento, gestos por cámara, IA local offline.
- Ambos módulos se comunican entre sí mediante una capa de "puente nativo" (bindings), que se define en la Fase 0.

---

## 6. Roadmap por fases (de lo simple a lo completo)

**Fase 0 — Fundación (recomendado empezar aquí)**
- Proyecto base en HTML/JavaScript, empaquetado con Electron (PC) y Capacitor (Android) — misma interfaz para ambas plataformas.
- Definir la estructura del "puente nativo" entre JavaScript y el futuro módulo en C++ (aunque el módulo en C++ esté vacío al inicio).
- Pantalla splash con el logo AIRAOS.
- Integrar el avatar chibi 2D (más simple) respondiendo con animaciones básicas, antes de pasar al 3D con three-vrm.

**Fase 1 — Conversación básica**
- Chat de texto conectado a un solo modelo (ej. Gemini o el que tengas API key).
- Burbuja flotante básica (overlay en Android / ventana flotante en PC).

**Fase 2 — Voz y memoria**
- Entrada/salida de voz.
- Memoria persistente simple (perfil + historial resumido).

**Fase 3 — Productividad**
- Generación de documentos.
- Recordatorios/calendario.

**Fase 4 — Multimedia**
- Reproductor con letras/fotogramas.
- Descargador de video.

**Fase 5 — Avatar 3D VRM completo + gestos por cámara**

**Fase 6 — Sistema/seguridad avanzada** (antivirus, optimización, auto-reparación)

**Fase 7 — Multiplataforma completa** (Linux nativo, control remoto tipo Telegram, GitHub ops)

> Cada fase debe compilar y probarse antes de pasar a la siguiente. No se avanza de fase con código que "no corre".

---

## 7. Notas para colaboradores

- Los assets visuales (**modelo 3D VRM** y **modelo 2D chibi**) ya están listos — falta decidir el motor de render antes de integrarlos (ver tabla de stack).
- Quien lidera el proyecto está aprendiendo JavaScript actualmente — el lado de PC (Electron) es donde ese aprendizaje aplica directo; el lado Android requiere Kotlin (se puede aprender en paralelo o delegar a otro colaborador).
- Evitar duplicar trabajo de los proyectos de referencia (Jenny, JARVIS-HRZ): tomar patrones de arquitectura, escribir implementación propia.
- Priorizar avanzar por fases pequeñas y funcionales antes que intentar construir varios módulos en paralelo.
