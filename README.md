# 🧠 A Robust ASR Study for Swahili
## 🔍 Exploring Benchmark Gaps and Real-World Speech Generalization

Welcome to our open-source repository exploring **automatic speech recognition (ASR)** in **Swahili**, where we investigate how open benchmark datasets compare to **real-world, noisy, conversational speech**. 

**GitHub Repository by** [DECODIS](https://www.decodis.com/)

We present a complete ablation study using:

- 🌐 Open-source datasets (Common Voice + FLEURS + OPENSLR)
- 🗣️ A hand-collected, high-variance real-world dataset
- 🧪 Three ASR models: Clean-only, Domain-only, Combined

---

## 🚀 Why This Matters

Low-resource African languages like Swahili and Yoruba are often trained and evaluated on clean, controlled datasets. But real-world usage involves:

- Noisy environments (phones, streets, homes)
- Spontaneous, conversational phrasing (Non-read out)
- Speaker and device diversity
- Non-standard syntax and informal speech
- Groups not-involved in data freelance.

🔎 We show that **benchmark performance is not a reliable proxy for real-world ASR quality** — and that even a small, well-labeled domain dataset can **improve generalization** meaningfully.

---

## 📦 Datasets Used

| Dataset | Type | Langs | Hours | Notes |
|--------|------|-------|--------|-------|
| **Common Voice 11.0** | Converstional, Read-aloud, crowd-sourced | Swahili | ~250h | noisy, Mixed mic quality, many speakers |
| **FLEURS** | Benchmark-quality read speech | Swahili | ~50h | Clean studio-style speech |
| **Custom Dataset** | Conversational, noisy, real-world | Swahili | ~50h | Diverse, high-noise, manually labeled |

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

We trained three models using the `whisper large v2` architecture with identical settings for fair comparison.

### 1. 🧼 Clean-Only: `Common Voice + FLEURS + OpenSLR`
- Best benchmark accuracy
- Poor generalization to real-world test set
- **FLEURS WER**: 12.21%  
- **Domain WER**: 62.86%

### 2. 🧩 Domain-Only: `Custom dataset only`
- Better WER on domain test set  
- Improvements even on FLEURS, Improves with more custom data,  
- **FLEURS WER**: 34.73% *(improved from 40.00% baseline)*  
- **Domain WER**: 40.44%

**Conclusion**: *Our dataset alone taught the model something generalizable.* It has:
- Good acoustic diversity
- Solid label quality
- Enough variation to create useful generalization to clean data
- showcases generalization as similar understanding of both

### 3. 🔀 Combined: `Common Voice + FLEURS + OpenSLR + Custom dataset`
- Better overall WER
- Slight trade-off on FLEURS, but large gain on domain data 
- **FLEURS WER**: 13.21% *(improved from 40.00% baseline)*  
- **Domain WER**: 39.42%

**Conclusion**: Combined data improves real-world usability with minimal loss on benchmarks.

---

## 🔍 Analysis: Is Our Dataset Good?

We asked:

> Is our custom data *hurting* or *helping*?

Here’s the evidence that it is **helping**:

- **FLEURS improved from 40% → 34%** just using our data  
- On clean + custom model, FLEURS WER only increased slightly (12 → 13)  
- Domain WER dropped significantly when our data was added (62 → 39)
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

| Model | FLEURS WER | Domain Test WER |
|-------|------------|------------------|
| CV + FLEURS | 12.21%  | 62.86%  |
| Custom only | 34.73%  | 40.44%  |
| All combined | 13.21% | 39.42%  |

---

## 🤗 Try the Models on Hugging Face

| Model | Training Data | Description | Hugging Face |
|-------|---------------|-------------|---------------|
| `cv-fleurs-openslr` | CV + FLEURS + OpenSLR | Clean-only, benchmark-centric | [🔗 View](https://huggingface.co/RafatK/Swahili-Whisper_Large_v2-Decodis_Base) |
| `asr-domain-only` | Custom only | Robust real-world ASR | [🔗 View](https://huggingface.co/RafatK/Swahili-Whisper-Largev2-Decodis_FT) |
| `combined` | All datasets | General-purpose ASR | [🔗 View](https://huggingface.co/RafatK/Swahili-Whisper_Largev2-Decodis_Comb_FT) |

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

GitHub Issues: Submit an issue

Hugging Face Discussions: Join the conversation

Your feedback will help us refine our dataset and improve ASR for underrepresented languages like Swahili and Yoruba.

---

## 📂 Repository Structure
- We include the Evaluation python notebook
  
## Dependencies
- Transformers
- Pytorch
- datasets


---

## 📜 Citation

```bibtex
@misc{asr_swahili_yoruba_2025,
  title={Robust ASR for Swahili and Yoruba: A Multidataset Ablation Study},
  author={Kazi Rafat},
  year={2025},
  url={https://github.com/King-Rafat/Robust_Swahili_ASR},
}


