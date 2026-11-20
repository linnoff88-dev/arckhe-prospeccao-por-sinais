# 📡 Prospección por Señales

[![Prospección por Señales](guia/assets/banner-es.jpg)](https://inematds.github.io/prospeccao-por-sinais/guia/es/)

**🇧🇷 [Português](README.md) · 🇺🇸 [English](README.en.md) · 🇪🇸 [Español](README.es.md)**

## Qué es

Este es un kit gratuito para quienes venden a empresas y quieren prospectar sin enviar correos a listas frías. La idea es buscar **señales**, es decir, acontecimientos públicos que muestran que una empresa puede necesitarte ahora (una vacante abierta, un producto lanzado, un nuevo director), y solo entonces encontrar a la persona que toma las decisiones y escribir un mensaje que mencione esa señal. Claude Code hace el trabajo pesado usando Clay (una plataforma de datos de empresas y contactos) y te entrega una hoja de cálculo para que la revises. Necesitas Claude Code, una cuenta de Clay (hay un plan gratuito y un período de prueba) y una tarde para completar el contexto de tu negocio.

## 📖 Guía de uso

Guía completa (página de presentación + paso a paso): **https://inematds.github.io/prospeccao-por-sinais/guia/es/**

## Antes de empezar

- **Claude Code** ≥ 2.1.91 (requiere una suscripción paga de Claude): `curl -fsSL https://claude.ai/install.sh | bash` (Mac/Linux), `irm https://claude.ai/install.ps1 | iex` (Windows) o `npm install -g @anthropic-ai/claude-code` — docs: https://docs.claude.com/en/docs/claude-code/overview
- **Una cuenta en Clay** (plan gratuito o prueba de 14 días).
- **git** (o descarga el [.zip](https://github.com/inematds/prospeccao-por-sinais/archive/refs/heads/main.zip)) y, solo para la skill opcional de señales, **Node.js** (`npx`).

## El proceso, de principio a fin

Quién hace qué: 🧠 tú en Claude Code · ⚙️ Clay/script · 🤖 agente (Claude Code trabajando por su cuenta)

| # | Paso | Comando | Quién |
|---|-------|---------|------|
| 1 | Descargar el kit y abrir Claude Code en la carpeta | `git clone https://github.com/inematds/prospeccao-por-sinais.git` · `cp -r prospeccao-por-sinais/kit ~/minha-prospeccao` · `cd ~/minha-prospeccao` · `claude` | 🧠 |
| 2 | Instalar el plugin de Clay (Claude Code ≥ 2.1.91) | `/plugin marketplace add clay-run/agent-plugins` · `/plugin install clay@clay-plugins` · "Ejecuta la habilidad clay:setup" | 🧠 |
| 3 | Completar el contexto del negocio | editar `contexto/*.md` (modelo en `contexto/exemplo/`) | 🧠 |
| 4 | Definir las señales | editar `sinais.yaml` · opcional: `npx skills add clay-run/clay-skill-creator --skill customer-signal-generator` | 🧠 + 🤖 |
| 5 | ICP: lista de empresas (primero 10 filas) | Paso 1 de `prompts/passo-a-passo.md` | 🤖 + ⚙️ |
| 6 | Señal de contratación monitoreada | Paso 2 | 🤖 + ⚙️ |
| 7 | Agente de investigación (lanzamiento de producto) | Paso 3 | 🤖 + ⚙️ |
| 8 | Persona que decide solo donde hay una señal (condición de ejecución: la suma de los pesos de las señales activas es 30 o más) | Paso 4 | 🤖 + ⚙️ |
| 9 | Correo en cascada + verificación | Paso 5 | ⚙️ |
| 10 | Mensaje contextualizado (asunto + cuerpo que menciona la señal) | Paso 6 — o todo de una vez con `/goal` (`prompts/goal-prospeccao.md`) | 🤖 |
| 11 | CSV final para revisión | `saida/leads-AAAA-MM-DD.csv` (columnas en `colunas-csv.md`) | 🤖 |
| 12 | Revisión humana | leer las filas con `revisar = sim`, corregir | 🧠 |
| 13 | Importar en el secuenciador y enviar despacio | importar CSV → campaña; dominio secundario con buena reputación, pocos envíos al día, spam < 0,3 % | 🧠 + ⚙️ |
| 14 | Supresión | quien pidió salir se agrega a `supressao.csv` ese mismo día | 🧠 |

Regla de oro (está en `kit/CLAUDE.md`): el agente **nunca gasta créditos sin pedir permiso**, **ejecuta 10 filas primero** y **nunca envía nada**.

## El kit

Los archivos del kit están en portugués (Claude Code los lee en cualquier idioma; traduce los modelos si lo prefieres).

```
kit/
├── CLAUDE.md                 reglas del agente (créditos, 10 filas, revisión, exclusión voluntaria, LGPD)
├── contexto/                 6 modelos: perfil-do-negocio, oferta, casos, provas, faq, tom-de-voz
│   └── exemplo/              los mismos 6, completados con una empresa FICTICIA
├── prompts/
│   ├── goal-prospeccao.md    prompt para /goal con un criterio de finalización verificable
│   └── passo-a-passo.md      un prompt por paso del flujo
├── sinais.yaml               señales de ejemplo con período de validez y peso
├── colunas-csv.md            columnas de la hoja de cálculo de salida
├── checklist-lgpd.md         lista práctica de verificación (no es una opinión legal)
└── supressao.csv             quienes pidieron salir
```

## Costos (documentación pública de Clay, verificada el 01/11/2026)

- Gratis: 100 créditos al mes. Prueba de 14 días: 1.000 créditos. Plan Launch: desde US$ 185 al mes (2.500 créditos + 15.000 acciones).
- En la cascada, los proveedores estándar de correo electrónico y teléfono celular devuelven el crédito si no encuentran datos; el teléfono celular no está disponible en el plan gratuito ni en la prueba.
- Fuente: https://github.com/clay-run/public-docs

## Referencias

- Plugin de Clay para agentes: https://github.com/clay-run/agent-plugins
- Gmail — pautas para remitentes: https://support.google.com/a/answer/81126?hl=es
- LGPD (Ley brasileña 13.709/2018 de protección de datos personales): https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm · ANPD (autoridad brasileña de protección de datos): https://www.gov.br/anpd

---

Contenido abierto y gratuito de [INEMA.CLUB](https://inema.club).