# FL Studio AI — AI Beat Maker & Music Production Engine

> **AI-powered beat generation, synthesis, mixing, and mastering — with MCP server integration for Claude Code and OpenCode**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)
[![Stars](https://img.shields.io/github/stars/IzzoIzzoIzzo/FL-STUDIO-AI?style=social)](https://github.com/IzzoIzzoIzzo/FL-STUDIO-AI)
[![Status](https://img.shields.io/badge/status-pre--release%20v8.0-blueviolet)](https://github.com/IzzoIzzoIzzo/FL-STUDIO-AI)
[![Python](https://img.shields.io/badge/python-3.8%2B-blue)](https://python.org)

---

## What It Is

**FL Studio AI** is a modular Python music production system that generates complete beats, melodies, chord progressions, basslines, and synthesizer patches — no manual piano roll entry required.

It works three ways:

- **MCP Server** — expose music tools (`generate_beat`, `synthesize_sound`, `mix_track`) directly to any MCP-compatible AI assistant (Claude Code, OpenCode). Ask your AI to make a beat; it calls the server and returns MIDI data ready for FL Studio.
- **REST API** — Flask server on `localhost:5000`. HTTP endpoints for every feature, curl-friendly, integrates with any frontend or script.
- **CLI / Python** — Direct command-line invocation for automation and batch workflows.
- **Browser DAW** (`studio.html`) — Standalone web UI with beats, synth, drum machine, sequencer, mixer, and export — no backend required.

> **Status:** Pre-Release v8.0 — 100+ Python modules, 20/20 core tests passing, all systems operational.

---

## Features (What Works Today)

### Beat & Track Generation
- 15+ genre styles: trap, house, hip hop, techno, lo-fi, dubstep, drum & bass, UK drill, garage, jungle, ambient, and more
- Natural language input: `python beatmaker.py make "dark trap beat in A minor 160 bpm"`
- Full song structure (intro, verse, chorus, outro) via `auto_creator.py`
- MIDI export ready for FL Studio piano roll

### Synthesis Engine
- 47+ presets across 11 categories (leads, bass, pads, plucks, keys, strings, brass, FX, bells, SFX, special)
- 5 synthesis methods: Wavetable, FM, Granular, Additive, Physical Modeling
- Additional methods: Karplus-Strong, Modal, Vector, Analog Modeling, Circuit Modeling
- ADSR envelopes, LFO modulation, filter bank, real-time arpeggiator
- 47 virtual instruments across bass, keys, pads, leads, drums, FX

### Drum Machine
- 5 kits: 808, trap, house, hip hop, techno
- Polyrhythms, polymeter, swing, humanization, groove templates
- 200+ patterns, 100+ styles in the pattern library

### AI Composition
- `ai_melody_engine.py` — neural melody and chord generation with emotion profiles
- `neural_music_generator.py` — LSTM-style composition with style transfer
- `music_theory_engine.py` — 50+ scales, 100+ chord types, voice leading
- `advanced_ai_composer.py` — 8 AI models: Markov Chain, LSTM, Style Transfer, Arrangement AI, and more

### Mixing & Mastering
- 8-channel mixer with EQ, compression, sends/returns, metering
- Stem separator — extract drums, bass, vocals, melody from audio
- Vocal processor — pitch, harmonizer, vocoder
- Mastering engine — 6 modes: analog, modern, vinyl, cassette, tape, digital. LUFS normalization
- Effects rack — EQ, compressor, saturator, delay, reverb, chorus, flanger, phaser, distortion
- Sidechain compression with envelope shaping

### Analysis Tools
- BPM detection, key detection, pitch tracking
- FFT spectrum analysis
- Audio format converter

### Creative / Esoteric (Early / Experimental)
- `esoteric_music_engine.py` — sacred geometry tuning, 528Hz Solfeggio frequencies, Solfeggio healing, binaural beat generation
- `music_color_cymatics.py` — frequency-to-color mapping, cymatic pattern visualization

### Browser DAW (`studio.html`)
- Single-file, zero-install — open in any browser
- Tabs: Beats, Synth, Drums, Sequencer, Mixer, Export, Settings
- Piano roll canvas, real-time audio via Web Audio API
- LLM prompt-to-music (connects to Ollama / Groq / OpenAI / Anthropic / Gemini via settings)
- MIDI / WAV export

---

## Quick Start

### 1. Start the API Server

```bash
python flstudio_ai_api.py
# Server runs at http://localhost:5000
```

### 2. Generate a Beat (CLI)

```bash
# Style + tempo + bars
python beatmaker.py generate trap 150 16

# Natural language
python beatmaker.py make "dark lofi beat in A minor"

# Full production (structure + mix + master)
python auto_creator.py
```

### 3. Use the Browser DAW (no server needed)

```
Open studio.html in your browser
```

### 4. Start the MCP Server (for Claude Code / OpenCode)

```bash
python flstudio_mcp_server_v2.py
# or
START_FLSTUDIO_MCP.bat
```

Then ask your AI assistant:
```
"Make a trap beat at 160 BPM in A minor"
"Generate a chord progression in D minor"
"Start playback in FL Studio"
```

---

## MCP Tools

When the MCP server is running at `localhost:5000`, these tools are available to any MCP client:

| Tool | Description |
|------|-------------|
| `generate_track` | Full track — drums, bass, melody, chords |
| `generate_drums` | Drum pattern in any style |
| `generate_bass` | Bassline with scale and pattern |
| `generate_melody` | Melody with scale and rhythm density |
| `generate_chords` | Chord progression with voicing |
| `flstudio_play` | Start FL Studio playback |
| `flstudio_stop` | Stop playback |
| `flstudio_record` | Toggle recording |
| `flstudio_new_pattern` | Create new pattern |
| `flstudio_piano_roll` | Open piano roll |
| `get_note_data` | Retrieve all note data |
| `get_midi_notes` | Retrieve MIDI format note data |

**Example call:**
```json
POST /mcp/call
{
  "tool": "generate_track",
  "arguments": {
    "style": "trap",
    "tempo": 150,
    "key": 57,
    "scale": "minor",
    "bars": 16
  }
}
```

---

## REST API Reference

```bash
# Generate a full track
curl -X POST http://localhost:5000/generate/track \
  -H "Content-Type: application/json" \
  -d '{"style":"house","key":60,"scale":"minor","bars":8,"tempo":128}'

# Generate drums only
curl -X POST http://localhost:5000/generate/drums \
  -d '{"style":"trap","bars":2}'

# Analyze key + BPM
curl -X POST http://localhost:5000/analyze/key
curl -X POST http://localhost:5000/analyze/bpm

# Mastering suggestion
curl http://localhost:5000/master/suggest
```

Key endpoints: `/generate/track` · `/generate/drums` · `/generate/bass` · `/generate/melody` · `/generate/chords` · `/generate/arps` · `/analyze/key` · `/analyze/bpm` · `/automation/volume` · `/samples/search` · `/creative/variations` · `/creative/fills`

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Language | Python 3.8+ |
| API server | Flask |
| Audio | numpy, scipy (DSP), soundfile |
| MIDI | python-midi, mido |
| MCP protocol | HTTP/JSON (Model Context Protocol) |
| FL Studio bridge | OSC (python-osc), pyautogui |
| Browser DAW | Vanilla HTML/CSS/JS, Web Audio API |
| AI composition | Custom Markov Chain, LSTM-style, style transfer |
| LLM integration | Ollama (local), Groq, OpenAI, Anthropic, Gemini (optional) |

**Dependencies (install once):**
```bash
pip install flask python-osc pyautogui numpy scipy soundfile mido
```

---

## Verification & Tests

```bash
# Quick test all 19 core modules
python debug_verify.py

# Comprehensive test suite (20/20)
python final_test_100.py

# End-to-end production test
python e2e_test.py

# Extended test suite
python test_suite_v2.py
```

Individual module tests:
```bash
python test_synth_quick.py
python test_mixer_quick.py
python test_analysis_quick.py
```

---

## Project Structure

```
AI FL STUDIO BUILD/
├── flstudio_ai_api.py          Main REST API (Flask, port 5000)
├── flstudio_mcp_server_v2.py   MCP protocol server (AI IDE integration)
├── beatmaker.py                Simple CLI beat generator
├── auto_creator.py             Full song generation
├── studio.html                 Browser DAW (single-file, no server needed)
├── launcher.py / launcher_web.html  Launcher UI
│
├── super_engine.py             Beat generation, 15+ styles
├── ai_melody_engine.py         Neural melody composition
├── neural_music_generator.py   LSTM-style + style transfer
├── music_theory_engine.py      50+ scales, 100+ chord types
├── advanced_synth.py           47+ presets, 5 synthesis methods
├── extensive_synth_engine.py   7 extended synthesis methods
├── drum_machine_v3.py          5 kits + patterns + fills
├── mixer_v3.py                 8-channel mixer
├── mastering_engine.py         6 mastering modes + LUFS
├── effects_rack.py             9-effect chain
├── stem_separator.py           Drum/bass/vocal/melody extraction
├── audio_analyzer.py           BPM, key, FFT spectrum
├── esoteric_music_engine.py    Sacred geometry, 528Hz, binaural (experimental)
├── music_color_cymatics.py     Frequency-to-color visualization (experimental)
│
├── audio/                      Audio assets and samples
├── exports/                    Generated MIDI and audio outputs
├── presets/                    Sound presets and configurations
│
└── 00 INDEX.md – 22 MODULATION.md   22 reference documentation files
```

---

## Roadmap

- [ ] Direct FL Studio OSC write-back (patterns → FL Studio in real-time)
- [ ] Persistent project save/load (`.flp`-adjacent format)
- [ ] SHADDAI Orchestration Layer (SOL) — 7-agent AI council controlling the music engine
- [ ] Pattern learning from user history (`23 PATTERN LEARNING.md`)
- [ ] Mobile-optimized browser DAW
- [ ] HuggingFace Spaces demo deployment
- [ ] VST plugin wrapper (long-term)

> Early/experimental modules are marked in the Features section above. The core generation, synthesis, mixing, and API pipeline is operational.

---

## License

MIT — Use freely. Build legacy.

---

<p align="center">
  Built by <a href="https://x.com/IzzoSol"><strong>IzzoSol</strong></a> &nbsp;·&nbsp;
  <a href="https://x.com/shaddaiAI">@shaddaiAI</a> &nbsp;·&nbsp;
  Part of the ⚡ <a href="https://github.com/IzzoIzzoIzzo/Shaddai"><strong>SHADDAI ecosystem</strong></a>
</p>
