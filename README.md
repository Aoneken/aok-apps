# 🚀 AOK Apps – Plataforma de Soluciones Técnicas

[![GitHub](https://img.shields.io/badge/GitHub-Aoneken%2Faok--apps-blue?logo=github)](https://github.com/Aoneken/aok-apps)
[![Node.js](https://img.shields.io/badge/Node.js-v22.17.0-green?logo=node.js)](https://nodejs.org/)
[![Docker](https://img.shields.io/badge/Docker-28.3.1-blue?logo=docker)](https://www.docker.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Ready-blue?logo=postgresql)](https://www.postgresql.org/)

> **Repositorio raíz de 4 aplicaciones con sinergias técnicas.**  
> Entorno: GitHub Codespaces | Stack: Node.js, PostgreSQL, Docker | IA: GitHub Copilot

---

## 📊 Informe Técnico del Entorno (Codespace)

### Información General
- **Nombre:** `gory-phantom-7vx6r4jxjrwwhrg79`
- **SO:** Ubuntu 24.04.2 LTS (Noble Numbat)
- **Kernel:** Linux 6.8.0-1030-azure
- **Hardware:** 2 vCPU (AMD EPYC 7763), 8 GB RAM, 32 GB disco
- **Docker:** 28.3.1 (DinD habilitado)
- **GitHub CLI & Copilot:** Integrados

### 💻 Lenguajes y Herramientas

| Lenguaje | Versión |
|---------|--------|
| Node.js | v22.17.0 |
| Python  | 3.12.1 |
| Ruby    | 3.4.1 |
| PHP     | 8.3.14 |
| Java    | OpenJDK 21.0.7 LTS |
| Go      | 1.24.5 |

| Herramienta | Versión |
|------------|---------|
| Git        | 2.50.1 |
| Docker     | 28.3.1 |
| kubectl    | v1.33.2 |
| Helm       | v3.18.4 |
| GitHub CLI | 2.75.0 |

> 📄 Ver [Informe_Completo_Inicial_del_Codespace.md](Informe_Completo_Inicial_del_Codespace.md) para detalles completos del entorno.

---

## 🎯 Proyectos Incluidos

| # | Proyecto | Descripción | Repo Sugerido |
|---|---------|-------------|---------------|
| 1️⃣ | **Reservas Deportivas** | Sistema multi-app: admin de instalaciones + app de jugadores con reservas, mensajería y reseñas | `reservas-admin`, `reservas-jugadores` |
| 2️⃣ | **Gestión Financiera** | Plataforma contable para individuos/pymes: cajas, inversiones (acciones, bonos, cripto), dividendos | `gestion-financiera` |
| 3️⃣ | **Data Scraper** | Sistema de ingesta y almacenamiento de datos desde fuentes digitales (boletines, noticias, informes) | `data-scraper` |
| 4️⃣ | **Channel Manager** | Sincronizador de calendarios vía API (Airbnb, Booking, Expedia) con bloqueo automático | `channel-manager` |

---

## 🔗 Sinergias Técnicas (Enfoque Constructivo)

### Componentes Reutilizables

#### 🔐 Autenticación y Gestión de Usuarios
- **Módulo compartido:** JWT + OAuth con roles y perfiles
- **Sinergias:** Proyectos 1 y 2 (perfiles sociales/financieros), Proyectos 3 y 4 (autenticación API)

#### 🏗️ Backend y Arquitectura
- **Stack común:** Node.js/Express o Python/FastAPI
- **Sinergias:** Proyectos 1 y 4 (calendarios en tiempo real con Redis), Proyectos 2 y 3 (ETL batch)

#### 🗄️ Modelos de Bases de Datos
- **BD primaria:** PostgreSQL (estructurada)
- **BD secundaria:** MongoDB (semi-estructurada, opcional)
- **Sinergias:** Proyectos 1 y 4 (esquemas para eventos temporales), Proyectos 2 y 3 (time-series)

#### 📢 Servicios Compartidos
- **Notificaciones:** Firebase/SendGrid para email + push
- **Integraciones API:** Servicios de terceros
- **Sinergias:** Proyectos 1 y 4 (mensajería), Proyectos 2 y 3 (alertas basadas en scraping)

### 📊 Tabla de Sinergias por Pareja

| Componente / Pareja | 1 y 2 | 1 y 3 | 1 y 4 | 2 y 3 | 2 y 4 | 3 y 4 |
|---------------------|-------|-------|-------|-------|-------|-------|
| Autenticación       | 🔴 Alta | 🟡 Media | 🔴 Alta | 🟡 Media | 🟢 Baja | 🟢 Baja |
| Backend/API         | 🟡 Media | 🟡 Media | 🔴 Alta | 🔴 Alta | 🟢 Baja | 🔴 Alta |
| Modelos BD          | 🔴 Alta | 🟡 Media | 🔴 Alta | 🔴 Alta | 🟡 Media | 🟡 Media |
| Servicios           | 🔴 Alta | 🔴 Alta | 🔴 Alta | 🔴 Alta | 🟡 Media | 🔴 Alta |

### 🛠️ Stack Común Recomendado

```yaml
Backend: Node.js + Express (o Python + FastAPI)
ORM: Prisma (Node.js) / SQLAlchemy (Python)
BD Principal: PostgreSQL
Cache: Redis (para calendarios y sesiones)
Mensajería: Bull/BullMQ (Node.js) para colas
Notificaciones: SendGrid (email) + Firebase (push)
Deploy: Docker + Railway/Render/AWS
CI/CD: GitHub Actions
```

---

## 📁 Arquitectura de Repositorios (Decisión Final)

### ✅ Estrategia: Multirepo por Aplicación

**Ideal para principiantes** – Simplicidad, aislamiento de errores, deploys independientes.

```bash
proyectos/
├── reservas-admin/          # App admin de reservas deportivas
├── reservas-jugadores/      # App jugadores (reservas + mensajería)
├── gestion-financiera/      # Plataforma financiera completa
├── data-scraper/            # Sistema de ingesta de datos
└── channel-manager/         # Sincronizador de calendarios
```

### 🔄 Reutilización de Código
- **Fase 1:** Mismo stack en todos los proyectos (copy-paste inicial)
- **Fase 2:** Crear repo `shared-libs` para paquetes npm comunes (auth, db-models, notifications)
- **Mitigación de riesgos:** Multi-tenancy en BD para aislar datos

### 📦 Estructura de Cada Repositorio (Plantilla)

```bash
reservas-admin/
├── src/
│   ├── routes/           # Definición de endpoints
│   ├── controllers/      # Lógica de negocio
│   ├── models/           # Modelos de datos
│   ├── middleware/       # Auth, validación, logs
│   └── services/         # Servicios externos (email, cache)
├── prisma/
│   └── schema.prisma     # Esquema de BD
├── tests/                # Tests unitarios e integración
├── .env.example          # Variables de entorno
├── package.json
├── Dockerfile
├── docker-compose.yml
├── .github/
│   └── workflows/        # GitHub Actions
└── README.md
```

---

## 🤖 Flujo de Trabajo con IA

### Roles Definidos

1. **🧠 Grok (Ingeniero Senior)** → Baja instrucciones en lenguaje natural
   - Ejemplo: *"Crea un backend en Node.js con Express para autenticación JWT en `reservas-admin`"*

2. **📨 Tú (Mensajero)** → Copias instrucciones a **GitHub Copilot**
   - Seleccionas modelo según la tarea

3. **⚡ GitHub Copilot** → Genera código en el Codespace
   - Implementa, prueba y ajusta

4. **💾 Commit & Push** → Subes cambios a GitHub
   - Grok verifica en el repositorio remoto

5. **🔄 Feedback → Iterar** → Ciclo continuo de mejora

### 🎯 Modelo de IA Recomendado por Tarea

| Tarea | Modelo Recomendado | Razón |
|-------|-------------------|-------|
| 📝 Documentación técnica | **Claude Sonnet 4.5** | Precisión en arquitectura |
| 🏗️ Diseño de arquitectura | **Claude Sonnet 4.5** | Análisis profundo |
| ⚡ Código rápido/prototipos | **Grok Code Fast 1** | Velocidad de generación |
| 🐛 Debugging complejo | **Claude Sonnet 4.5** | Razonamiento detallado |
| 🔧 Scripts de automatización | **Grok Code Fast 1** | Implementación directa |

---

## 🗓️ Roadmap Inicial

| Semana | 🎯 Tarea | 📌 Entregable |
|--------|----------|--------------|
| **1** | Crear 5 repositorios en GitHub | Repos vacíos con README inicial |
| **2** | Setup backend base (Node.js + Express + Prisma) | Endpoint `/health` funcionando |
| **3** | Implementar autenticación JWT en `reservas-admin` | Login/register + middleware auth |
| **4** | Replicar estructura en otros 4 proyectos | Mismo stack en todos |
| **5** | Dockerizar primer proyecto | `docker-compose up` funcional |
| **6** | Configurar CI/CD (GitHub Actions) | Tests automáticos en PRs |
| **7+** | Desarrollo de funcionalidades específicas | Features por proyecto |

---

## 🚀 Próximos Pasos Inmediatos

### ✅ Checklist de Setup

- [ ] **Crear repositorios en GitHub**
  ```bash
  gh repo create Aoneken/reservas-admin --public
  gh repo create Aoneken/reservas-jugadores --public
  gh repo create Aoneken/gestion-financiera --public
  gh repo create Aoneken/data-scraper --public
  gh repo create Aoneken/channel-manager --public
  ```

- [ ] **Clonar repositorios en Codespace**
  ```bash
  cd /workspaces
  gh repo clone Aoneken/reservas-admin
  gh repo clone Aoneken/reservas-jugadores
  # ... etc
  ```

- [ ] **Implementar backend base en `reservas-admin`**
  - Inicializar Node.js (`npm init -y`)
  - Instalar dependencias (`express`, `prisma`, `jsonwebtoken`, `bcrypt`)
  - Crear estructura de carpetas
  - Configurar Prisma con PostgreSQL
  - Implementar endpoint `/health`

- [ ] **Pedir siguiente instrucción a Grok** 🧠

---

## 📚 Recursos Adicionales

- 📄 [Manual de Inducción Completo](Manual_Inducción.md)
- 🖥️ [Informe del Codespace](Informe_Completo_Inicial_del_Codespace.md)
- 🔗 [Repositorio Principal](https://github.com/Aoneken/aok-apps)

---

## 👤 Maintainer

**Aoneken**  
📧 comercial@aoneken.com  
🔗 [GitHub](https://github.com/Aoneken)

---

## 📊 Estado del Proyecto

![Estado](https://img.shields.io/badge/Estado-En%20Desarrollo-yellow)
![Última actualización](https://img.shields.io/badge/Última%20actualización-Octubre%202025-blue)

**Versión:** 1.0.0  
**Última actualización:** 31 de octubre de 2025

---

<div align="center">
  
**🌟 Construido con GitHub Copilot & Grok IA 🌟**

</div>