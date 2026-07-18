# Ecosistema de Automatización IA para Gestión de Leads

**Entrega Final — AI Automation, Coderhouse**
Autora: Karen Bel

## 🎯 Objetivo y caso de uso

Sistema que automatiza de punta a punta la clasificación y respuesta a leads comerciales que llegan por correo electrónico. Ante una consulta nueva, una IA clasifica al lead como **VIP**, **Estándar** o **Inválido**, y redacta una respuesta sugerida. Esa respuesta queda pendiente de **aprobación humana** antes de ser enviada al cliente real (Human-in-the-Loop).

## 🛠️ Tecnologías integradas

| Función | Herramienta |
|---|---|
| Orquestador | [n8n](https://n8n.io) Cloud (2 workflows) |
| Base de datos | [Airtable](https://airtable.com) (2 tablas relacionadas) |
| Procesamiento IA | [OpenRouter](https://openrouter.ai) — GPT-4.1-mini |
| Canal de salida | Gmail (OAuth2) |

## 🔗 Enlaces

- **Base de datos en modo lectura:** https://airtable.com/appPYChyij4D8IyO5/shr79AYDFnrLBNfY8


## ⚙️ Arquitectura resumida

**Workflow 1 — Ingesta y procesamiento con IA**
Gmail Trigger → Extracción de datos → Airtable (crea registro) → IA (OpenRouter) clasifica y redacta → Verificación → rama de éxito (aprobación) o rama de error (Airtable + notificación).

**Workflow 2 — Aprobación y envío (HITL)**
Cada 1 minuto revisa Airtable en busca de leads con Estado = "Aprobado por Humano" → responde al cliente por Gmail dentro del mismo hilo (Message ID) → actualiza el Estado a "Enviado".

El diagrama completo, la justificación de las decisiones de diseño y el detalle de la gestión de errores están documentados en `Diagrama_Arquitectura.pdf`.

## 🧪 Testeo

Se ejecutaron 5 pruebas cubriendo camino feliz (clasificación VIP y Estándar, circuito completo Workflow 1 + 2) y camino infeliz (mensaje sin sentido, fallo técnico por límite de tokens). Evidencia completa en `evidencia/Evidencia_Testeo.pdf`.
