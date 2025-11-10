# 🧪 GameCI_Devops

# 🎮 Unity CI/CD Templates (GameCI + GitHub Actions)

Este repositorio contiene **workflows reutilizables y parametrizables** para automatizar procesos de integración y despliegue en proyectos Unity, aprovechando [GameCI](https://game.ci), GitHub Actions y herramientas externas como Discord e Itch.io.

> 🎯 **Objetivo:** Centralizar y estandarizar la automatización de builds Unity (WebGL y Windows) entre múltiples repositorios, facilitando su mantenimiento y configuración.

---

## 🚀 ¿Qué ofrece este repositorio?

✅ Workflows listos para compilar proyectos Unity para:
- **WebGL**
- **StandaloneWindows64 (Windows)**

✅ Funcionalidades adicionales (opcionales y configurables):
- 🌐 **Publicación en Itch.io** (`publishToItch: true`)
- 🔔 **Notificaciones en Discord** (`sendToDiscord: true`)
- 📊 **Métricas de build** (tamaño, duración, estado, versión, etc.)
- 🧠 **Versionado automático** (`bundleVersion + Run + Entorno`)
- 📦 **Resúmenes automáticos** en Markdown y JSON

---

## 🧩 Arquitectura y Estructura

```txt
unity-ci-templates/
├── .github/
│   └── workflows/
│       ├── build-core.yml         # 🧠 Workflow principal configurable por inputs
│       ├── build-webgl.yml        # 🌐 Alias: llama a build-core con target WebGL
│       ├── build-windows.yml      # 💻 Alias: llama a build-core con target Windows
│       ├── notify-discord.yml     # 🔔 Subworkflow: notifica a Discord (modular)
│       └── publish-itchio.yml     # 🚀 Subworkflow: publica en Itch.io (solo WebGL)
└── README.md                      # 📘 Este documento
```
---

## 📊 Métricas generadas

El workflow genera automáticamente:
- Archivo metrics/build-metrics.json con datos útiles para análisis
- Resumen visible en el job de GitHub Actions con:
    - ✅ Estado
    - 🕒 Duración
    - 🧱 Tamaño de la build
    - 🌱 Rama
    - 🔗 Enlace al artifact

## 📌 Notas importantes

- El workflow base es `build-core.yml`, que incluye toda la lógica.
- Los alias (`build-webgl.yml`, `build-windows.yml`) solo lo invocan con parámetros predefinidos.
- Los subworkflows (notify-discord.yml y publish-itchio.yml) están separados y modulares para máxima reutilización.

## Ejemplo WebGL
```yml
# .github/workflows/build-webgl.yml
name: Example - Build WebGL

on:
  workflow_dispatch:
  push:
    branches:
      - PRE_PRODUCCION
      - PRODUCCION

jobs:
  build-webgl:
    uses: Pax16gamedev/TestGameCI_DevOps/.github/workflows/build-webgl.yml@DESARROLLO
    secrets: inherit
    with:
      sendToDiscord: false
      publishToItch: true
      itchioChannel: "pax16/test-devops:webgl"    
```

---

## Ejemplo Windows
```yml
# .github/workflows/build-windows.yml
name: Example - Build Windows

on:
  workflow_dispatch:
  push:
    branches:
      - PRE_PRODUCCION
      - PRODUCCION

jobs:
  build-windows:
    uses: Pax16gamedev/TestGameCI_DevOps/.github/workflows/build-windows.yml@DESARROLLO
    with:
      unityVersion: 6000.2.10f1
      sendToDiscord: true
    secrets: inherit
```