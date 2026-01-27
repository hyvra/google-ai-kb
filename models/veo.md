# Veo — Video Generation

> Google's state-of-the-art video generation model with native audio.

---

## Quick Facts

| Attribute | Value |
|-----------|-------|
| Current Version | Veo 3.1 |
| Model String | `veo-3.1-generate-preview` |
| Max Duration | 8 seconds (base), 60+ seconds (extended) |
| Resolution | Up to 4K |
| Frame Rate | 24 fps |
| Audio | Native generation |

---

## Key Features

### Native Audio Generation

Veo 3.1 generates synchronized audio:
- Dialogue
- Sound effects
- Ambient noise
- Music

```python
from google import genai

client = genai.Client()

operation = client.models.generate_videos(
    model="veo-3.1-generate-preview",
    prompt="""A wise old sailor on a ship deck, grey beard, speaking:
    "This ocean, it's a force, a wild, untamed might."
    Audio: waves crashing, seagulls, wind"""
)

# Wait for completion
while not operation.done:
    time.sleep(20)
    operation = client.operations.get(operation)

# Save video
for video in operation.response.generated_videos:
    video.save("sailor.mp4")
```

### Scene Extension

Create longer videos by extending from the last frame:

```python
# Generate initial clip
operation = client.models.generate_videos(
    model="veo-3.1-generate-preview",
    prompt="Aerial shot of a forest at sunrise"
)
# ... wait for completion ...

initial_video = operation.response.generated_videos[0]

# Extend the scene
operation2 = client.models.generate_videos(
    model="veo-3.1-generate-preview",
    prompt="The camera descends into the forest canopy",
    video=initial_video  # Continue from last frame
)
```

### Reference Images (Ingredients to Video)

Use images to control characters, objects, and style:

```python
operation = client.models.generate_videos(
    model="veo-3.1-generate-preview",
    prompt="The character walks through a cyberpunk city",
    config={
        "reference_images": [
            character_image,  # Your character design
            style_image       # Visual style reference
        ]
    }
)
```

### Vertical Video

Native support for mobile formats:

```python
operation = client.models.generate_videos(
    model="veo-3.1-generate-preview",
    prompt="A person dancing in a studio",
    config={
        "aspect_ratio": "9:16"  # Vertical for TikTok/Shorts
    }
)
```

---

## Model Versions

| Version | Features | Status |
|---------|----------|--------|
| Veo 3.1 | Native audio, scene extension, references | Current |
| Veo 3.1 Fast | Lower latency, good quality | Current |
| Veo 3 | Native audio (initial release) | Available |
| Veo 2 | No audio, text/image to video | Legacy |

---

## Code Examples

### Text to Video

```python
from google import genai
import time

client = genai.Client()

operation = client.models.generate_videos(
    model="veo-3.1-generate-preview",
    prompt="""
    Cinematic shot: A lone astronaut stands on Mars, 
    red dust swirling around their boots. 
    They look up at Earth in the sky.
    Camera slowly pushes in.
    Audio: wind, breathing, subtle emotional score
    """,
    config={
        "aspect_ratio": "16:9",
        "person_generation": "allow_adult"
    }
)

# Poll for completion
while not operation.done:
    print("Generating...")
    time.sleep(20)
    operation = client.operations.get(operation)

# Save result
video = operation.response.generated_videos[0]
video.save("mars_astronaut.mp4")
```

### Image to Video

```python
# Start with a still image
from PIL import Image
import base64

image = Image.open("landscape.jpg")
# Convert to base64...

operation = client.models.generate_videos(
    model="veo-3.1-generate-preview",
    prompt="Gentle camera push forward, leaves rustling in wind",
    image=image_data,
    config={"aspect_ratio": "16:9"}
)
```

### Upscaling

```python
operation = client.models.generate_videos(
    model="veo-3.1-generate-preview",
    prompt="...",
    config={
        "resolution": "4k"  # or "1080p"
    }
)
```

---

## Prompt Engineering

### Include Camera Direction

```python
# ✅ Good prompt
"""
Dolly shot following a woman walking through a neon-lit alley.
Camera at eye level, tracking smoothly.
Shallow depth of field, bokeh lights in background.
"""

# ❌ Vague prompt
"Woman walking in an alley"
```

### Specify Audio

```python
"""
A thunderstorm over a city skyline.
Audio: thunder rumbles, rain on glass, distant car horns,
       atmospheric synth score building tension
"""
```

### Camera Terminology

| Term | Effect |
|------|--------|
| `dolly` | Camera moves forward/backward |
| `tracking` | Camera follows subject |
| `pan` | Camera rotates left/right |
| `tilt` | Camera rotates up/down |
| `crane` | Camera moves vertically |
| `handheld` | Slight shake, documentary feel |
| `steady` | Smooth, controlled movement |

---

## Pricing

Veo is priced per second of generated video.

| Tier | Approximate Cost |
|------|------------------|
| Standard | $$$ per second |
| 4K upscale | Additional charge |

*Check [official pricing](https://ai.google.dev/pricing)*

---

## Where to Use Veo

| Platform | Access |
|----------|--------|
| Gemini API | Direct API calls |
| AI Studio | Web interface |
| Vertex AI | Enterprise deployment |
| Flow | Creative workflow app |
| YouTube Shorts | Integrated creation |
| Google Vids | Workspace videos |

---

## Safety & Watermarking

All Veo videos include:
- **SynthID** — Invisible watermark in every frame
- **Visible watermark** — Configurable
- **Content filters** — Safety moderation

---

## Limitations

- **Duration**: 8 seconds base (extend with scene extension)
- **Latency**: Generation takes 1-5 minutes
- **Consistency**: Extended scenes may drift
- **Real people**: Limited/restricted

---

## Comparison

| Aspect | Veo 3.1 | Sora 2 |
|--------|---------|--------|
| Max duration | 8s (+extension) | 25s |
| Native audio | ✅ | ❌ |
| Physics | Good | Better |
| Character consistency | Good | Good |
| API access | Yes | Limited |

---

## Related

- [Imagen](imagen.md) — Image generation
- [Gemini Live](gemini-live.md) — Real-time video input
- [AI Studio](../platforms/ai-studio.md) — Test Veo
