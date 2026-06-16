# Plan de Pruebas - DungeonAssistant

**ID del Plan:** TP-DA-2026-001  
**Título:** Plan de Pruebas Integral - DungeonAssistant v1.0  
**Preparado por:** [Tu Nombre]  
**Fecha:** 14 de junio de 2026  
**Versión:** 1.0

---

## 1. Introducción

### 1.1 Propósito
Validar la funcionalidad, rendimiento, seguridad y usabilidad de DungeonAssistant, una PWA mobile-first para gestión de campañas D&D 5e con integración de IA, antes de su lanzamiento oficial.

### 1.2 Objetivos Generales
- Validar que todas las funcionalidades críticas operen correctamente
- Asegurar la integración entre frontend (React/Vite) y backend (FastAPI)
- Verificar la conectividad con servicios externos (Supabase, Gemini API, dnd5eapi.co)
- Confirmar la sincronización en tiempo real vía Socket.io
- Validar la experiencia de usuario en dispositivos móviles y desktop

---

## 2. Alcance de Pruebas

### 2.1 En Alcance

#### Backend (FastAPI)
| Módulo | Descripción |
|--------|-------------|
| Autenticación | Login, registro, validación de tokens JWT |
| Campañas | CRUD de campañas, gestión de roles (GM/Player) |
| Personajes | Hoja de personaje D&D 5e, validación de reglas |
| Sesiones | Creación, inicio, cierre de sesiones |
| NPCs | Generación con IA, edición, inventario |
| OCR | Procesamiento de hojas físicas con Gemini Vision |
| Asistente IA | Chat conversacional con contexto de campaña |
| Búsqueda D&D 5e | Integración con dnd5eapi.co |
| WebSockets | Sincronización en tiempo real |

#### Frontend (React + Vite)
| Módulo | Descripción |
|--------|-------------|
| Welcome Page | Login/Registro interactivo |
| Dashboard | Listado de campañas del usuario |
| Detalle Campaña | Vista GM con gestión de jugadores |
| Hoja Personaje | Formulario con validación D&D 5e |
| Visor 3D | Visualización de dados con ammo.wasm |
| Temas visuales | Sistema de temas (claro/oscuro) |
| Crónicas | Registro de notas por sesión |
| OCR Tab | Interfaz para escaneo de hojas |
| PWA | Funcionalidad offline, instalación |

#### Integraciones
- Supabase (PostgreSQL)
- Google Gemini API (IA y OCR)
- dnd5eapi.co (datos D&D 5e)
- Socket.io (tiempo real)

### 2.2 Fuera de Alcance
- Pruebas de carga masiva (más de 100 usuarios concurrentes)
- Pruebas de penetración avanzadas
- Compatibilidad con navegadores antiguos (IE11)
- Dispositivos con versiones de OS anteriores a 2 años

---

## 3. Estrategia de Pruebas

### 3.1 Tipos de Pruebas

| Tipo | Descripción | Herramienta |
|------|-------------|-------------|
| **Pruebas Unitarias** | Validar funciones individuales | pytest, Jest |
| **Pruebas de Integración** | Verificar comunicación entre módulos | pytest + httpx |
| **Pruebas E2E** | Flujos completos de usuario | Playwright/Cypress |
| **Pruebas de API** | Validar endpoints REST | Postman/pytest |
| **Pruebas de WebSocket** | Sincronización en tiempo real | socket.io-client |
| **Pruebas de UI/UX** | Usabilidad y diseño responsive | Manual |
| **Pruebas de Seguridad** | Autenticación, autorización, inyección | Manual + herramientas |
| **Pruebas de Rendimiento** | Tiempos de respuesta | k6/JMeter |
| **Pruebas PWA** | Offline, instalación, service worker | Lighthouse |

### 3.2 Priorización de Pruebas

**Prioridad 1 - Críticas (Smoke Tests)**
- Login/Registro exitoso
- Creación de campaña
- Conexión WebSocket
- Carga de hoja de personaje
- Endpoint /health

**Prioridad 2 - Alta**
- Gestión de roles (GM/Player)
- Edición de personaje con validación D&D 5e
- Generación de NPCs con IA
- OCR de hojas físicas
- Sincronización en tiempo real

**Prioridad 3 - Media**
- Temas visuales (claro/oscuro)
- Visor 3D de dados
- Crónicas y notas
- Búsqueda en dnd5eapi.co
- Funcionalidad offline PWA

**Prioridad 4 - Baja**
- Animaciones y transiciones
- Mensajes de error específicos
- Casos edge en validaciones

---

## 4. Cronograma de Pruebas

| Fase | Fecha Inicio | Fecha Fin | Duración | Responsable |
|------|--------------|-----------|----------|-------------|
| Planificación | 15/06/2026 | 16/06/2026 | 2 días | QA Lead |
| Diseño de casos | 17/06/2026 | 23/06/2026 | 5 días | QA Team |
| Configuración entorno | 24/06/2026 | 25/06/2026 | 2 días | DevOps/QA |
| Ejecución - Smoke | 26/06/2026 | 26/06/2026 | 1 día | QA Team |
| Ejecución - Funcional | 27/06/2026 | 07/07/2026 | 7 días | QA Team |
| Ejecución - Integración | 08/07/2026 | 12/07/2026 | 5 días | QA Team |
| Ejecución - E2E | 13/07/2026 | 17/07/2026 | 5 días | QA Team |
| Verificación de bugs | 18/07/2026 | 22/07/2026 | 5 días | QA + Dev |
| Pruebas de rendimiento | 23/07/2026 | 24/07/2026 | 2 días | QA Team |
| Pruebas de seguridad | 25/07/2026 | 28/07/2026 | 2 días | QA Team |
| Cierre y reporte | 29/07/2026 | 30/07/2026 | 2 días | QA Lead |

**Buffer adicional:** 3 días para imprevistos

---

## 5. Entorno de Pruebas

### 5.1 Hardware y Software

| Componente | Especificación |
|------------|----------------|
| **Backend** | Python 3.11+, FastAPI, uvicorn |
| **Frontend** | Node.js 18+, React 18, Vite, pnpm |
| **Base de datos** | PostgreSQL (Supabase) |
| **Navegadores** | Chrome 120+, Firefox 115+, Safari 17+, Edge 120+ |
| **Móviles** | iOS 16+, Android 12+ |
| **OS Testing** | Windows 11, macOS 14, Ubuntu 22.04 |

### 5.2 URLs de Entornos

| Entorno | URL | Propósito |
|---------|-----|-----------|
| Desarrollo Local | http://localhost:5173 (frontend), http://localhost:8000 (backend) | Desarrollo |
| Staging | [URL de staging] | Pruebas pre-producción |
| Producción | https://dungeon-assistant-test.vercel.app | Validación final |

### 5.3 Datos de Prueba

- **Usuarios de prueba:** 5 cuentas (1 GM, 4 Players)
- **Campañas de prueba:** 3 campañas con diferentes estados
- **Personajes de prueba:** 10 personajes con diferentes clases/niveles
- **Datos mock:** Hojas de personaje en PDF para OCR
- **Datos de producción:** Anonimizados para pruebas de rendimiento

### 5.4 Configuración de Variables de Entorno

```env
# Backend
DATABASE_URL=postgresql://...
SUPABASE_URL=...
SUPABASE_KEY=...
GOOGLE_GEMINI_API_KEY=...
SECRET_KEY=...

# Frontend
VITE_API_URL=...
VITE_SOCKET_URL=...
```

---

## 6. Recursos y Responsabilidades

| Rol | Nombre | Responsabilidades |
|-----|--------|-------------------|
| QA Lead | [Nombre] | Plan de pruebas, coordinación, reportes |
| QA Engineer 1 | [Nombre] | Pruebas de API, integración, automatización |
| QA Engineer 2 | [Nombre] | Pruebas E2E, UI/UX, PWA |
| QA Engineer 3 | [Nombre] | Pruebas de seguridad, rendimiento |
| Dev Support | [Nombre] | Soporte técnico, triage de bugs, entorno |
| Product Owner | [Nombre] | Validación de requisitos, UAT |

---

## 7. Entregables de Pruebas

### 7.1 Antes de Pruebas
- [x] Plan de pruebas (este documento)
- [ ] Casos de prueba documentados
- [ ] Datos de prueba preparados
- [ ] Entorno de pruebas configurado

### 7.2 Durante Pruebas
- [ ] Log de ejecución de pruebas
- [ ] Reporte de defectos (bugs)
- [ ] Reporte de progreso diario
- [ ] Métricas de cobertura

### 7.3 Después de Pruebas
- [ ] Reporte final de pruebas
- [ ] Reporte de UAT
- [ ] Lecciones aprendidas
- [ ] Notas de lanzamiento

---

## 8. Criterios de Entrada y Salida

### 8.1 Criterios de Entrada
- [ ] Código desplegado en entorno de staging
- [ ] Base de datos configurada con datos de prueba
- [ ] Variables de entorno configuradas
- [ ] Acceso a servicios externos verificado (Gemini, Supabase)
- [ ] Casos de prueba revisados y aprobados
- [ ] Entorno de pruebas estable

### 8.2 Criterios de Salida
- [ ] 95% de casos de prueba críticos ejecutados
- [ ] 100% de casos de prueba críticos aprobados
- [ ] No hay bugs críticos o severos abiertos
- [ ] Pruebas de regresión completadas
- [ ] Reporte final de pruebas aprobado
- [ ] UAT completado y firmado

### 8.3 Criterios de Suspensión
- [ ] Entorno de pruebas inestable
- [ ] Bug bloqueante que impide continuar
- [ ] Servicios externos no disponibles
- [ ] Cambio significativo en requisitos

---

## 9. Riesgos y Mitigaciones

| Riesgo | Probabilidad | Impacto | Mitigación |
|--------|--------------|---------|------------|
| Plazos ajustados | Alta | Alto | Priorizar pruebas críticas, automatizar donde sea posible |
| Inestabilidad del entorno | Media | Alto | Tener entorno local como backup, monitoreo constante |
| Dependencia de servicios externos | Media | Alto | Mocks para Gemini y dnd5eapi, pruebas sin conexión |
| Bugs críticos tardíos | Media | Alto | Pruebas tempranas, integración continua |
| Cambios de último minuto | Alta | Medio | Buffer de tiempo, comunicación constante con dev |
| Limitación de dispositivos | Baja | Medio | Usar BrowserStack o similar para cobertura |

---

## 10. Casos de Prueba Principales

### 10.1 Autenticación

| ID | Caso de Prueba | Prioridad | Tipo |
|----|----------------|-----------|------|
| AUTH-001 | Registro exitoso con email válido | Crítica | Funcional |
| AUTH-002 | Login exitoso con credenciales válidas | Crítica | Funcional |
| AUTH-003 | Login fallido con credenciales inválidas | Alta | Funcional |
| AUTH-004 | Recuperación de contraseña | Alta | Funcional |
| AUTH-005 | Sesión expira después de timeout | Media | Funcional |
| AUTH-006 | Token JWT válido en todas las peticiones | Crítica | Seguridad |

### 10.2 Gestión de Campañas

| ID | Caso de Prueba | Prioridad | Tipo |
|----|----------------|-----------|------|
| CAMP-001 | Crear campaña con nombre y lore | Crítica | Funcional |
| CAMP-002 | Listar campañas del usuario | Crítica | Funcional |
| CAMP-003 | Editar campaña (solo GM) | Alta | Funcional |
| CAMP-004 | Eliminar campaña (solo GM) | Alta | Funcional |
| CAMP-005 | Invitar jugador a campaña | Alta | Funcional |
| CAMP-006 | Cambiar rol GM <-> Player | Alta | Funcional |
| CAMP-007 | Transferir rol de GM | Media | Funcional |

### 10.3 Hoja de Personaje

| ID | Caso de Prueba | Prioridad | Tipo |
|----|----------------|-----------|------|
| CHAR-001 | Crear personaje con datos básicos | Crítica | Funcional |
| CHAR-002 | Validación de atributos D&D 5e | Crítica | Funcional |
| CHAR-003 | Cálculo automático de modificadores | Alta | Funcional |
| CHAR-004 | Inventario dinámico | Alta | Funcional |
| CHAR-005 | Validación contra dnd5eapi.co | Alta | Integración |
| CHAR-006 | OCR de hoja física | Alta | Funcional |
| CHAR-007 | Visor 3D de dados | Media | Funcional |

### 10.4 Tiempo Real (Socket.io)

| ID | Caso de Prueba | Prioridad | Tipo |
|----|----------------|-----------|------|
| WS-001 | Conexión WebSocket exitosa | Crítica | Integración |
| WS-002 | Notificación de inicio de sesión | Alta | Funcional |
| WS-003 | Sincronización de notas compartidas | Alta | Funcional |
| WS-004 | Reconexión automática tras desconexión | Alta | Funcional |
| WS-005 | Manejo de múltiples usuarios en campaña | Media | Rendimiento |

### 10.5 Integración con IA

| ID | Caso de Prueba | Prioridad | Tipo |
|----|----------------|-----------|------|
| AI-001 | Generación de NPC con rasgos aleatorios | Alta | Funcional |
| AI-002 | Asistente conversacional con contexto | Alta | Funcional |
| AI-003 | OCR con Gemini Vision | Alta | Funcional |
| AI-004 | Resumen automático de sesión | Media | Funcional |
| AI-005 | Análisis de notas (detección NPCs/ítems) | Media | Funcional |

### 10.6 PWA

| ID | Caso de Prueba | Prioridad | Tipo |
|----|----------------|-----------|------|
| PWA-001 | Instalación en móvil | Alta | Funcional |
| PWA-002 | Funcionalidad offline básica | Alta | Funcional |
| PWA-003 | Service worker registrado | Media | Funcional |
| PWA-004 | Icono y splash screen | Baja | UI/UX |

---

## 11. Métricas de Pruebas

| Métrica | Objetivo | Fórmula |
|---------|----------|---------|
| Cobertura de requisitos | 100% | (Requisitos con tests / Total requisitos) × 100 |
| Tasa de aprobación | ≥95% | (Tests aprobados / Tests ejecutados) × 100 |
| Densidad de defectos | <0.1 | Defectos / KLOC |
| Eficiencia de detección | >90% | Defectos encontrados en fase / Total defectos fase |
| Tests automatizados | >60% | Tests automáticos / Total tests |

---

## 12. Herramientas de Pruebas

| Categoría | Herramienta | Propósito |
|-----------|-------------|-----------|
| Gestión de pruebas | TestRail / Notion | Casos de prueba, ejecución |
| Automatización API | pytest + httpx | Pruebas de backend |
| Automatización E2E | Playwright | Flujos completos |
| Pruebas de carga | k6 | Rendimiento |
| Monitoreo | Sentry | Errores en producción |
| CI/CD | GitHub Actions | Ejecución automática |
| Reporte de bugs | GitHub Issues | Tracking de defectos |

---

## 13. Aprobación del Plan

| Rol | Nombre | Firma | Fecha |
|-----|--------|-------|-------|
| QA Lead | | | |
| Product Owner | | | |
| Tech Lead | | | |
| Project Manager | | | |

---

## Apéndice A: Glosario

- **GM:** Game Master (Maestro de Juego)
- **PWA:** Progressive Web App
- **OCR:** Optical Character Recognition
- **RAG:** Retrieval-Augmented Generation
- **E2E:** End-to-End

## Apéndice B: Referencias

- [TestRail - How To Create A Test Plan](https://www.testrail.com/blog/create-a-test-plan/)
- [ISTQB Test Plan Template](https://www.istqb.org/)
- [DungeonAssistant - LEEME.md](./LEEME.md)
- [DungeonAssistant - SETUP.md](./SETUP.md)

---

**Historial de Cambios**

| Versión | Fecha | Autor | Descripción |
|---------|-------|-------|-------------|
| 1.0 | 14/06/2026 | [Tu Nombre] | Versión inicial |
