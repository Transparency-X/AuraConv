# **AuraConv: Real-Time Convolution Filter with Dynamic Sample Processing** 🎵

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
| **Block Samples** | Number of audio samples per processing block | 50–2000 samples |
| **Block Duration** | Percentage of each block to process (mute or pass) | 10–90% |
| **Invert Blocking Polarity** | Toggle between muting or passing the selected block portion | On/Off |
| **Auto-Loop Samples** | Automatically modulate block size between min/max in a triangle wave | Min: 50–2000, Max: 50–2000, Loop Time: 0.5–10s |

---
### **🌈 Colored Noise Types**
| **Noise Color** | **Spectral Characteristic** | **Sound Character** | **Common Uses** |
|-----------------|-----------------------------|---------------------|-----------------|
| **White** | Flat spectrum (equal energy per Hz) | Harsh, static-like | General sound design, masking |
| **Pink** | Equal energy per octave (1/f) | Balanced, natural | Relaxation, nature sounds |
| **Brown/Red** | 1/f² (more low-frequency energy) | Deep, rumbling | Sub-bass, textures |
| **Blue** | 1/f^(1/2) (more high-frequency energy) | Bright, hissing | Sparkle, air |
| **Purple/Violet** | 1/f^(2/3) (even more high-frequency) | Very bright, crisp | Digital, futuristic |
| **Green** | Mid-frequency emphasis | Nasal, boxy | Telephone, vintage |
| **Grey** | Psychoacoustically equal loudness | Even perceived volume | Testing, calibration |
| **Black** | Silence (or very low frequency) | None | Mute, pause |

**Bonus:** **Auto-Loop Noise Colors** – Cycle through noise types over a configurable time period (0.5–10s).

---
### **⚡ Polarity Control**
| Option | Microphone | White Noise | Use Case |
|--------|------------|-------------|----------|
| **Neither** | Normal | Normal | Standard processing |
| **Microphone Only** | ✅ Inverted | Normal | Isolate mic phase effects |
| **White Noise Only** | Normal | ✅ Inverted | Isolate noise phase effects |
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
- **3 Default Presets** included (cannot be deleted):
  - **Evolving Atmosphere** – Dynamic, shifting soundscapes
  - **Phase-Swept Drone** – Rich, phase-modulated textures
  - **Spatial Noise Cloud** – 3D immersive noise
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
| **Audio Units for iOS** | iOS/macOS integration | ⭐⭐ |

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
| Browser | AudioWorklet | Microphone Access | Auto-Loop | 3D Rotation | Presets |
|---------|---------------|-------------------|-----------|-------------|---------|
| Chrome | ✅ | ✅ | ✅ | ✅ | ✅ |
| Firefox | ✅ | ✅ | ✅ | ✅ | ✅ |
| Edge | ✅ | ✅ | ✅ | ✅ | ✅ |
| Safari | ⚠️ Partial | ✅ | ✅ | ⚠️ Limited | ✅ |
| Mobile Chrome | ✅ | ✅ | ✅ | ⚠️ Varies | ✅ |

*⚠️ Safari and mobile browsers may have limited AudioWorklet support.*

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
- **Questions?** Check the [FAQ](#faq) below

---
---
## **❓ FAQ**

---
### **🔊 Audio Processing**
#### **Q: What does "Block Samples" mean?**
A: It defines the **size of each processing block** in audio samples. A higher value = larger chunks of audio processed together, creating smoother but less rhythmic effects.

#### **Q: How does Block Duration (50%) work?**
A: It determines **what percentage of each block is affected** by the blocking/muting:
- **50% =** First half of each block is processed
- **10% =** Only the first 10% is affected (short bursts)
- **90% =** First 90% is affected (long silences)

#### **Q: What does Invert Blocking Polarity do?**
A: It **swaps** which part of the block is processed:
- **OFF:** First X% of block is **muted** (silence gaps)
- **ON:** First X% of block is **passed** (chopped bursts)

#### **Q: How does Auto-Loop interact with Block Samples?**
A: Auto-Loop **modulates the Block Samples value** between your min/max settings in a **triangle wave pattern** (min → max → min). The Block Duration percentage is then applied to this **dynamic block size**.

---
### **🎛️ Feature Interactions**
#### **Q: Are all options available with Auto-Loop selected?**
✅ **Yes!** All features work **independently** with Auto-Loop enabled.
- Auto-Loop **only modulates the block size** (samples)
- You can still:
  - Switch audio sources (mic/noise/combined)
  - Apply polarity inversion
  - Adjust block duration
  - Toggle blocking polarity
  - Enable rotation
  - Adjust reverb decay

#### **Q: Should "Invert Blocking Polarity" be available with Auto-Loop?**
✅ **Yes, and it should remain an option.**
- **Auto-Loop** controls **WHAT** (block size)
- **Invert Blocking Polarity** controls **HOW** (mute or pass the block portion)
- They are **orthogonal** (independent) features that can create **evolving rhythmic patterns**

#### **Q: What is the impact of Block Duration: 50% and Convolution Reverb Decay Time?**
| **Parameter** | **What It Does** | **Impact** | **Example** |
|---------------|------------------|------------|-------------|
| **Block Duration: 50%** | Defines **which portion** of each block is processed (muted or passed) | - **50% =** First 50% of samples in each block are affected <br> - Creates rhythmic **silence gaps** or **chopped bursts** | Block Size = 100 samples, Duration = 50% → **First 50 samples muted/passed** |
| **Reverb Decay Time: 3s** | Controls **how long** the reverb tail lasts | - **1s =** Short, tight reverb <br> - **10s =** Long, washy reverb <br> - Applied **after** all other processing | Higher decay = more sustained, ambient effect |

#### **Q: What is the order of processing?**
A: The signal flow is:
1. **Audio Source Selection**
2. **Polarity Inversion** (per source)
3. **Auto-Loop Noise Colors** (if enabled)
4. **Auto-Loop Block Samples** (if enabled)
5. **Block Processing** (size + duration + polarity)
6. **Circular Rotation** (3D spatial)
7. **Convolution Reverb**

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
