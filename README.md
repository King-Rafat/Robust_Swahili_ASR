<p align="center">
  <a href="https://decodis.com/">
    <img
      src="https://static.wixstatic.com/media/41bde8_fdfad2782d8641edb098e72f1ea10d65~mv2.png/v1/fill/w_185,h_50,al_c,q_85,usm_0.66_1.00_0.01,enc_avif,quality_auto/41bde8_fdfad2782d8641edb098e72f1ea10d65~mv2.png" style="display: inline-block; vertical-align: middle;"
      alt="DECODIS_Website"
    />
  </a>
  </p>
  
# 🧠 A Robust ASR Study for Swahili and Yoruba  
## 🔍 Exploring Benchmark Gaps and Real-World Speech Generalization  

Welcome to our open-source repository exploring **automatic speech recognition (ASR)** in **Swahili** and **Yoruba**, where we investigate how open benchmark datasets compare to **real-world, noisy, conversational speech**.  

**GitHub Repository by** [DECODIS](https://www.decodis.com/)  

We present a complete ablation study using:

- 🌐 Open-source datasets  
- 🗣️ A hand-collected, high-variance real-world dataset  
- 🧪 Three ASR models: Open-Source-only, Custom-only, Combined  

---

## 🚀 Why This Matters  

Low-resource African languages like Swahili and Yoruba are often trained and evaluated on clean, controlled datasets. But real-world usage involves:

- Noisy environments (phones, streets, homes)  
- Spontaneous, conversational phrasing (Non-read out)  
- Speaker and device diversity  
- Non-standard syntax and informal speech  
- Groups not-involved in data freelance  

🔎 We show that **benchmark performance is not a reliable proxy for real-world ASR quality** — and that even a small, well-labeled domain dataset can **improve generalization** meaningfully.

Decodis collects “in the wild” natural language data sets in the course of conducting research with populations who speak low-resource languages.  The audio data is collected by Interactive Voice Recording (IVR) by calling a basic or smartphone.  The interview questions prompt interviewees to answer in open-ended responses. One interview can be completed by 1000+ people in one week, quickly yielding hundreds of hours of natural language data.

---

## 📦 Datasets Used

**Swahili**  
| Dataset | Type | Langs | Hours | Notes |
|--------|------|-------|--------|-------|
| **Open Source Dataset** | Converstional, Read-aloud, crowd-sourced | Swahili | ~400h |Clean studio-style and noisy speech, Mixed mic quality, many speakers, manually labelled |
| **Decodis Custom Dataset** | Conversational, noisy, real-world | Swahili | ~50h | Diverse, high-noise, manually labeled |

**Yoruba**  
| Dataset | Type | Langs | Hours | Notes |
|--------|------|-------|--------|-------|
| **Open Source Dataset** | Converstional, Read-aloud, crowd-sourced | Yoruba | ~40h |Clean studio-style and noisy speech, Mixed mic quality, many speakers, manually labelled |
| **Decodis Dataset** | Conversational, noisy, real-world | Yoruba | ~23h | Diverse, high-noise, manually labeled |


### 🧠 Custom Dataset Highlights

- 🎙️ **Audio type**: Mobile, WhatsApp, interviews, community voice recordings  
- 🗣️ **Speech styles**: Conversational, informal, overlapping, hesitations  
- 🌍 **Geographic & dialect diversity**: Multiple regional accents  
- 🔊 **Noise**: Indoor, outdoor, street, wind, device hum  
- ✅ **Transcript quality**: 90%+ alignment verified by native speakers  
- 🎯 **Use cases**: Real-life human-computer interaction, subtitle generation, local voice assistants  

This dataset is **small but high-quality**, with audio/text that *actually reflects how people speak* — unlike read-aloud, non-diverse, corpora.

---

## 🧪 Model Variants Trained

All models use the same Whisper Large v2 architecture and training setup for controlled comparison.

---

### 🇰🇪 Swahili

#### 1. 🧼 Opensource-Only: 
- Strong benchmark performance, but poor real-world generalization.
- **FLEURS WER**: 13.31%  
- **Decodis WER**: 69.86%  

> 📌 The model performs well on controlled, clean datasets, but collapses on spontaneous speech — suggesting it learns patterns specific to open-source corpora, not transferable language understanding.

#### 2. 🧩 Decodis-Only: `Custom dataset only`
- Trained solely on 50 hours of diverse, noisy real-world audio.
- Surprisingly decent benchmark performance.
- **FLEURS WER**: 34.73% *(improved from 40.00% baseline)*  
- **Decodis WER**: 40.44%  

> ✅ This model generalizes *both ways*: even without access to clean corpora, it learns transferrable acoustic and linguistic patterns that improve FLEURS. This proves the **depth and diversity** of the Decodis data — it's noisy, but rich.

#### 3. 🔀 Combined: `All datasets`
- Balanced performance across both domains.
- **FLEURS WER**: 12.41%  
- **Decodis WER**: 39.42%  

> ✅ This model demonstrates **dual generalization** — solid performance on both clean and noisy environments. The Decodis dataset acts as a generalization booster, adding robustness to a model otherwise fragile to real-world variation.

---

### 🇳🇬 Yoruba

#### 1. 🧼 Opensource-Only: 
- Performs decently on clean test sets.
- Suffers massive degradation on real-world data.
- **FLEURS WER**: 26.18%  
- **Decodis WER**: 81.29%  

> ❌ Like Swahili, this model learns to excel on artificial data but fails on natural language from actual speakers. It is *narrowly overfit* to benchmark formats.

#### 2. 🧩 Decodis-Only: `Custom dataset only`
- Despite being trained on just 23 hours, it generalizes to unseen test types.
- **FLEURS WER**: 66.22%  
- **Decodis WER**: 64.51%  

> ✅ This model shows resilience and real-world generalization. Although worse on benchmarks, it understands conversational, dialectal, noisy speech much better than the opensource-only model. This suggests the Decodis Yoruba corpus is **semantically and acoustically grounded**.

#### 3. 🔀 Combined: `All datasets`
- Overall better balance between benchmark and real-world.
- **FLEURS WER**: 25.44%  
- **Decodis WER**: 62.05%  

> ✅ Including our dataset adds **useful speech variability**. This model generalizes moderately across domains, unlike the benchmark-trained model which fails catastrophically outside its data distribution.

---

## 🔍 Analysis: Is Our Dataset Good?

We asked:

> Is our custom data *hurting* or *helping*?

Here’s the evidence that it is **helping**:

- **FLEURS improved from 40% → 34%** just using our data    
- Domain WER dropped significantly when our data was added (69% → 39%)  
- Models trained with our data are **less fragile** to noise, rephrasing, speaker shifts  

### ✨ Additional Indicators of Quality  

| Metric | Observation |
|--------|-------------|
| Label alignment | Manual double-checking by fluent speakers, 90%+ alignment |
| Noise coverage | Realistic noise (street, indoors, devices, overlapping speech) |
| Spontaneity | Includes hesitation, filler words, false starts |
| Speaker diversity | Varied accents, male/female balance |
| Device diversity | Mobile mics, WhatsApp recordings, low bitrate |

This dataset, though 1/6 the size of the combined corpus, contributes **disproportionately to generalization**. That speaks to **high-quality supervision and relevant acoustic variance**.

---

## 📈 WER Summary

| Language | Model | FLEURS WER | Decodis WER |
|----------|-------|------------|--------------|
| Swahili | Opensource | 12.21%  | 62.86%  |
| Swahili | Decodis Only | 34.73%  | 40.44%  |
| Swahili | Combined | 13.21% | 39.42%  |
| Yoruba | Opensource | 26.18% | 81.29%  |
| Yoruba | Decodis Only | 66.22% | 64.51%  |
| Yoruba | Combined | 25.44% | 62.05%  |

---

## 🤗 Try the Models on Hugging Face  

### Swahili

| Model | Training Data | Description | Hugging Face |
|-------|---------------|-------------|---------------|
| `Swahili Opensource` | Opensource-Only | Clean-only, benchmark-centric | [🔗 View](https://huggingface.co/RafatK/Whisper_Largev2-Swahili-Decodis_Base) |
| `Swahili Custom` | Custom only | Robust real-world ASR | [🔗 View](https://huggingface.co/RafatK/Whisper_Largev2-Swahili-Decodis_FT) |
| `Swahili Combined` | All datasets | General-purpose ASR | [🔗 View](https://huggingface.co/RafatK/Whisper_Largev2-Swahili-Decodis_Comb_FT) |

### Yoruba

| Model | Training Data | Description | Hugging Face |
|-------|---------------|-------------|---------------|
| `Yoruba Opensource` | Opensource-Only | Clean-only, benchmark-centric | [🔗 View](https://huggingface.co/RafatK/Whisper_Largev2-Yoruba-Decodis_Base) |
| `Yoruba Custom` | Custom only | Robust real-world ASR | [🔗 View](https://huggingface.co/RafatK/Whisper_Largev2-Yoruba-Decodis_FT) |
| `Yoruba Combined` | All datasets | General-purpose ASR | [🔗 View](https://huggingface.co/RafatK/Whisper_Largev2-Yoruba-Decodis_Comb_FT) |

---

## 🧪 Community Evaluation & Feedback  

We’re asking the community to **try these models** and help confirm the core insight:

> 📌 **Benchmark WER is not enough. Real-world data is essential.**

Try your own audio, evaluate model predictions, and tell us:

- Does our custom-trained model work better on your speech?  
- Are there accent mismatches or coverage gaps?  
- Does benchmark-trained ASR work well in your environment?  

---

📝 Please try the models and share your feedback, issues, or results via:

- GitHub Issues: Submit an issue  
- Hugging Face Discussions: Join the conversation  

Your feedback will help us refine our dataset and improve ASR for underrepresented languages like Swahili and Yoruba.

---

## 📂 Repository Structure  
- Evaluation notebook  
- Training configs  
- Dataset documentation  

## 📦 Dependencies  

- `transformers`  
- `datasets`  
- `evaluate`  
- `torch`  

---

## 📜 Citation  

```bibtex
@misc{asr_swahili_yoruba_2025,
  title={Robust ASR for Swahili and Yoruba: A Multidataset Ablation Study},
  author={Kazi Rafat},
  year={2025},
  url={https://github.com/King-Rafat/Robust_Swahili_ASR},
}
