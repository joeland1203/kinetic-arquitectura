# KINETIC ARQUITECTURA — ESTADO Y CONTEXTO DEL PROYECTO

> Documento de persistencia de sesión generado para retomar el desarrollo sin pérdida de contexto.

---

## 1. URLs y Despliegues Activos

- **Dominio Principal en Producción**: [https://kinetic.codigobinario.com.mx](https://kinetic.codigobinario.com.mx)
- **Vercel Direct URL**: [https://kinetic-arquitectura.vercel.app](https://kinetic-arquitectura.vercel.app)
- **Repositorio GitHub**: [https://github.com/joeland1203/kinetic-arquitectura](https://github.com/joeland1203/kinetic-arquitectura)
- **Servidor de Desarrollo Local**: `http://localhost:4321` (gestionado en segundo plano con `astro dev --background`)

---

## 2. Pila Tecnológica

- **Framework**: [Astro v7+](https://astro.build) (SSR / Static mode con `@tailwindcss/vite` v4).
- **3D Engine**: [Three.js](https://threejs.org/) con `OrbitControls` y `GLTFLoader`.
- **Compresión 3D**: `meshoptimizer` (`MeshoptDecoder`) para decodificar mallas `EXT_meshopt_compression` de `gltfpack`.
- **Estilos & Tipografía**: Tailwind CSS v4, fuentes editoriales sans y monoespaciadas, paleta Anti-Slop (bloques oscuros `#080808`, `#111111`, acentos en platino `#a1a1aa` y oro arquitectónico `#d4af37`).

---

## 3. Arquitectura de Componentes y Orden de Secciones

En `src/pages/index.astro`, el flujo de la landing page sigue una narrativa editorial asimétrica:

1. **Header de Navegación Fijo con Glassmorphism**:
   - Logo *Kinetic Arquitectura* con indicador pulsante.
   - Enlaces ancla con scroll suave (`#desarrollo`, `#ingenieria`, `#sustentabilidad`, `#contacto`).
   - Contador dinámico de fotogramas (`FRAME 001/175`) y menú móvil interactivo.

2. **Hero Scrollytelling (`#scrollyContainer`, `min-h-[450vh]`)**:
   - Canvas 2D interactivo a pantalla completa (`#kineticCanvas`, 175 fotogramas WebP en `public/frames/frame-001.webp` a `175.webp`).
   - Algoritmo de interpolación continua **LERP** (`lerpFactor = 0.08`) a 60 FPS con soporte para pantallas Retina.
   - **Micro-Crossfade de Canvas**:
     - *Corte 1 (Exterior a Lobby)*: Frames 35 al 39 (Scroll ~17% a 26%). Base en frame 35, overlay en frame 39 con interpolación `ctx.globalAlpha`.
     - *Corte 2 (Lobby a Recepción)*: Frames 131 al 137 (Scroll ~70% a 81%). Base en frame 131, overlay en frame 137 con interpolación `ctx.globalAlpha`.
   - **Máscaras Editoriales Flotantes Centradas** (`#heroTransitionContainer`):
     - Contenedor dedicado `absolute inset-0 flex items-center justify-center` con fondo translúcido (`bg-[#080808]/30 backdrop-blur-md border-y border-white/15 shadow-[0_8px_40px_rgba(0,0,0,0.4)]`).
     - *Panel 1*: `01.5 / SECUENCIA DE ACCESO` // `UMBRAL Y TRANSICIÓN TÉRMICA`.
     - *Panel 2*: `02.5 / MATERIALIDAD` // `INMERSIÓN MONOLÍTICA`.
   - **Bloques Editoriales Laterales** (`#heroTextContainer`):
     - *Bloque 1* (0% a 18%): `01 / DESARROLLO VERTICAL`
     - *Bloque 2* (26% a 70%): `02 / ENVOLVENTES BIOCLIMÁTICAS`
     - *Bloque 3* (81% a 96%): `03 / RIGOR TECTÓNICO` (con CTAs hacia Desarrollo y Kinetic Lab 3D)

3. **Sección 01: Desarrollo Patrimonial (`src/components/DesarrolloSection.astro`)**:
   - Anchor: `#desarrollo`.
   - Layout editorial tipo revista arquitectónica asimétrica.
   - Proyectos insignia: *Torre Kinetic Sky*, *Cantilever Zero*, *The Kinetic Helix* con especificaciones técnicas tabulares.

4. **Sección 3D Interactiva: Kinetic Lab (`src/components/ModelViewer3D.astro`)**:
   - Anchor: `#modelo-3d`.
   - Carga y renderiza `public/models/casa_flotante.glb` con decodificación `MeshoptDecoder`.
   - Iluminación de estudio arquitectónico (luz ambiental difusa, directional light cálida a 45°, fill light fría).
   - Centrado automático por BoundingBox y BoundingSphere con escala ampliada (2x).
   - Controles `OrbitControls` con damping suave, auto-rotación automática y modal interactivo para inspección técnica.

5. **Sección 02: Rigor Técnico & Ingeniería (`src/components/IngenieriaSection.astro`)**:
   - Anchor: `#ingenieria`.
   - Fichas técnicas numeradas (02.1 a 02.4): Disipadores sísmicos viscoelásticos, exoesqueleto diagrid, cálculo por elementos finitos (FEA).
   - Modal de análisis estructural interactivo.

6. **Sección 03: Arquitectura Bioclimática & Sustentabilidad (`src/components/SustentabilidadSection.astro`)**:
   - Anchor: `#sustentabilidad`.
   - Filosofía termodinámica, ciclo de vida ACV, métricas EUI, certificación LEED Platinum BD+C.

7. **Sección 04: Contacto Privado & Colofón (`src/components/ContactoSection.astro`)**:
   - Anchor: `#contacto`.
   - Formulario editorial de consulta privada para inversionistas patrimoniales.
   - Ateliers físicos en Ciudad de México (Paseo de la Reforma) y Zúrich (Bahnhofstrasse).

---

## 4. Infraestructura & DevOps

- **Cloudflare**:
  - Zona: `codigobinario.com.mx` (Zone ID `53ee2609d127258bc86e231395682c41`).
  - Registro: CNAME `kinetic` → `cname.vercel-dns.com` (DNS Only / SSL Full).
- **Vercel**:
  - Proyecto: `kinetic-arquitectura` (ID `prj_YWZQUXKrZsqCEaByJtrRwglVaIK1`).
  - Team: `team_wZDtNNe1DbOgu6uwl7sLwI6I` (`joeland1203`).
  - Dominios asignados: `kinetic.codigobinario.com.mx`, `kinetic-arquitectura.vercel.app`.
- **Git**:
  - Rama: `main`.
  - Remote: `origin` apuntando a `https://github.com/joeland1203/kinetic-arquitectura.git`.

---

## 5. Comandos de Trabajo Habituales

```bash
# Iniciar servidor dev en segundo plano (regla del workspace)
astro dev --background

# Consultar estado y logs del dev server
astro dev status
astro dev logs

# Compilar proyecto para producción
npm run build
```
