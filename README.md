# 🔴 TikTok Live Recorder — GitHub Pages

Grabador de directos de TikTok que funciona **100% en el navegador**, sin servidor, sin instalar nada.

## 🚀 Cómo subir a GitHub Pages

1. Crea un repositorio nuevo en GitHub (puede ser privado o público)
2. Sube el archivo `index.html` a la raíz del repo
3. Ve a **Settings → Pages → Source → Deploy from branch → main → / (root)**
4. En 1-2 minutos tendrás tu URL: `https://TU_USUARIO.github.io/TU_REPO`

---

## ⚙️ Cómo usarlo

### Paso 1 — Obtén la URL del stream M3U8

Necesitas `yt-dlp` instalado una sola vez:

```bash
pip install yt-dlp
yt-dlp --get-url https://www.tiktok.com/@USUARIO/live --cookies cookies.txt
```

Esto te da una URL tipo:
```
https://pull-hls-f19.tiktokcdn.com/.../index.m3u8
```

### Paso 2 — Abre la web y pega la URL

1. Abre tu GitHub Pages
2. Pega las cookies (opcional, para directos privados)
3. Pon el @usuario y el nombre del archivo
4. **Pega la URL M3U8** en el campo ④
5. Pulsa **▶ INICIAR GRABACIÓN**

### Paso 3 — Al terminar

- Pulsa **■ DETENER** cuando quieras parar
- El navegador procesa el vídeo con FFmpeg.wasm
- **Se descarga automáticamente en MP4** ⬇️

---

## 🧠 Cómo funciona por dentro

```
TikTok Stream (M3U8)
        ↓
  Proxy CORS (corsproxy.io)
        ↓
  Navegador descarga segmentos .ts
        ↓
  FFmpeg.wasm ensambla → MP4
        ↓
  Descarga automática al PC
```

- **Sin servidor** — solo HTML + JavaScript
- **Sin instalación** — abre y listo
- **Caché automático** — cookies y configuración guardadas
- **Multi-pestaña** — graba varios directos a la vez

---

## ⚠️ Limitaciones

- Necesitas la URL M3U8 directa (conseguida con yt-dlp una vez)
- Las URLs de stream expiran (~1h), hay que renovarlas
- Directos muy largos (>2h) pueden consumir mucha RAM del navegador

---

## 🛠️ Alternativa con servidor (grabación ilimitada)

Si quieres grabación automática sin URL manual, usa la versión Flask:
- `server.py` — backend Python con yt-dlp integrado
- Resuelve la URL automáticamente y graba sin límite de tiempo
