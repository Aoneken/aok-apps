# Instrucciones para GitHub Copilot

## Reglas Generales
- Usa **Node.js 22 + Express + Prisma + PostgreSQL**.
- Estructura modular: `src/routes`, `src/controllers`, `src/middleware`.
- Usa **ESM** (`import`/`export`).
- JWT para autenticación.
- `.env` para configuración.
- Docker-ready.

## Convenciones
- Nombres de archivos: `kebab-case.js`
- Commits: Conventional Commits (`feat:`, `fix:`, `refactor:`)
- Código: Prettier + ESLint (configurados en `.vscode`)

## Flujo
1. Recibe instrucción de Grok.
2. Genera código.
3. Ejecuta `npm run dev` localmente.
4. Commit y push.
