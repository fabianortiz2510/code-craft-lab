# code-craft-lab

Laboratorio personal para aprender desarrollo frontend moderno con **React + TypeScript**, construyendo un proyecto real paso a paso (hito por hito) y aplicando arquitectura y Clean Code.

## Creación del Frontend

La estructura base de `frontend/`:

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

##  Cómo arrancar

```bash
cd frontend
npm install      # solo la primera vez
npm run dev      # servidor de desarrollo → http://localhost:5173
npm run build    # compila y verifica tipos (debe terminar sin errores)
```

---

