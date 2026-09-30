<<<<<<< HEAD
<div align="center">
  <h1>AIRAOS</h1>
  <p><i>IA asistente personal, multiplataforma, offline-first.</i></p>
  <p>
    <img src="https://img.shields.io/badge/python-%3E%3D3.10-blue" alt="Python">
    <img src="https://img.shields.io/badge/platform-Android%20%7C%20Windows%20%7C%20Linux-lightgrey" alt="Platforms">
    <img src="https://img.shields.io/badge/license-Apache%202.0-green" alt="License">
  </p>
</div>

---

## ¿Qué es AIRAOS?

**AIRAOS** es un asistente personal con avatar visual (**AIRA**) que funciona como una
capa de asistencia constante sobre el sistema: no es "una app más", sino un compañero
que escucha, recuerda y actúa.

- **Multiplataforma**: Android y PC (Windows, Linux, Linux Mint, Debian, KDE Neon).
- **Offline y online**: funciona con modelos locales (Ollama / LM Studio) o con
  proveedores remotos según la configuración del usuario.
- **Escalable por hardware**: adaptado a dispositivos de gama baja, media y alta.
- **Activable por voz**: *"Activate AIRA"*, *"Ayúdame AIRA"* o simplemente *"AIRA"*.

El proyecto evoluciona sobre la base de [OpenJarvis](https://github.com/open-jarvis/OpenJarvis),
un backend de asistente modular con primitivas de inteligencia componibles, del que
AIRAOS hereda la arquitectura y al que añade la capa de producto: identidad visual,
avatar, burbuja flotante y experiencia multiplataforma.

---

## Arquitectura

| Capa | Tecnología | Ubicación |
| --- | --- | --- |
| Backend (agente) | Python | `src/` |
| Interfaz web | React / Vite | `frontend/` |
| App de escritorio | Tauri (Rust) | `desktop/`, `frontend/src-tauri/` |
| Servidor en dispositivo | Loopback `127.0.0.1` | `src/openjarvis/server/` |
| Documentación | MkDocs | `docs/`, `mkdocs.yml` |
| Modelos locales | Ollama | `models/` (no versionado) |

El servidor corre **solo en loopback** y toda la información se guarda en el sandbox de
la aplicación: permisos mínimos, sin datos fuera del dispositivo por defecto.

---

## Identidad visual

- **Splash screen**: logo de 4 círculos unidos estilo Yin-Yang, morado oscuro y gris.
- **Burbuja flotante** estilo Siri/Hey Google: visible con la pantalla encendida o
  apagada, con pulso de color mientras escucha.
- **Paletas personalizables** por el usuario.
- **Avatar 3D VRM** (vestuario que cambia según hora, clima y región) y **avatar 2D
  chibi** disponibles como assets listos para integrar.

---

## Requisitos

- Python **3.10 – 3.13**
- [uv](https://docs.astral.sh/uv/) para gestión de dependencias
- Node.js 20+ (frontend y escritorio)
- Rust estable (solo para compilar Tauri)

---

## Puesta en marcha

```bash
# 1. Clonar
git clone https://github.com/Sandra2244/AIRAOS.git
cd AIRAOS

# 2. Entorno de Python
uv sync
source .venv/bin/activate        # Windows: .venv\Scripts\activate

# 3. Frontend
cd frontend && npm install && npm run dev
```

Los **pesos de modelo no se versionan** (son binarios de cientos de MB). Descárgalos
con Ollama en `models/` cuando los necesites:

```bash
ollama pull llama3.2
```

---

## Desarrollo

```bash
make test      # suite de pruebas
make lint      # lint y formato
make dev       # entorno de desarrollo completo
```

Convenciones de contribución en [`CONTRIBUTING.md`](CONTRIBUTING.md) y registro de
cambios en [`CHANGELOG.md`](CHANGELOG.md).

---

## Documentación

- Visión y roadmap técnico: [`AIRAOS_Vision_y_Roadmap.md`](AIRAOS_Vision_y_Roadmap.md)
- Documentación del sitio: `docs/` (se sirve con `mkdocs serve`)
- Arquitectura heredada de OpenJarvis: <https://open-jarvis.github.io/OpenJarvis/>

---

## Licencia

Apache 2.0 — ver [`LICENSE`](LICENSE).

Proyectos de referencia citados en el roadmap (Jenny/flagDiZero con licencia AGPL-3.0)
se toman como **inspiración arquitectónica**; el código de AIRAOS es propio.
=======
# AIRAOS
>>>>>>> 3c0c602ac840d6aa87d25bd09c34924a07df2f0e
