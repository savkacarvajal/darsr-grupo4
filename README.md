# DARSR — Sistema de Gestión de Migración Segura (TecnoNorte → AWS)

Sistema web que automatiza la gestión de la migración segura de la infraestructura on premise
de **TecnoNorte** hacia **AWS**, basado en un Sistema de Gestión de Seguridad de la Información
(SGSI) y una matriz de riesgos **R = P × I** (ISO/IEC 27001:2022).

**Asignatura:** Diseño de Arquitectura de Redes Seguras — INACAP La Serena
**Docente:** Daniel Ruz Moreno
**Grupo:** 4 _(reemplazar por el número de grupo)_
**Integrantes:** Savka Carvajal · Carlos Villarroel · Esteban Ardiles

- **Sistema publicado (Cloudflare Pages):** https://darsr-grupo4.pages.dev
- **Repositorio (GitHub):** https://github.com/savkacarvajal/darsr-grupo4
- **Datos del proyecto:** [`/data/proyecto-grupo4.json`](data/proyecto-grupo4.json)

> Reemplazar `N` / `grupo4` por el número de grupo asignado en: el nombre del repo, el subdominio
> de Cloudflare, el archivo de datos, la base `darsr_g4`, la VPC `10.4.0.0/16` y los IDs `R-G4-XX`.
> El número de grupo se edita dentro del propio sistema (módulo **② Alcance → Grupo (N)**) y se
> propaga automáticamente a toda la nomenclatura.

---

## Módulos del sistema

| # | Módulo | Función |
|---|---|---|
| ① | Resumen | Indicadores calculados automáticamente (activos, riesgos por nivel, controles, avance, riesgos sobre criterio) |
| ② | Alcance | Alcance del SGSI, objetivos y criterio de aceptación del riesgo |
| ③ | Inventario | Activos con tipo, zona, IP, servicio, clasificación y responsable |
| ④ | Identificación | Amenazas y vulnerabilidades por activo, con su evidencia |
| ⑤ | Matriz | Cálculo R = P × I, clasificación, matriz de calor 5×5 y priorización |
| ⑥ | Tratamiento | Opción de tratamiento + control del Anexo A ISO/IEC 27001:2022 y riesgo residual |
| ⑦ | Migración | Plan por etapas, arquitectura AWS, responsabilidad compartida y evidencias |
| ⑧ | Verificación | Resultados de pruebas y comparación residual vs. inherente |
| ⑨ | Política | Política general + políticas específicas (on premise / on cloud) |
| ⑩ | Documento | Generación automática del documento técnico en PDF |

Persistencia en el navegador (**localStorage**) + **exportación/importación JSON**.

---

## Escala de cálculo (Guía Didáctica)

**Riesgo = Probabilidad × Impacto** (1 a 5 cada uno).

| Nivel | Probabilidad (P) | Impacto (I) |
|---|---|---|
| 1 | Menos de 1 ataque al año en el sector | Menos de 50 usuarios, datos no clasificados |
| 2 | 1–2 ataques al año, vulnerabilidades menores | 50–500 usuarios, datos internos |
| 3 | 3–5 ataques al año, vulnerabilidades conocidas | 500–5.000 usuarios, datos personales |
| 4 | 6–10 ataques al año, intentos documentados | 5.000–50.000 usuarios, datos financieros o sistemas críticos |
| 5 | Más de 10 ataques al año o intentos activos | Más de 50.000 usuarios, operación paralizada o violación legal |

| Nivel de riesgo | Rango R | Acción |
|---|---|---|
| Bajo | 1 – 5 | Monitorear |
| Medio | 6 – 9 | Mejorar controles |
| Alto | 10 – 16 | Intervenir pronto |
| Crítico | 17 – 25 | Intervenir ya |

**Criterio de aceptación:** riesgo residual ≤ 9 aceptable; Alto/Crítico (> 9) obligan a tratar.

---

## Registro de validación (casos de prueba)

| Probabilidad | Impacto | Resultado esperado | Resultado obtenido |
|---|---|---|---|
| 4 | 5 | 20 · Crítico | ✔ 20 · Crítico |
| 2 | 3 | 6 · Medio | ✔ 6 · Medio |
| 3 | 5 | 15 · Alto | ✔ 15 · Alto |
| 4 | 4 | 16 · Alto | ✔ 16 · Alto |
| 1 | 5 | 5 · Bajo | ✔ 5 · Bajo |

---

## Modificaciones respecto de la actividad práctica base

Este sistema **amplía** la "Matriz de Riesgos" de la actividad práctica (CoopAndes Digital)
hasta una aplicación completa de gestión de la migración. Cambios principales:

- De una única vista de matriz a **10 módulos** navegables de un SGSI.
- **Panel de resumen** con indicadores automáticos (riesgos por nivel, controles, avance, riesgos sobre criterio).
- **Inventario de activos** e **identificación** de amenazas/vulnerabilidades con evidencia.
- **Catálogo de controles del Anexo A de ISO/IEC 27001:2022** integrado en el tratamiento.
- **Módulo de migración** (etapas, arquitectura AWS y responsabilidad compartida) y **verificación** con riesgo residual.
- **Política de seguridad** general + específicas, trazables a los riesgos.
- **Generación automática del documento técnico en PDF** a partir de los datos.
- **Exportación/importación en JSON** y persistencia en `localStorage`.
- Caso **TecnoNorte** precargado con falencias detectadas en el código, el script SQL y las especificaciones.

---

## Despliegue en Cloudflare Pages

1. Subir este repositorio a GitHub como `darsr-grupo4` (público).
2. En Cloudflare → **Workers & Pages** → crear aplicación de tipo **Pages** e importar el repositorio.
3. Configurar **sin framework**, **sin comando de build**, directorio raíz como salida.
4. Nombre del proyecto: `darsr-grupo4` → URL pública `https://darsr-grupo4.pages.dev`.
5. Cada `push` actualiza el sitio automáticamente.

## Uso local

Abrir `index.html` en cualquier navegador (Firefox o Chrome). No requiere servidor ni dependencias.

## Estructura

```
darsr-grupo4/
├── index.html                  # Sistema completo (HTML + CSS + JS, sin backend)
├── data/
│   └── proyecto-grupo4.json     # Datos del proyecto (export del sistema)
└── README.md
```
