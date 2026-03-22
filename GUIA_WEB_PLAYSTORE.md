# 🌐 ZPolar Chess — Guía de publicación Web + Play Store

## Estructura de archivos

```
zpolar_web/
├── index.html      ← Juego completo (todo en uno)
├── manifest.json   ← Config PWA (para instalar como app)
├── sw.js           ← Service Worker (jugar sin internet)
├── icons/          ← Crear estos iconos
│   ├── icon-192.png
│   └── icon-512.png
└── screenshots/    ← Para Play Store
    └── screen1.png
```

---

## PASO 1 — Probar localmente

Abre `index.html` directamente en Chrome/Firefox.
¡No necesitas servidor para probarlo!

---

## PASO 2 — Subir a GitHub Pages (GRATIS)

### 2.1 Crear repositorio
1. Ve a **https://github.com** → "New repository"
2. Nombre: `zpolar-chess`
3. Visibilidad: **Public**
4. Clic en "Create repository"

### 2.2 Subir archivos
```bash
# Opción A: usando Git
git init
git add .
git commit -m "ZPolar Chess v1.0"
git remote add origin https://github.com/TU_USUARIO/zpolar-chess.git
git push -u origin main
```

O arrastra los archivos directamente en GitHub.com

### 2.3 Activar GitHub Pages
1. Tu repositorio → **Settings** → **Pages**
2. Source: "Deploy from a branch"
3. Branch: **main** → `/` (root)
4. Clic en **Save**
5. Tu URL: `https://TU_USUARIO.github.io/zpolar-chess`

¡En 2 minutos está online! 🎉

---

## PASO 3 — Dominio personalizado (opcional)

Si tienes un dominio propio (ej: `zpolar.chess`):
1. En tu proveedor DNS: añadir registro CNAME
   ```
   www → TU_USUARIO.github.io
   ```
2. En GitHub Pages → "Custom domain" → escribe tu dominio

---

## PASO 4 — Crear iconos

Crea una carpeta `icons/` con:
- `icon-192.png` — 192×192 px
- `icon-512.png` — 512×512 px

Herramientas gratuitas:
- **Canva** (canva.com) — plantillas de iconos
- **Favicon.io** (favicon.io) — generador rápido
- Usa el símbolo ♟ sobre fondo oscuro (#0d0d14)

---

## PASO 5 — Subir a Play Store via TWA

TWA (Trusted Web Activity) convierte tu web app en APK.

### 5.1 Instalar Bubblewrap (herramienta de Google)
```bash
npm install -g @bubblewrap/cli
```

### 5.2 Inicializar el proyecto
```bash
mkdir zpolar-twa && cd zpolar-twa
bubblewrap init --manifest https://TU_USUARIO.github.io/zpolar-chess/manifest.json
```

Responde las preguntas:
- Package name: `com.zpolar.chess`
- App name: `ZPolar Chess`
- Short name: `ZPolar`
- Signing key: crear nuevo

### 5.3 Compilar APK
```bash
bubblewrap build
```
Genera: `app-release-signed.apk` y `app-release.aab`

### 5.4 Verificar el dominio (IMPORTANTE para TWA)
Crear el archivo en tu servidor:
```
https://TU_USUARIO.github.io/.well-known/assetlinks.json
```

Contenido (Bubblewrap lo genera automáticamente):
```json
[{
  "relation": ["delegate_permission/common.handle_all_urls"],
  "target": {
    "namespace": "android_app",
    "package_name": "com.zpolar.chess",
    "sha256_cert_fingerprints": ["TU_FINGERPRINT"]
  }
}]
```

### 5.5 Subir a Play Store
1. **https://play.google.com/console** → Crear app
2. Producción → Nueva versión → Sube el `.aab`
3. Completa: descripción, capturas, política de privacidad
4. Enviar a revisión (1-3 días)

---

## Checklist rápido

- [ ] `index.html` abre bien en móvil
- [ ] Iconos 192px y 512px creados
- [ ] Subido a GitHub Pages
- [ ] URL pública funcionando
- [ ] Bubblewrap instalado
- [ ] APK generado y probado
- [ ] Cuenta Google Play ($25 única vez)
- [ ] App subida y en revisión

---

## Tiempos estimados

| Tarea | Tiempo |
|---|---|
| Subir a GitHub Pages | 10 minutos |
| Crear iconos | 20 minutos |
| Generar APK con Bubblewrap | 30 minutos |
| Publicar en Play Store | 1 hora |
| Revisión de Google | 1-3 días |

---

## Alternativas de hosting gratuito

| Plataforma | URL |
|---|---|
| GitHub Pages | github.io |
| Netlify | netlify.app |
| Vercel | vercel.app |
| Cloudflare Pages | pages.dev |

Todas son gratuitas y perfectas para TWA.
