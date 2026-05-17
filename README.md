# **AuraConv: Real-Time Convolution Filter with Dynamic Sample Processing** 🎵

auraconv-blocky.pages.dev

*Real-time audio convolution and sample manipulation in your browser*

---

## **📌 Overview**

**AuraConv** is a **web-based audio effects processor** that implements a **moving average convolution filter** with **dynamic sample blocking**, **polarity inversion**, **auto-looping modulation**, **3D spatial rotation**, and **colored noise generation**. Built entirely with the **Web Audio API**, it delivers **low-latency, real-time audio processing** directly in your browser—**no installation, plugins, or backend required**.

Whether you're a **sound designer, musician, or audio experimenter**, AuraConv offers a **unique toolkit** for manipulating audio signals in creative ways, from rhythmic chopping to spatial effects and beyond.

---

## **✨ Features**

---

### **🎤 Audio Sources**
| Source | Description | Use Case |
|--------|-------------|----------|
| **Microphone** | Real-time audio input from your device | Voice, instruments, live processing |
| **Colored Noise** | 8 types of colored noise (White, Pink, Brown, Blue, Purple, Green, Grey, Black) | Sound design, textures, masking |
| **Mic + Noise** | Combined microphone and colored noise (mixed at balanced levels) | Hybrid soundscapes, experimental effects |

---

### **🎚️ Sample Processing**
| Feature | Description | Range |
|---------|-------------|-------|
| **Block Samples** | Number of audio samples per processing block | **50–10,000 samples** |
| **Block Duration** | Percentage of each block to process (mute or pass) | 10–90% |
| **Invert Blocking Polarity** | Toggle between muting or passing the selected block portion | On/Off |
| **Auto-Loop Samples** | Automatically modulate block size between min/max in a triangle wave | Min: 50–10,000, Max: 50–10,000, Loop Time: 0.5–10s |

---

### **🌈 Colored Noise Types**
| **Noise Color** | **Spectral Characteristic** | **Sound Character** | **Common Uses** |
|-----------------|-----------------------------|---------------------|-----------------|
| **White** | Flat spectrum (equal energy per Hz) | Harsh, static-like | General sound design, masking |
| **Pink** | Equal energy per octave (1/f) | Balanced, natural | Relaxation, ambient |
| **Brown/Red** | 1/f² (more low-frequency energy) | Deep, rumbling | Sub-bass, textures |
| **Blue** | 1/f^(1/2) (more high-frequency energy) | Bright, hissing | Sparkle, air |
| **Purple/Violet** | 1/f^(2/3) (even more high-frequency) | Very bright, crisp | Digital, futuristic |
| **Green** | Mid-frequency emphasis | Nasal, boxy | Telephone, vintage |
| **Grey** | Psychoacoustically equal loudness | Even perceived volume | Testing, calibration |
| **Black** | Silence (or very low frequency) | None | Mute, pause |

**Bonus:** **Auto-Loop Noise Colors** – Cycle through noise types over a configurable time period (0.5–10s).

---
### **⚡ Polarity Control**
| Option | Microphone | Noise | Use Case |
|--------|------------|-------|----------|
| **Neither** | Normal | Normal | Standard processing |
| **Microphone Only** | ✅ Inverted | Normal | Isolate mic phase effects |
| **Noise Only** | Normal | ✅ Inverted | Isolate noise phase effects |
| **Both** | ✅ Inverted | ✅ Inverted | Full phase cancellation/experimentation |

---
### **🎛️ Spatial & Effects**
| Feature | Description | Range |
|---------|-------------|-------|
| **Circular Rotation (3D Spatial)** | HRTF-based 3D audio positioning (circular motion) | Rate: 0.1–2.0 Hz |
| **Convolution Reverb** | Custom impulse response reverb with adjustable decay | Decay Time: 1–10s |

---
### **💾 Presets System**
- **Save** your current configuration as a named preset
- **Load** presets to instantly apply all settings
- **Delete** custom presets you no longer need
- **5 Default Presets** included (cannot be deleted):
  - **Evolving Atmosphere** – Dynamic, shifting soundscapes
  - **Phase-Swept Drone** – Rich, phase-modulated textures
  - **Spatial Noise Cloud** – 3D immersive noise
  - **Deep Sub-Bass Modulation** – Ultra-low frequency effects
  - **Extreme Slow Motion** – Very slow, tidal modulation
- **Persistent Storage** – Presets saved to browser’s localStorage

---
---
## **📊 Signal Flow & Feature Stacking**

The audio signal flows through these stages **in this exact order**:

```
[AUDIO SOURCE]
       │
       ▼
[POLARITY INVERSION] ───► Mic: ±1, Noise: ±1 (per-source)
       │
       ▼
[AUTO-LOOP NOISE COLORS] ───► Cycles through noise types
       │
       ▼
[AUTO-LOOP BLOCK SAMPLES] ───► Modulates block size (min↔max)
       │
       ▼
[BLOCK PROCESSING]
       ├── Block Size: X samples (static or auto-looped)
       ├── Block Duration: Y% (e.g., 50% = first Y% of samples are affected)
       └── Invert Blocking: Mute affected OR pass affected
       │
       ▼
[CIRCULAR ROTATION] ───► 3D spatial positioning (HRTF panning)
       │
       ▼
[CONVOLUTION REVERB] ───► Decay Time: Z seconds
       │
       ▼
[OUTPUT] ───► To speakers/headphones
```

---
---
## **🚀 Roadmap**

---

### **📌 Short-Term (Next 3–6 Months)**
| Feature | Description | Priority |
|---------|-------------|----------|
| **Multi-Band Processing** | Apply effects to specific frequency bands | ⭐⭐⭐⭐ |
| **Wet/Dry Mix** | Blend processed and unprocessed signals | ⭐⭐⭐⭐ |
| **Visual Feedback** | Real-time waveform/spectrogram display | ⭐⭐⭐⭐ |
| **Custom LFO Waveforms** | Sawtooth, square, triangle waves for auto-loop | ⭐⭐⭐ |
| **Mobile Optimization** | Improved touch controls and performance | ⭐⭐⭐ |
| **Preset Import/Export** | Share presets as JSON files | ⭐⭐⭐ |

---
### **🌟 Long-Term (6–12 Months)**
| Feature | Description | Priority |
|---------|-------------|----------|
| **MIDI Controller Support** | Map parameters to external MIDI devices | ⭐⭐⭐ |
| **Audio File Import/Export** | Process pre-recorded audio | ⭐⭐⭐ |
| **Custom Impulse Responses** | Upload your own IR files for reverb | ⭐⭐ |
| **Multi-Channel Processing** | Stereo/multi-channel support | ⭐⭐ |
| **Plugin Format (VST3/AU)** | Use AuraConv in DAWs | ⭐⭐ |

---
### **💡 Experimental (Future Exploration)**
| Feature | Description | Priority |
|---------|-------------|----------|
| **AI-Powered Filtering** | Auto-adjust parameters based on input audio | ⭐ |
| **Collaborative Mode** | Real-time multi-user audio sessions | ⭐ |
| **WebSocket Streaming** | Stream audio between devices | ⭐ |
| **GPU Acceleration** | Offload processing to WebGL/WebGPU | ⭐⭐ |
| **Machine Learning Effects** | Neural network-based audio processing | ⭐ |

---
---
## **📥 Installation & Usage**

---

### **🚀 Quick Start (No Installation Needed!)**
1. **Download** the latest release from [GitHub Releases](https://github.com/your-username/auraconv-filter/releases)
2. **Extract** the ZIP file
3. **Open `index.html`** in a modern browser (Chrome, Firefox, Edge, Safari)
4. **Click "Start Audio"** and grant microphone permissions if needed

---
### **🎧 Browser Compatibility**
| Browser | AudioWorklet | Microphone Access | Auto-Loop | 3D Rotation | Presets | Background Playback |
|---------|---------------|-------------------|-----------|-------------|---------|-------------------|
| Chrome | ✅ | ✅ | ✅ | ✅ | ✅ | ⚠️ Limited (10-30s) |
| Firefox | ✅ | ✅ | ✅ | ✅ | ✅ | ⚠️ Limited (~1min) |
| Edge | ✅ | ✅ | ✅ | ✅ | ✅ | ⚠️ Limited (10-30s) |
| Safari | ⚠️ Partial | ✅ | ✅ | ⚠️ Limited | ✅ | ❌ No |
| Mobile Chrome | ✅ | ✅ | ✅ | ⚠️ Varies | ✅ | ❌ No |
| Mobile Firefox | ✅ | ✅ | ✅ | ⚠️ Varies | ✅ | ⚠️ Limited (~1min) |

*⚠️ Background playback is limited on mobile browsers to save battery. See [FAQ](#faq) for workarounds.*

---
---
## **🤝 Contributing**
We welcome contributions! Here’s how you can help:

### **🛠️ How to Contribute**
1. **Fork** the repository
2. **Clone** your fork locally
3. **Commit** your changes with clear, descriptive messages
4. **Push** to your fork
5. **Submit a Pull Request** for review

### **📝 Development Setup**
```bash
git clone https://github.com/your-username/auraconv-filter.git
cd auraconv-filter
# Open index.html in your browser to test
```

### **🐛 Reporting Issues**
- **Bugs?** [Open an issue](https://github.com/your-username/auraconv-filter/issues)
- **Feature Requests?** [Start a discussion](https://github.com/your-username/auraconv-filter/discussions)

---
---
## **❓ FAQ**

---
### **🔊 Audio Processing**
#### **Q: What does "Block Samples" mean?**
A: It defines the **size of each processing block** in audio samples. Larger values create **slower, deeper modulation effects**:
- **50-200 samples:** Fast, high-frequency effects (shimmer, flutter)
- **500-1000 samples:** Mid-frequency effects (wah, chopping)
- **2000-5000 samples:** Slow, deep modulation (pulsing, breathing)
- **10,000 samples:** **Extreme slow modulation** (tidal, slow motion)

#### **Q: How different are 5k and 10k from 1k/2k?**
| **Block Size** | **Fundamental Frequency** | **Notch Spacing** | **Gap Length (50%)** | **Effect** |
|----------------|---------------------------|-------------------|------------------------|------------|
| 1000 | 44.1 Hz | 44.1 Hz | 11.35ms | Slow pulsing |
| 2000 | 22.05 Hz | 22.05 Hz | 22.7ms | Very slow pulsing |
| **5000** | **8.82 Hz** | **8.82 Hz** | **56.8ms** | **Deep sub-bass modulation** |
| **10000** | **4.41 Hz** | **4.41 Hz** | **113.5ms** | **Extreme slow motion** |

- **5000 samples:** Very deep, sub-bass modulation (like ocean waves)
- **10000 samples:** Ultra-slow, tidal effects (below typical hearing range but effective for modulation)

#### **Q: What does Block Duration (50%) mean?**
A: It determines **what percentage of each block is affected** by the blocking/muting:
- **50% =** First half of each block is processed (muted or passed)
- **Depth:** ~20-30 dB notches at 50% (clearly audible comb filter effect)

#### **Q: What does Invert Blocking Polarity do?**
A: It **swaps** which part of the block is processed:
- **OFF:** First X% of block is **muted** (silence gaps)
- **ON:** First X% of block is **passed** (chopped bursts)

---
### **🎛️ Feature Interactions**
#### **Q: Are all options available with Auto-Loop selected?**
✅ **Yes!** All features work **independently** with Auto-Loop enabled. Auto-Loop **only modulates the block size** (samples) between your min/max settings.

#### **Q: Should "Invert Blocking Polarity" be available with Auto-Loop?**
✅ **Yes, and it should remain an option.**
- **Auto-Loop** controls **WHAT** (block size)
- **Invert Blocking Polarity** controls **HOW** (mute or pass the block portion)
- They are **orthogonal** (independent) features that can create **evolving rhythmic patterns**

---
### **💻 Technical**
#### **Q: Why does the app need microphone access?**
A: Only if you select **Microphone** or **Mic + Noise** as the audio source. You can use **Colored Noise** without microphone permissions.

#### **Q: Is my audio recorded or stored?**
A: **No.** AuraConv processes audio **in real-time, entirely in your browser**. Nothing is recorded, stored, or sent anywhere.

#### **Q: Can I use this in a DAW?**
A: Not yet, but **VST3/AU plugin support** is on the [roadmap](#🚀-roadmap). For now, use it as a **standalone web app**.

#### **Q: How do I share presets with others?**
A: While presets are saved locally, you can **export/import** them by:
1. Opening your browser’s **Developer Tools** (F12)
2. Going to **Application > Local Storage**
3. Copying the `auraconv-presets` value (JSON)
4. Sharing this with others (they can import via the same method)

#### **Q: Why does audio stop when the app is in the background?**
A: **Browser limitations** – Mobile/Chrome **throttle or pause** JavaScript execution when:
- App is **backgrounded** (switched to another app)
- Tab is **not visible** (switched to another tab)

**Workarounds:**
- **Desktop:** No issue – Chrome/Firefox/Edge **do not throttle** background audio
- **Android:** Disable battery optimization for Chrome, use Firefox, or keep tab in split-screen
- **iOS:** Use Chrome/Firefox (Safari has strict background limits)
- **General:** The app **detects when it returns to focus** and shows a warning to resume

---
---
## **📜 License**
This project is open-source and licensed under the **[MIT License](LICENSE)**.

---
## **🙌 Acknowledgments**
- Inspired by the **JSFX plugin ecosystem** and classic convolution filters
- Built with **Web Audio API** and **AudioWorklet** for real-time performance
- Special thanks to the **open-source audio community** for their tools and libraries

---
## **📬 Support & Community**
- **Follow Us:** [Twitter](https://twitter.com/your-handle) | [Mastodon](https://mastodon.social/@your-handle)
- **Discussions:** [GitHub Discussions](https://github.com/your-username/auraconv-filter/discussions)
- **Bug Reports:** [GitHub Issues](https://github.com/your-username/auraconv-filter/issues)

---
**🎉 Happy Sound Designing!**
*– The AuraConv Team*
