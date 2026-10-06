---
name: como-energy-sticker-i2i
description: Turn one user-provided photo into a flat-vector COMO sticker whose color and graphic atmosphere follow the user's existing current energy field. Use for image-to-image sticker creation or implementing this flow in the COMO mini program.
---

# COMO 能量贴纸

Use the uploaded photo as the edit target and the user's existing current energy as the visual direction. Make a recognizable sticker from the actual subject in the photo; do not replace it with the prompt example of a coffee scene.

## Resolve the two inputs

- Use the image the user supplied for this request. Inspect it before writing the prompt. Preserve its main subject, defining silhouette, object count, and important spatial relationships.
- In a COMO app context, read the current energy value from the existing owner-scoped current-energy field (readEnergyNow() / the already-derived meFamily). Do not infer energy from the person's appearance, photo colors, scene, text, or personality.
- If the current energy field cannot be read, do not invent one or silently choose a family. Tell the user it is unavailable and ask them to select an energy.
- Use only the image and energy needed for this generation. Do not add unrelated profile details or expose private identifiers.

## Build the image prompt

Compose one concise image-to-image prompt in this order:

Photo subject and invariants + COMO sticker treatment + current energy atmosphere + required sticker details + output constraints

Describe the visible subject from the photo, then state what must stay recognizable and what can be stylized. Keep the source image as the only scene reference. Apply the selected energy family as color and graphic language; never treat its palette as proof of anyone else's identity.

| Current energy | Product hue | Graphic direction |
|---|---|---|
| MORO | green | calm and grounded; stable rounded masses or a quiet dot field |
| VEO | yellow / ochre | exploratory and active; directional, offset geometric shapes |
| LUMO | coral red | expressive and social; lively composition with restrained halftone marks |
| SONA | purple | responsive and balanced; paired shapes, soft grid, or echoing arcs |

When working in miniprogram-1, read the exact family colors from miniprogram/components/como-ui/tokens.wxss. The current mapping is MORO green, VEO yellow, LUMO coral red, and SONA purple. Keep energy color separate from feedback/status color. A small pink mushroom badge is a shared decorative mark, not an energy indicator.

### Required visual treatment

- Flat vector sticker with a strong, consistent ink outline, hard edges, high contrast, and a single hard shadow offset down and right.
- No gradients, blur, glossy lighting, photorealistic repainting, or 3D rendering.
- Isolate the sticker on a plain white background. If the chosen generator supports transparency and the user asks for a transparent cutout, preserve that request instead.
- Include one small pink mushroom badge with light spots, placed on a suitable object or near the sticker edge. Keep it secondary to the photo's subject.
- Do not add text, dates, logos, watermarks, extra people, or objects absent from the source unless the user explicitly asks.
- Ignore model-specific suffixes such as --v 6.0 unless the selected generator documents that syntax.

## Generate

For a standalone image request, use the available image-generation tool in image-to-image mode and attach the actual supplied photo as the reference. If the image is already available as a local file, use its local path; if it exists only as a recent conversation attachment, include that attachment. Do not substitute a text-only generation.

For work inside the COMO mini program, keep generation server-side: call the configured CloudBase function generateImage-3AA3UB with the compiled prompt and the current owner's uploaded photo URL. Configure it for model HY-Image-v3.0-I2I-ToB-v1.0.1 and keep the prompt within 500 characters. Do not call the image model directly from the mini-program client or switch providers. Keep the current energy family and source photo bound to the same owner.

## Check and return

- Inspect the generated image at full size and as a small sticker. Check subject recognition, key relationships, energy color, thick outline, lower-right shadow, white isolation, and the small mushroom badge.
- If the main subject or a key relationship was lost, retry once with that invariant stated more concretely. If it still fails, show the result with a brief limitation instead of calling it preserved.
- Show the image first. Keep any note brief and identify the current energy direction and selected composition. Never claim the subject was preserved if the output visibly changed it.
