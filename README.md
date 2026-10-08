# LTX-2.5 en ComfyUI con una AMD — flujos en español

Flujos del tutorial **«Videos con IA en tu PC con una AMD»** de **El Dino Porthos** (YouTube: @eldinoporthos).

| Archivo | Qué es |
|---|---|
| **`ltx25_receta_porthos_es.json`** | El recomendado: LTX-2.5 imagen a video **optimizado** (hasta 6× más rápido) y en español |
| `ltx25_plantilla_es.json` | La plantilla oficial de ComfyUI, solo traducida (para comparar) |

## Cómo usarlo
1. Haz clic en **`ltx25_receta_porthos_es.json`** (arriba) y pulsa el botón **«Download raw file»** (la flechita ⬇ arriba a la derecha).
2. Abre **ComfyUI** y **arrastra el archivo** desde tu carpeta de Descargas encima del lienzo. Al soltarlo, el flujo aparece.
   (También: menú *Flujo de trabajo → Abrir*.)
3. Descarga los modelos de https://huggingface.co/Lightricks/LTX-2.5 (acepta antes la licencia) y ponlos en `ComfyUI/models/`:

| Carpeta | Archivo | Peso |
|---|---|---|
| `diffusion_models` | ltx-2.5-22b-distilled-transformer-comfy-int8-convrot.safetensors | 21,5 GB |
| `text_encoders` | gemma4-12b-with-proj-ltx-2.5-comfy-int8-convrot.safetensors | 15,4 GB |
| `vae` | ltx-2.5-video-vae-conv-bf16.safetensors | 1,5 GB |
| `vae` | ltx-2.5-audio-vae-bf16.safetensors | 0,4 GB |
| `latent_upscale_models` | ltx-2.5-latent-spatial-upscaler-x2-bf16-1.0.safetensors | 1,0 GB |

## Qué cambia la receta
1. **Atención INT8**: nodo «Backend de atención del modelo» → `comfy kitchen attention`
2. **Sigmas de la etapa 2**: `0.909375, 0.725, 0.421875, 0.0`
3. **Sampler de la etapa 2**: `euler`
4. **VAE de video**: `ltx-2.5-video-vae-conv-bf16`
5. **Decodificar el video**: tamaño temporal `4096` (sin bloques: evita el fotograma roto cada ~2 s)
- Sin el mejorador de descripciones (en AMD escribía texto sin sentido).
- **Texto a video**: dentro de la cajita grande, grupo «Ajustes del video» → «¿Texto a video (sin imagen)?» en `true`.

Medido en: AMD Radeon RX 9070 XT 16 GB · Ryzen 9 9950X3D · 48 GB de RAM · Windows 11 (ComfyUI con ROCm).
1080p · 15 s: **57 min con la plantilla → 9 min con la receta**.

Libre para usar y compartir.
