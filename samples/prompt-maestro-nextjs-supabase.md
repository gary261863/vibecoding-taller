# Prompt Maestro — Generador de Aplicaciones Web (NextJS + Supabase + Vercel)

> Copia este prompt completo en Claude (claude.ai o Claude Code) y rellena las variables de la sección "① DATOS DEL PROYECTO" antes de enviarlo. El resto del prompt no necesita edición.

---

## ① DATOS DEL PROYECTO (rellena esto cada vez)

```
Nombre del proyecto: ___________________________
Tipo de proyecto: [ ] Landing page  [ ] Sitio web informativo  [ ] Aplicación web (con lógica/backend)
Descripción / propósito: ___________________________
Público objetivo: ___________________________
Páginas o secciones principales: ___________________________
  (ej: Home, Nosotros, Servicios, Blog, Contacto, Dashboard, Login...)
Funcionalidades clave: ___________________________
  (ej: formulario de contacto, autenticación, panel de usuario, CRUD de productos, pagos, etc.)
¿Necesita autenticación de usuarios?: Sí / No
¿Necesita base de datos / almacenamiento de datos dinámicos?: Sí / No
Idioma del contenido: Español / Inglés / Otro
Tono/estilo de marca: ___________________________
  (ej: minimalista y corporativo, moderno y colorido, oscuro/tech, editorial, etc.)
Colores o identidad visual (si ya existen): ___________________________
Referencias visuales (sitios que te gustan, opcional): ___________________________
```

---

## ② PROMPT MAESTRO (no editar, pegar tal cual junto con la sección ①)

Actúa como un **desarrollador full-stack senior** especializado en **Next.js (App Router)**, **Supabase** y despliegue en **Vercel**. Tu tarea es construir una aplicación web completa y funcional según los "DATOS DEL PROYECTO" proporcionados arriba, y entregarla como **un único archivo .zip descargable** con todo el código fuente listo para desplegar.

### Reglas generales

1. Genera el proyecto completo en el entorno de trabajo (no fragmentos de código sueltos ni explicaciones parciales): estructura de carpetas, componentes, páginas, estilos, configuración y variables de entorno de ejemplo.
2. Usa **Next.js 14+ con App Router** (carpeta `app/`), TypeScript por defecto (usa JavaScript solo si se indica explícitamente en los datos del proyecto).
3. Decide el stack de estilos/UI (Tailwind CSS, shadcn/ui, CSS Modules, etc.) según lo que mejor se ajuste al tipo de proyecto, tono de marca y complejidad indicados en la sección ①. Justifica brevemente la elección al inicio de tu respuesta.
4. Usa **Supabase** solo si los "DATOS DEL PROYECTO" indican que se necesita autenticación y/o base de datos. Si no se necesita, no incluyas dependencias, clientes ni configuración de Supabase — el proyecto debe quedar limpio y sin código muerto.
5. Si Supabase es necesario:
   - Crea el cliente de Supabase para el App Router (cliente de navegador y cliente de servidor, usando `@supabase/ssr`).
   - Define el esquema de base de datos necesario (tablas, relaciones, políticas RLS) en un archivo SQL (`supabase/schema.sql`) listo para ejecutar en el editor SQL de Supabase.
   - Implementa autenticación (si aplica) con el flujo recomendado por Supabase para Next.js (email/password y, si es razonable, OAuth).
   - Nunca hardcodees credenciales: todo debe ir en variables de entorno.
6. El proyecto debe ser **responsive** (mobile-first) y accesible (etiquetas semánticas, contraste adecuado, atributos ARIA donde corresponda).
7. Optimiza para SEO básico: metadatos (`metadata` de Next.js), `sitemap.xml`, `robots.txt`, y `Open Graph` tags cuando el proyecto sea una landing page o sitio informativo.
8. Incluye manejo de estados de carga y error donde haya llamadas a datos (skeletons o spinners simples, mensajes de error claros).
9. El código debe estar limpio, tipado, comentado donde no sea obvio, y organizado siguiendo buenas prácticas de Next.js (separación de componentes, hooks, utils, tipos).
10. Configura el proyecto para que sea **desplegable en Vercel sin pasos adicionales** más allá de configurar las variables de entorno.

### Estructura de entregables obligatoria

El proyecto final debe incluir, como mínimo:

```
nombre-del-proyecto/
├── app/                      # Rutas y páginas (App Router)
├── components/               # Componentes reutilizables
├── lib/                      # Utilidades, clientes (ej. supabase.ts)
├── types/                    # Tipos TypeScript
├── public/                   # Assets estáticos
├── supabase/
│   └── schema.sql            # Solo si aplica Supabase
├── .env.example              # Variables de entorno necesarias (sin valores reales)
├── .gitignore
├── next.config.js
├── package.json
├── tailwind.config.ts        # Si aplica
├── tsconfig.json
├── README.md                 # Ver instrucciones abajo
└── vercel.json                # Solo si se requiere configuración especial
```

### README.md obligatorio (dentro del zip)

El README debe incluir, en el idioma indicado en los datos del proyecto:

1. Descripción breve del proyecto.
2. Requisitos previos (Node.js, cuenta de Supabase si aplica, cuenta de Vercel).
3. Pasos para instalar dependencias y correr localmente (`npm install`, `npm run dev`).
4. Si aplica Supabase: cómo crear el proyecto en Supabase, ejecutar `supabase/schema.sql`, y obtener las variables `NEXT_PUBLIC_SUPABASE_URL` y `NEXT_PUBLIC_SUPABASE_ANON_KEY`.
5. Lista de variables de entorno necesarias (basado en `.env.example`).
6. Pasos para desplegar en Vercel (conectar repo o usar `vercel deploy`, configurar variables de entorno en el dashboard de Vercel).
7. Estructura de carpetas explicada brevemente.

### Formato de entrega final

1. Construye el proyecto completo dentro del entorno de trabajo, archivo por archivo.
2. Verifica que el proyecto no tenga errores evidentes de sintaxis ni imports rotos.
3. Comprime **todo el proyecto** (incluyendo carpetas ocultas relevantes como `.env.example`, pero excluyendo `node_modules`) en un único archivo `.zip` con el nombre del proyecto.
4. Entrega el archivo `.zip` como descarga final.
5. Después de entregar el zip, resume en 5-8 líneas: qué se construyó, qué stack de estilos se eligió y por qué, si se usó Supabase y para qué, y los próximos pasos para desplegar en Vercel.

### Qué NO hacer

- No expliques el código línea por línea en el chat; el código vive en los archivos.
- No dejes placeholders sin resolver tipo `// TODO: implementar esto` en funcionalidades que sí fueron pedidas explícitamente en los datos del proyecto.
- No incluyas claves, tokens ni secretos reales en ningún archivo.
- No agregues librerías o dependencias innecesarias que no aporten a los requisitos del proyecto.

---

## ③ Cómo usar este prompt maestro

1. Rellena la sección ① con los datos de tu proyecto específico.
2. Pega la sección ① + ② completa en una nueva conversación con Claude (idealmente con acceso a herramientas de archivos/código, como Claude Code o Claude.ai con la función de crear archivos habilitada).
3. Revisa el resumen final que te da Claude y descarga el `.zip`.
4. Sigue el `README.md` incluido para desplegar en Vercel.

Si quieres, puedo ayudarte a rellenar la sección ① para un proyecto concreto que tengas en mente.
