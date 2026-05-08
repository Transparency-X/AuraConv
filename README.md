# **AuraConv: Real-Time Convolution Filter with Dynamic Sample Processing** 🎵

AuraConv Logo  
*Real-time audio convolution and sample manipulation in your browser*

---

## **📌 Overview**

**AuraConv** is a **web-based audio effects processor** that implements a **moving average convolution filter** with **dynamic sample blocking**, **polarity inversion**, **auto-looping modulation**, and **3D spatial rotation**. Built entirely with the **Web Audio API**, it delivers **low-latency, real-time audio processing** directly in your browser—no installation, plugins, or backend required.

Whether you're a **sound designer, musician, or audio experimenter**, AuraConv offers a **unique toolkit** for manipulating audio signals in creative ways, from rhythmic chopping to spatial effects and beyond.

---

## **✨ Features**

---

### **🎤 Audio Sources**


| Source          | Description                                                    |
| --------------- | -------------------------------------------------------------- |
| **Microphone**  | Real-time audio input from your device's microphone            |
| **White Noise** | Pure white noise generation                                    |
| **Mic + Noise** | Combined microphone and white noise (mixed at balanced levels) |


---

### **🔄 Sample Processing**


| Feature                      | Description                                                          | Range                                          |
| ---------------------------- | -------------------------------------------------------------------- | ---------------------------------------------- |
| **Block Samples**            | Number of audio samples per processing block                         | 50–2000 samples                                |
| **Block Duration**           | Percentage of each block to process (mute or pass)                   | 10–90%                                         |
| **Invert Blocking Polarity** | Toggle between muting or passing the selected block portion          | On/Off                                         |
| **Auto-Loop Samples**        | Automatically modulate block size between min/max in a triangle wave | Min: 50–2000, Max: 50–2000, Loop Time: 0.5–10s |


---

### **⚡ Polarity Control**


| Option               | Microphone | White Noise | Use Case                                |
| -------------------- | ---------- | ----------- | --------------------------------------- |
| **Neither**          | Normal     | Normal      | Standard processing                     |
| **Microphone Only**  | ✅ Inverted | Normal      | Isolate mic phase effects               |
| **White Noise Only** | Normal     | ✅ Inverted  | Isolate noise phase effects             |
| **Both**             | ✅ Inverted | ✅ Inverted  | Full phase cancellation/experimentation |


---

### **🎚️ Spatial & Effects**


| Feature                            | Description                                          | Range             |
| ---------------------------------- | ---------------------------------------------------- | ----------------- |
| **Circular Rotation (3D Spatial)** | HRTF-based 3D audio positioning (circular motion)    | Rate: 0.1–2.0 Hz  |
| **Convolution Reverb**             | Custom impulse response reverb with adjustable decay | Decay Time: 1–10s |


---

## **🔍 Signal Flow & Feature Stacking**

---

### **📊 Processing Order**

The audio signal flows through these stages **in this exact order**:

```
[AUDIO SOURCE]
       │
       ▼
[POLARITY INVERSION] ───► Mic: ±1, Noise: ±1 (per-source)
       │
       ▼
[AUTO-LOOP] ───► Block Size: min ↔ max (triangle wave)
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

### **🔧 Feature Interaction Table**


| **Feature**            | **Audio Source** | **Polarity Inversion** | **Auto-Loop**           | **Block Processing**   | **Rotation**      | **Reverb**      |
| ---------------------- | ---------------- | ---------------------- | ----------------------- | ---------------------- | ----------------- | --------------- |
| **Audio Source**       | ✅ Primary        | ✅ Applied per-source   | ✅ Independent           | ✅ Independent          | ✅ Independent     | ✅ Independent   |
| **Polarity Inversion** | ✅ Before mixing  | ✅ **Core**             | ✅ Independent           | ✅ Independent          | ✅ Independent     | ✅ Independent   |
| **Auto-Loop**          | ✅ Independent    | ✅ Independent          | ✅ **Core**              | ✅ Modulates block size | ✅ Independent     | ✅ Independent   |
| **Block Processing**   | ✅ Independent    | ✅ Independent          | ✅ Uses auto-looped size | ✅ **Core**             | ✅ Before rotation | ✅ Before reverb |
| **Rotation**           | ✅ Independent    | ✅ Independent          | ✅ Independent           | ✅ After blocking       | ✅ **Core**        | ✅ Before reverb |
| **Reverb**             | ✅ Independent    | ✅ Independent          | ✅ Independent           | ✅ After blocking       | ✅ After rotation  | ✅ **Core**      |


---

### **❓ Feature Stacking FAQ**

#### **1. Are all options available with Auto-Loop selected?**

✅ **Yes!** All features work **independently** with Auto-Loop enabled.

- Auto-Loop **only modulates the block size** (samples)
- You can still:
  - Switch audio sources (mic/noise/combined)
  - Apply polarity inversion
  - Adjust block duration
  - Toggle blocking polarity
  - Enable rotation
  - Adjust reverb decay

**Example:** Auto-loop block size from 100–1000 samples while inverting mic polarity and using 3D rotation.

---

#### **2. Should "Invert Blocking Polarity" be available with Auto-Loop?**

✅ **Yes, and it should remain an option.**

- **Auto-Loop** controls **WHAT** (block size)
- **Invert Blocking Polarity** controls **HOW** (mute or pass the block portion)
- They are **orthogonal** (independent) features:
  - Auto-Loop: `Block Size = 100 → 1000 → 100` (triangle wave)
  - Invert Blocking: `Mute first 50%` **OR** `Pass first 50%` (static choice)
- **Combined Effect:** Creates **evolving rhythmic patterns** where both the block size *and* the processing behavior can change over time.

---

#### **3. Impact of Block Duration (50%) and Convolution Reverb Decay Time?**


| **Parameter**             | **What It Does**                                                       | **Impact**                                                                                                                                                        | **Example**                                                                  |
| ------------------------- | ---------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| **Block Duration: 50%**   | Defines **which portion** of each block is processed (muted or passed) | - **50% =** First 50% of samples in each block are affected - **10% =** Only first 10% affected (shorter bursts) - **90% =** First 90% affected (longer silences) | Block Size = 100 samples, Duration = 50% → **First 50 samples muted/passed** |
| **Reverb Decay Time: 3s** | Controls **how long** the reverb tail lasts                            | - **1s =** Short, tight reverb - **10s =** Long, washy reverb - Applied **after** all other processing                                                            | Higher decay = more sustained, ambient effect                                |


**Key Insight:**

- Block Duration affects **rhythmic chopping** (time domain)
- Reverb Decay affects **spatial depth** (frequency domain)
- They **stack additively** for complex textures.

---

### **🎨 Visual Representation of Signal Impact**

#### **📈 Single Source (Microphone) Flow**

```
[Mic Input]
    │
    ▼ (Polarity: Normal or -1)
[Polarity Inversion]
    │
    ▼ (Block Size: Static or Auto-Looped)
[Block Processing: 100 samples]
    │
    ├──► First 50 samples (50% duration): MUTE or PASS (based on Invert Blocking)
    └──► Remaining 50 samples: PASS or MUTE
    │
    ▼ (3D Positioning)
[Circular Rotation: Front → Left → Back → Right]
    │
    ▼ (Spatial Depth)
[Convolution Reverb: 3s Decay]
    │
    ▼
[Output: Processed Audio]
```

#### **📊 Combined Source (Mic + Noise) Flow**

```
[Mic Input] ──► [Polarity: ±1] ──┐
                                     ├──► [Mixer] ──► [Block Processing] ──► [Rotation] ──► [Reverb]
[Noise Input] ──► [Polarity: ±1] ──┘
```

- **Mic and Noise** are **independently polarity-inverted** before mixing
- **Block Processing** applies to the **mixed signal**
- **Rotation** positions the **mixed, processed signal** in 3D space
- **Reverb** adds depth to the **final output**

---

#### **🎚️ Auto-Loop + Block Processing Interaction**

```
Time: 0s ┬─────────┬─────────┬─────────┬─────────┐
         │ Block:50 │ Block:500│ Block:50 │ Block:500│
         │          │          │          │          │
Auto-Loop:│    ▲    │     ▼    │    ▲    │     ▼    │ (Triangle Wave: 50↔500)
         │          │          │          │          │
Block    :│[MUTE 25]│[MUTE 250]│[MUTE 25]│[MUTE 250]│ (50% Duration)
Duration:│         │          │         │          │
         └─────────┴─────────┴─────────┴─────────┘
           Samples: 50 100 150 200 250 300...
```

- **Auto-Loop** modulates block size **over time**
- **Block Duration** (50%) always mutes/passes the **first half** of the current block
- **Result:** Rhythmic pattern where **both block size and mute length change**

---

## **🚀 Roadmap**

---

### **📌 Short-Term (Next 3–6 Months)**


| Feature                  | Description                                    | Priority |
| ------------------------ | ---------------------------------------------- | -------- |
| **Preset System**        | Save/load/share custom configurations          | ⭐⭐⭐⭐     |
| **Visual Feedback**      | Real-time waveform/spectrogram display         | ⭐⭐⭐⭐     |
| **Custom LFO Waveforms** | Sawtooth, square, triangle waves for auto-loop | ⭐⭐⭐      |
| **Wet/Dry Mix**          | Blend processed and unprocessed signals        | ⭐⭐⭐⭐     |
| **Mobile Optimization**  | Improved touch controls and performance        | ⭐⭐⭐      |


---

### **🌟 Long-Term (6–12 Months)**


| Feature                      | Description                               | Priority |
| ---------------------------- | ----------------------------------------- | -------- |
| **MIDI Controller Support**  | Map parameters to external MIDI devices   | ⭐⭐⭐      |
| **Multi-Band Processing**    | Apply effects to specific frequency bands | ⭐⭐       |
| **Audio File Import/Export** | Process pre-recorded audio                | ⭐⭐⭐      |
| **Custom Impulse Responses** | Upload your own IR files for reverb       | ⭐⭐       |
| **Plugin Format (VST3/AU)**  | Use AuraConv in DAWs                      | ⭐⭐       |


---

### **💡 Experimental (Future Exploration)**


| Feature                      | Description                                 | Priority |
| ---------------------------- | ------------------------------------------- | -------- |
| **AI-Powered Filtering**     | Auto-adjust parameters based on input audio | ⭐        |
| **Collaborative Mode**       | Real-time multi-user audio sessions         | ⭐        |
| **WebSocket Streaming**      | Stream audio between devices                | ⭐        |
| **GPU Acceleration**         | Offload processing to WebGL/WebGPU          | ⭐⭐       |
| **Machine Learning Effects** | Neural network-based audio processing       | ⭐        |


---

## **📥 Installation & Usage**

---

### **🚀 Quick Start (No Installation Needed!)**

1. **Download** the latest release from [GitHub Releases](https://github.com/your-username/auraconv-filter/releases)
2. **Extract** the ZIP file
3. **Open `index.html**` in a modern browser (Chrome, Firefox, Edge, Safari)
4. **Click "Start Audio"** and grant microphone permissions if needed

---

### **🎧 Browser Compatibility**


| Browser       | AudioWorklet | Microphone Access | Auto-Loop | 3D Rotation |
| ------------- | ------------ | ----------------- | --------- | ----------- |
| Chrome        | ✅            | ✅                 | ✅         | ✅           |
| Firefox       | ✅            | ✅                 | ✅         | ✅           |
| Edge          | ✅            | ✅                 | ✅         | ✅           |
| Safari        | ⚠️ Partial   | ✅                 | ✅         | ⚠️ Limited  |
| Mobile Chrome | ✅            | ✅                 | ✅         | ⚠️ Varies   |


*⚠️ Safari and mobile browsers may have limited AudioWorklet support.*

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

## **❓ FAQ**

---

### **🔊 Audio Processing**

#### **Q: What does "Block Samples" mean?**

A: It defines the **size of each processing block** in audio samples. A higher value = larger chunks of audio processed together, creating smoother but less rhythmic effects.

#### **Q: How does Block Duration (50%) work?**

A: It determines **what percentage of each block is affected** by the blocking/muting:

- **50% =** First half of each block is muted (or passed, if Invert Blocking is on)
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

#### **Q: Can I use all features at once?**

A: **Yes!** All features are designed to work together. For example:

- Auto-loop block size from 100–1000 samples
- Invert mic polarity
- Set block duration to 30%
- Enable 3D rotation
- Add 5s reverb decay

#### **Q: Does the order of features matter?**

A: **Yes, but it's fixed.** The processing order is:

1. Audio Source + Polarity Inversion
2. Auto-Loop (modulates block size)
3. Block Processing (size + duration + polarity)
4. Circular Rotation
5. Convolution Reverb

This order ensures **predictable results** when stacking features.

---

### **💻 Technical**

#### **Q: Why does the app need microphone access?**

A: Only if you select **Microphone** or **Mic + Noise** as the audio source. You can use **White Noise** without microphone permissions.

#### **Q: Is my audio recorded or stored?**

A: **No.** AuraConv processes audio **in real-time, entirely in your browser**. Nothing is recorded, stored, or sent anywhere.

#### **Q: Can I use this in a DAW?**

A: Not yet, but **VST3/AU plugin support** is on the [roadmap](#🚀-roadmap). For now, use it as a **standalone web app**.

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
