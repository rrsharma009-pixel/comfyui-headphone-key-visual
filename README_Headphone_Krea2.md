# Headphone Product Key Visual — Krea 2

## Overview

This project generates a cinematic product key visual for a premium wireless headphone brand using ComfyUI and the Krea 2 Turbo model. The composition places the headphones on the right side of a 16:9 landscape frame, leaving dark negative space on the left for advertising typography.

## Objective

Create a high-end product-advertising image featuring matte-black and brushed-gold wireless headphones, premium material details, and cinematic cosmic audio effects. The workflow is designed to produce a single 1920 × 1080 image.

## Model and Environment

| Component | Configuration |
|---|---|
| Diffusion model | `Krea2/krea2_turbo_fp8_scaled.safetensors` |
| Model LoRA | `Krea2/galaxyace_krea2.safetensors` |
| LoRA model strength | `1.0` |
| Text encoder | `qwen3VL4BAbliteratedComfyui_v10.safetensors` |
| Text encoder type | `krea2` |
| VAE | `qwen_image_vae.safetensors` |
| ComfyUI workflow format | Native ComfyUI workflow |
| Resolution | `1920 × 1080` |
| Output filename prefix | `HeadPhone` |

The model files are external dependencies and are not included in this repository. The workflow's note includes model-source URLs.

## Prompt

The workflow uses the following positive prompt:

> A cinematic, premium key visual for the wireless headphone brand,serving as the hero product on the right-hand side of a 16:9 landscape framing. A cinematic three-quarter view of the matte-black and brushed-gold wireless headphones, showcasing their premium materials like textured leather on the headband, memory foam ear cups, and metallic joints. The headphones hover gracefully just above a dark, wet-reflective surface.
>
> From the ear cups, mesmerizing, cinematic waves of stardust, cosmic nebula gases in deep indigo, violet, and gold, and glowing digital audio-frequency waves spiral and ripple outward into the darkness, visually representing immersive sound and modern technology. The atmosphere is filled with natural, fine particles of light and mist catching dramatic, cinematic rim and edge-lighting.
>
> The background is a vast, dark, atmospheric environment, beautifully blurred with a shallow depth of field, fading into deep shadows on the left third of the image to provide ample and uncluttered negative space for typography. The shot possesses the high-end quality of a professional product advertisement, with natural lens flare and bokeh, entirely free of watermarks, signatures, or accidental text.

The workflow's prompt node reports `75 / 77 tokens`. This is the prompt stored in the supplied JSON.

## Generation Settings

| Setting | Value |
|---|---|
| Sampler | `euler` |
| Scheduler | `simple` |
| Steps | `16` |
| CFG | `1` |
| Denoise | `1.0` |
| Seed | `50` |
| Seed behavior | `fixed` |
| Latent batch size | `1` |
| Latent dimensions | `1920 × 1080` |

## Workflow

1. Load the Krea 2 Turbo FP8 diffusion model using `UNETLoader`.
2. Load the Qwen3-VL text encoder with `CLIPLoader`, configured for the `krea2` type.
3. Load `qwen_image_vae.safetensors` with `VAELoader`.
4. Apply `galaxyace_krea2.safetensors` through `LoraLoaderModelOnly` at strength `1.0`.
5. Create an empty latent image at 1920 × 1080 with `EmptyLatentImage`.
6. Encode the product-art direction using `CLIPTextEncode`.
7. Create the negative conditioning branch with `ConditioningZeroOut`.
8. Generate the image with `KSampler` using the settings listed above.
9. Decode the generated latent with `VAEDecode`.
10. Preview the image and save the output using the `HeadPhone` filename prefix.

## Image Direction

The prompt specifies the following visual priorities:

- Matte-black and brushed-gold headphones as the hero product.
- Three-quarter product view with visible premium material details.
- Dark, wet-reflective surface below the product.
- Cosmic stardust, nebula gases, and audio-frequency waves in indigo, violet, and gold.
- Cinematic rim lighting, subtle mist, particles, lens flare, and bokeh.
- Deep shadows and uncluttered negative space on the left for advertising copy.
- No watermarks, signatures, or accidental text.

## Evaluation

The generated visual can be reviewed against these criteria:

- The headphones read clearly as the primary product.
- The black and gold materials remain visually distinct.
- Lighting, reflections, and effects support the product rather than obscure it.
- The composition preserves usable negative space on the left.
- The image has a coherent cinematic advertising look.
- No obvious artifacts or unintended text distract from the product.

## Repository Contents

```text
Assessment-2-Headphone-Key-Visual/
├── README.md
├── workflows/
│   └── Headphone_Krea2.json
└── outputs/
    └── HeadPhone.png
```

The output filename shown is the intended name; the actual saved filename may include a ComfyUI counter suffix.

## Installation and Reproduction

1. Install ComfyUI with support for the workflow's native nodes.
2. Install the three model files listed in the **Model and Environment** section in the model directories expected by ComfyUI.
3. Open `Headphone_Krea2.json` in ComfyUI.
4. Confirm the model, text encoder, VAE, and LoRA are available in their loader nodes.
5. Queue the workflow to generate the 1920 × 1080 image.
6. Review the preview and saved output.

## Training

This project uses pretrained-model inference and a pretrained LoRA. No model training or fine-tuning is performed in this workflow.

## Known Limitations

- The result depends on the installed model files, custom model variants, and ComfyUI version.
- The workflow's saved seed is fixed at `50`; reproducing the exact image also depends on compatible model versions and runtime settings.
- Text or brand logos may not render accurately through image generation and may require separate design work if required for a final advertisement.
- The workflow creates one image per run and does not include a separate upscaling stage.
