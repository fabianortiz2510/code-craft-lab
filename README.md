# code-craft-lab

Laboratorio personal para aprender desarrollo frontend moderno con **React + TypeScript**, construyendo un proyecto real paso a paso (hito por hito) y aplicando arquitectura y Clean Code.

## Cómo se creó el frontend

La estructura base de `frontend/` se generó desde la raíz del repo con:

```bash
npm create vite@latest frontend -- --template react-ts
```

| Parte del comando | Qué hace |
|---|---|
| `npm create vite@latest` | Ejecuta el asistente oficial de Vite (`create-vite`) en su versión más reciente |
| `frontend` | Nombre de la carpeta que se crea (usa `.` para crearlo en la carpeta actual) |
| `--` | Separa los argumentos de `npm` de los que recibe Vite |
| `--template react-ts` | Plantilla de React + TypeScript (`react` sería solo JavaScript) |

Durante el asistente se eligió **ESLint** como linter y se aceptó instalar dependencias y arrancar el servidor.

**Limpieza posterior de la plantilla:**
- `App.tsx` reducido a un componente mínimo (`return <div></div>`)
- `App.css` e `index.css` vaciados (eran estilos de la demo)
- `src/assets/` eliminable (logos de la demo)
- `"strict": true` añadido en `tsconfig.app.json`

## 🚀 Cómo arrancar

```bash
cd frontend
npm install      # solo la primera vez
npm run dev      # servidor de desarrollo → http://localhost:5173
npm run build    # compila y verifica tipos (debe terminar sin errores)
```

---

# 📚 Notas de aprendizaje

## 1. Estructura de un proyecto frontend

Hay que distinguir dos cosas: **lo que genera la herramienta** y **lo que decides tú**.

### 1.1 Lo que genera la herramienta (Vite + React + TS)

Todo proyecto creado con Vite parte de esta base:

```
frontend/
├── public/              ← archivos que se sirven tal cual (favicon, iconos)
├── src/                 ← TU código (aquí trabajas el 95% del tiempo)
│   ├── main.tsx         ← punto de entrada: arranca React
│   ├── App.tsx          ← componente raíz
│   └── index.css        ← estilos globales
├── index.html           ← la única página HTML; tiene el <div id="root">
├── package.json         ← dependencias y scripts (npm run dev, build…)
├── package-lock.json    ← versiones exactas instaladas (no se edita a mano)
├── vite.config.ts       ← configuración de Vite
├── tsconfig*.json       ← configuración de TypeScript
└── eslint.config.js     ← reglas del linter
```

> Otras herramientas usan otra base. Ejemplo: **Next.js** usa una carpeta `app/` donde las carpetas se convierten en rutas (`app/login/page.tsx` → `/login`).

### 1.2 Cómo arranca la aplicación

```
index.html  →  main.tsx  →  App.tsx  →  (tus componentes)
(div#root)    (arranca React)  (componente raíz)
```

- `main.tsx` **importa** `App` y lo dibuja dentro de `<div id="root">`.
- Por eso `App.tsx` **nunca puede quedar vacío**: debe exportar un componente.

### 1.3 Lo que decides tú: la estructura de `src/`

React **no impone** ninguna estructura. Existen dos enfoques principales:

**A) Por tipo técnico** — común en tutoriales y proyectos pequeños

```
src/
├── components/   ← TODOS los componentes
├── hooks/        ← TODOS los hooks
├── services/     ← TODAS las llamadas a APIs
└── types/        ← TODOS los tipos
```

- ✅ Fácil de entender al inicio.
- ❌ No escala: con muchos archivos se vuelve un cajón desordenado y una misma funcionalidad queda repartida en varias carpetas.

**B) Por feature (dominio)** — el enfoque que usamos en este proyecto

```
src/
├── app/              ← lo global (App, rutas, providers)
├── features/
│   ├── tasks/        ← TODO lo de tareas junto
│   │   ├── components/
│   │   ├── hooks/
│   │   └── types/
│   └── auth/         ← TODO lo de login junto
└── shared/           ← lo reutilizable por varias features (Botón, Modal…)
```

- ✅ Escala bien: cada funcionalidad vive en un solo lugar.
- ✅ Si borras `features/auth/`, eliminas el login completo sin tocar nada más.

> 🧠 **Idea clave:** la *base* la pone la herramienta; la *estructura de `src/`* la diseñas tú según el tamaño y las necesidades del proyecto.

---

## 2. Anatomía de un componente React

```tsx
// ① IMPORTS: lo que este archivo necesita de otros

// ② TIPOS: qué datos recibe el componente
interface ClimaProps {
  ciudad: string;
  grados: number;
}

// ③ COMPONENTE: función en PascalCase que recibe props y DEVUELVE JSX
function Clima({ ciudad, grados }: ClimaProps) {
  return (
    <div className="clima">     {/* ④ un solo elemento padre */}
      <h2>{ciudad}</h2>         {/* ⑤ {} inserta JavaScript */}
      <p>{grados} °C</p>
    </div>
  );
}

// ⑥ EXPORT: para que otros archivos puedan usarlo
export default Clima;
```

Uso: `<Clima ciudad="Bogotá" grados={14} />`

---

## 3. Buenas prácticas aprendidas

- **Código muerto se borra.** Si una clase CSS, archivo o import no lo usa nadie, se elimina: confunde a quien lea el código después.
- **`"strict": true` siempre** en `tsconfig.app.json`. Sin él, TypeScript deja pasar errores con `null`/`undefined` y tipos `any` implícitos.
- **Evitar el operador `!`** (non-null assertion). Silencia al compilador; solo es aceptable cuando la existencia está garantizada (ej. `#root` en `main.tsx`).
- **No ejecutar `npm audit fix --force`** sin entender qué hace: puede actualizar paquetes a versiones incompatibles y romper el proyecto.
- **Los comandos `npm` se ejecutan dentro de `frontend/`.**

---

## 🗺️ Progreso

| Hito | Tema | Estado |
|---|---|---|
| 0 | Anatomía de componentes (`src/playground/`) | 🔄 En curso |
| 1 | Base y componentes de presentación — app de tareas | ⏳ Pendiente |
