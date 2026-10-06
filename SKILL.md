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

Photo subject and invariants + COMO sticker treatment + current energy atmosphere + composition + optional low-priority mushroom easter egg + output constraints

Describe the visible subject from the photo, then state what must stay recognizable and what can be stylized. Keep the source image as the only scene reference. Apply the selected energy family as color and graphic language; never treat its palette as proof of anyone else's identity.

| Current energy | Product hue | Graphic direction |
|---|---|---|
| MORO | green | calm and grounded; stable rounded masses or a quiet dot field |
| VEO | yellow / ochre | exploratory and active; directional, offset geometric shapes |
| LUMO | coral red | expressive and social; lively composition with restrained halftone marks |
| SONA | purple | responsive and balanced; paired shapes, soft grid, or echoing arcs |

When working in miniprogram-1, read the exact family colors from miniprogram/components/como-ui/tokens.wxss. The current mapping is MORO green, VEO yellow, LUMO coral red, and SONA purple. Keep energy color separate from feedback/status color. The mushroom is a shared decorative mark, not an energy indicator.

## Standard COMO mushroom easter egg

Use assets/como-mushroom-standard.png as the canonical shape reference whenever a mushroom badge is included. Preserve these traits:

- A broad, slightly asymmetrical hot-pink dome with a thick black outer contour.
- Several uneven warm-ivory patches on the cap, each separated by bold black strokes. Do not replace them with a generic red cap and evenly spaced white circles.
- A curved pale-blush stalk that narrows under the cap and widens into a rounded base, with a thick black outline and one simple inner black curve.
- Treat it as a watermark-like easter egg: one faint, small mark (about 3–5% of canvas width), tucked into existing edge whitespace. Never enlarge it, move the subject to make room, or let it compete with the photo, energy palette, or composition. If there is no quiet space, omit it.
- Use the reference for the mushroom only. Do not copy its large blank canvas into the generated composition.

Composition priority is photo subject and relationships first, energy atmosphere second, chosen layout third, mushroom easter egg last.

### Required visual treatment

- Flat vector sticker with a strong, consistent ink outline, hard edges, high contrast, and a single hard shadow offset down and right.
- No gradients, blur, glossy lighting, photorealistic repainting, or 3D rendering.
- Isolate the sticker on a plain white background. If the chosen generator supports transparency and the user asks for a transparent cutout, preserve that request instead.
- If a mushroom badge fits without changing the composition, include one subtle mark matching the standard shape. Keep it faint and subordinate; never make it a focal element.
- Do not add text, dates, logos, any watermark besides the optional tiny mushroom mark, extra people, or objects absent from the source unless the user explicitly asks.
- Ignore model-specific suffixes such as --v 6.0 unless the selected generator documents that syntax.

## Generate

For a standalone image request, use the available image-generation tool in image-to-image mode and attach the actual supplied photo as the edit target. When both images are available as local files, include assets/como-mushroom-standard.png as a secondary motif-only reference, with the prompt stating that it must remain tiny and faint. If the user photo exists only as a recent conversation attachment, include it and use the morphology description above for the optional easter egg. Do not substitute a text-only generation.

For work inside the COMO mini program, keep generation server-side: call the configured CloudBase function generateImage-3AA3UB with the compiled prompt and the current owner's uploaded photo URL. The image-to-image request has one source-photo input, so describe the optional faint mushroom badge in the prompt rather than adding it as a second model input. Configure the function for model HY-Image-v3.0-I2I-ToB-v1.0.1 and keep the prompt within 500 characters. Do not call the image model directly from the mini-program client or switch providers. Keep the current energy family and source photo bound to the same owner.

## Check and return

- Inspect the generated image at full size and as a small sticker. Check subject recognition, key relationships, energy color, thick outline, lower-right shadow, white isolation, and confirm any mushroom mark is tiny, faint, and subordinate.
- If the main subject or a key relationship was lost, retry once with that invariant stated more concretely. If it still fails, show the result with a brief limitation instead of calling it preserved.
- Show the image first. Keep any note brief and identify the current energy direction and selected composition. Never claim the subject was preserved if the output visibly changed it.
