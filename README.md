# eco: una interfaz propia para tu Spotify

Una sola página web. En la **computadora** reproduce música directamente en el navegador; en el **celular** funciona como control remoto de la app oficial de Spotify (Spotify no permite reproducir desde navegadores móviles).

## Qué hace
- Carrusel 3D con tus playlists, lo que escuchaste hace poco y tus álbumes guardados.
- Fondo que toma los colores de la portada que está sonando.
- Vinilo que gira mientras suena y reproductor de cristal (aleatorio, repetir, adelantar, me gusta).
- Letra sincronizada por línea (de LRCLIB, un servicio gratuito). Si tocas una línea, la canción salta a ese momento.
- Atajos en la compu: espacio para pausar, flechas para moverte, Esc para cerrar.

## Qué NO hace (y por qué)
- **Karaoke con guía de tono ni puntaje**: Spotify no da las notas de las canciones.
- **Letra palabra por palabra**: LRCLIB casi siempre sincroniza por línea, y algunas canciones no tienen letra.
- **Visualizador que reaccione al audio**: Spotify retiró el análisis de audio y el audio viene cifrado.
- **Recomendaciones ("Para ti")**: Spotify las retiró para apps nuevas.

## Requisitos
- Spotify **Premium** (obligatorio desde febrero de 2026 para apps en modo desarrollo).
- Máximo 5 usuarios autorizados, que agregas en el Dashboard de Spotify.

## Probar sin cuenta
Abre `index.html?demo` desde un servidor local (ver paso 1 de abajo).

## Instalación

### 1. Probar en tu compu
```
cd eco
python -m http.server 8000 --bind 127.0.0.1
```
Abre **http://127.0.0.1:8000/** (debe ser `127.0.0.1`, no `localhost`: Spotify ya no acepta `localhost`).

### 2. Crear la app en Spotify
1. Ve a https://developer.spotify.com/dashboard y crea una app.
2. Marca **Web API** y **Web Playback SDK**.
3. En *Redirect URIs* agrega la dirección exacta que muestra eco en su pantalla de inicio (por ejemplo `http://127.0.0.1:8000/`). Puedes tener varias: agrega también la de GitHub Pages (paso 3).
4. En *User Management* agrega el correo de tu cuenta de Spotify.
5. Copia el **Client ID** y pégalo en eco. No necesitas el Client Secret: eco usa PKCE y nunca lo pide.

### 3. Usarlo en el celular (GitHub Pages)
El celular necesita una dirección `https://`, así que súbelo a GitHub Pages:
1. Crea un repo (por ejemplo `eco`) y sube `index.html`, `fonts/` y `demo/`.
2. En *Settings → Pages* elige la rama `main` y la carpeta raíz.
3. Tu dirección será `https://TU-USUARIO.github.io/eco/`. Agrégala, idéntica y con la `/` final, en *Redirect URIs*.
4. En el celular, ábrela en Safari o Chrome y usa "Agregar a pantalla de inicio" para que se abra a pantalla completa.

Para controlar desde el celular, la app de Spotify tiene que estar abierta (o haber sonado hace poco) en ese teléfono o en otro dispositivo.

## Límites a tener en cuenta
- La cuota de la API es por cuenta de desarrollador. eco consulta el estado cada 5 s en el celular y cada 20 s cuando suena en el navegador, y se detiene cuando la pestaña está en segundo plano. Si se acaba la cuota, te avisa y se pausa un rato.
- El botón "Me gusta" usa los nuevos endpoints `/me/library` de 2026. Si Spotify los cambia, ese botón será lo primero que deje de funcionar.
