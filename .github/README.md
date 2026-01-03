# Información relevante
❌ La plantilla NO viaja con el workflow reutilizable.

## 🧠 Regla fundamental de GitHub Actions (muy importante)

Cuando un repo hijo hace esto:

``` yml
uses: RiojaDevs/RiojaDevs_main_workflows/.github/workflows/assign_pr_reviewer.yml@main
```

- 👉 GitHub solo ejecuta ese archivo YAML
- 👉 NO clona el repo completo
- 👉 NO copia archivos auxiliares

Es decir:

- Se ejecuta el workflow
- Pero el contexto del repo es el repo hijo
- El action de Kentaro busca la plantilla en el repo actual

``` bash
.github/auto_assign.yml
```

Y no la encuentra si no esta ahi.

## 🧠 Modelo mental correcto
Workflow reutilizable  → vive en repo central
Configuracion runtime → vive en repo hijo


# SOLUCIÓN
Copiar los archivos a modo plantilla en cada repo hijo