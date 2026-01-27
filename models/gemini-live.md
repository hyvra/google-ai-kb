# Gemini Live API

> Real-time, bidirectional streaming for voice and video applications.

---

## Quick Facts

| Attribute | Value |
|-----------|-------|
| Model String | `gemini-2.5-flash-native-audio-preview` |
| Type | Streaming API |
| Latency | Ultra-low (real-time) |
| Modalities | Audio, Video, Text |
| Status | Preview |

---

## What It Is

Gemini Live API enables **real-time, bidirectional streaming** — meaning you can:
- Send audio/video continuously
- Receive responses as they're generated
- Have natural, conversational interactions
- Process live camera/microphone input

---

## When to Use

✅ **Use Gemini Live for:**
- Voice assistants
- Real-time transcription
- Live video analysis
- Interactive voice apps
- Phone/call center AI

❌ **Don't use for:**
- Batch processing
- Text-only applications
- When latency doesn't matter

---

## Key Features

### Native Audio Output

The model can generate speech directly (not just text-to-speech):

```python
import asyncio
import wave
from google import genai

client = genai.Client()

async def voice_conversation():
    async with client.aio.live.connect(
        model="gemini-2.5-flash-native-audio-preview",
        config={"response_modalities": ["AUDIO"]}
    ) as session:
        await session.send_client_content(
            turns={"parts": [{"text": "Tell me a joke"}]}
        )
        
        wf = wave.open("response.wav", "wb")
        wf.setnchannels(1)
        wf.setsampwidth(2)
        wf.setframerate(24000)
        
        async for chunk in session.receive():
            if chunk.data:
                wf.writeframes(chunk.data)
        
        wf.close()

asyncio.run(voice_conversation())
```

### Tool Use in Live Mode

```python
tools = [
    {"google_search": {}},
    {"function_declarations": [
        {"name": "get_weather", "description": "Get weather for location"}
    ]}
]

async with client.aio.live.connect(
    model="gemini-2.5-flash-native-audio-preview",
    config={
        "response_modalities": ["AUDIO"],
        "tools": tools
    }
) as session:
    await session.send_client_content(
        turns={"parts": [{"text": "What's the weather in Tokyo?"}]}
    )
    # Model can search web and respond with audio
```

### Live Video Input

```python
# Stream video frames for real-time analysis
async with client.aio.live.connect(
    model="gemini-2.5-flash-native-audio-preview",
    config={"response_modalities": ["TEXT"]}
) as session:
    # Send video frame
    await session.send_realtime_input(
        media_chunks=[{
            "mime_type": "image/jpeg",
            "data": frame_bytes
        }]
    )
    
    await session.send_client_content(
        turns={"parts": [{"text": "What do you see?"}]}
    )
```

---

## Architecture

```
┌─────────────┐     WebSocket      ┌─────────────────┐
│   Client    │◄──────────────────►│  Gemini Live    │
│  (Browser/  │   Bidirectional    │     API         │
│   Mobile)   │     Streaming      │                 │
└─────────────┘                    └─────────────────┘
      │                                    │
      ▼                                    ▼
  ┌───────┐                         ┌───────────┐
  │ Mic   │                         │  Model    │
  │ Camera│                         │  + Tools  │
  └───────┘                         └───────────┘
```

---

## Pricing

Live API is priced per:
- Audio input duration
- Audio output duration
- Additional tool calls

*Check [official pricing](https://ai.google.dev/pricing) for current rates*

---

## Code Example: Voice Assistant

```python
import asyncio
import pyaudio
from google import genai

client = genai.Client()

RATE = 16000
CHUNK = 1024

async def voice_assistant():
    p = pyaudio.PyAudio()
    
    # Input stream (microphone)
    input_stream = p.open(
        format=pyaudio.paInt16,
        channels=1,
        rate=RATE,
        input=True,
        frames_per_buffer=CHUNK
    )
    
    # Output stream (speaker)
    output_stream = p.open(
        format=pyaudio.paInt16,
        channels=1,
        rate=24000,
        output=True
    )
    
    async with client.aio.live.connect(
        model="gemini-2.5-flash-native-audio-preview",
        config={
            "response_modalities": ["AUDIO"],
            "speech_config": {
                "voice_config": {"prebuilt_voice_config": {"voice_name": "Puck"}}
            }
        }
    ) as session:
        
        async def send_audio():
            while True:
                data = input_stream.read(CHUNK)
                await session.send_realtime_input(
                    media_chunks=[{"mime_type": "audio/pcm", "data": data}]
                )
                await asyncio.sleep(0.01)
        
        async def receive_audio():
            async for chunk in session.receive():
                if chunk.data:
                    output_stream.write(chunk.data)
        
        await asyncio.gather(send_audio(), receive_audio())

asyncio.run(voice_assistant())
```

---

## Voice Options

Available prebuilt voices:
- `Puck` — Playful, energetic
- `Charon` — Calm, measured
- `Kore` — Warm, friendly
- `Fenrir` — Deep, authoritative
- `Aoede` — Bright, clear

```python
config = {
    "speech_config": {
        "voice_config": {
            "prebuilt_voice_config": {
                "voice_name": "Kore"
            }
        }
    }
}
```

---

## Limitations

- **Preview status** — API may change
- **Connection-based** — Requires persistent WebSocket
- **Latency-sensitive** — Needs good network
- **Resource intensive** — Higher compute requirements

---

## Related

- [Gemini 3 Flash](gemini-3-flash.md) — Standard API
- [Tools Overview](../tools/README.md) — Available tools
- [Antigravity](../platforms/antigravity.md) — Uses Live API for voice
