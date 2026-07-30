# Traspaso Ya — Guía de despliegue paso a paso

Esta carpeta ya está lista para subir a **Vercel** (gratis para este uso).
Contiene:
- `index.html` → tu app (ya ajustada para usar el proxy en vez de llamar directo a Anthropic)
- `api/extract.js` → el "puente" que guarda tu llave de Anthropic de forma segura y habla con la IA por ti

## Paso 1 — Consigue tu API key de Anthropic

1. Entra a https://console.anthropic.com
2. Crea una cuenta (si no tienes) y agrega una forma de pago — el uso de "Extraer datos" consume créditos según lo que uses, es pago por uso.
3. Ve a **API Keys** → **Create Key** → cópiala. Se ve como `sk-ant-...`. Guárdala, no la vuelvas a ver completa después.

## Paso 2 — Crea tu cuenta en Vercel

1. Entra a https://vercel.com y crea una cuenta (puedes usar tu correo o GitHub).

## Paso 3 — Sube el proyecto

**Opción fácil (arrastrar y soltar, sin usar terminal):**
1. En Vercel, click **Add New → Project**.
2. Elige **"Deploy without Git" / "Upload"** (o crea un repo en GitHub y sube esta carpeta ahí, y luego conéctalo — cualquiera de las dos funciona).
3. Arrastra esta carpeta completa (`index.html` + la carpeta `api`).

**Opción con terminal (si tienes Node instalado en tu computador):**
```
npm install -g vercel
cd carpeta-donde-descomprimiste-esto
vercel
```
Sigue las preguntas en pantalla (acepta las opciones por defecto).

## Paso 4 — Configura tu API key en Vercel

1. En el proyecto dentro de Vercel, ve a **Settings → Environment Variables**.
2. Agrega una variable:
   - **Name:** `ANTHROPIC_API_KEY`
   - **Value:** la llave que copiaste en el Paso 1
3. Guarda.
4. Ve a la pestaña **Deployments** y dale **Redeploy** (para que tome la nueva variable).

## Paso 5 — Pruébala

1. Vercel te da una URL como `https://traspaso-ya-tuusuario.vercel.app`.
2. Ábrela, sube una foto de una tarjeta de propiedad, toca "Extraer datos".
3. Si todo quedó bien configurado, debería leer los datos igual que aquí en el chat.

## Si algo falla

- **"Extraer datos" da error:** revisa en Vercel → tu proyecto → **Deployments** → click el deployment → **Functions** → busca `extract` y mira el error ahí. Casi siempre es que la variable `ANTHROPIC_API_KEY` no quedó bien guardada o falta redeploy.
- **Quieres cambiar algo del diseño o los formularios:** edita `index.html` directamente y vuelve a subir (o si usaste Git, solo haz push y Vercel actualiza solo).

## Sobre el costo

- Vercel: gratis en este nivel de uso.
- Anthropic: pagas solo por lo que uses. Cada "Extraer datos" es una llamada; el costo es bajo (fracciones de centavo a pocos centavos por imagen), pero revisa los precios actuales en https://www.anthropic.com/pricing antes de lanzarlo al público, sobre todo si esperas muchos usuarios.

## Siguiente paso (pasarela de pagos)

Cuando quieras cobrar por usar la app, dime y seguimos desde aquí — se agrega en el mismo backend (`api/`), con Wompi o ePayco si es para Colombia.
