# 🧠 A Robust ASR Study for Swahili
## 🔍 Exploring Benchmark Gaps and Real-World Speech Generalization

Welcome to our open-source repository exploring **automatic speech recognition (ASR)** in **Swahili**, where we investigate how open benchmark datasets compare to **real-world, noisy, conversational speech**. 

**GitHub Repository by** [DECODIS](https://www.decodis.com/)

We present a complete ablation study using:

- 🌐 Open-source datasets (Common Voice + FLEURS)
- 🗣️ A hand-collected, high-variance real-world dataset
- 🧪 Three ASR models: Clean-only, Domain-only, Combined

---

## 🚀 Why This Matters

Low-resource African languages like Swahili and Yoruba are often evaluated on clean, controlled datasets. But real-world usage involves:

- Noisy environments (phones, streets, homes)
- Spontaneous, conversational phrasing
- Speaker and device diversity
- Non-standard syntax and informal speech

🔎 We show that **benchmark performance is not a reliable proxy for real-world ASR quality** — and that even a small, well-labeled domain dataset can **improve generalization** meaningfully.

---

## 📦 Datasets Used

| Dataset | Type | Langs | Hours | Notes |
|--------|------|-------|--------|-------|
| **Common Voice 13.0** | Read-aloud, crowd-sourced | Swahili, Yoruba | ~250h | Mixed mic quality, many speakers |
| **FLEURS** | Benchmark-quality read speech | Swahili, Yoruba | ~50h | Clean studio-style speech |
| **Custom Dataset** | Conversational, noisy, real-world | Swahili, Yoruba | ~50h | Diverse, high-noise, manually labeled |

### 🧠 Custom Dataset Highlights

- 🎙️ **Audio type**: Mobile, WhatsApp, interviews, community voice recordings  
- 🗣️ **Speech styles**: Conversational, informal, overlapping, hesitations  
- 🌍 **Geographic & dialect diversity**: Multiple regional accents  
- 🔊 **Noise**: Indoor, outdoor, street, wind, device hum  
- ✅ **Transcript quality**: 90%+ alignment verified by native speakers  
- 🎯 **Use cases**: Real-life human-computer interaction, subtitle generation, local voice assistants

This dataset is **small but high-quality**, with audio/text that *actually reflects how people speak* — unlike read-aloud corpora.

---

## 🧪 Model Variants Trained

We trained three models using the `wav2vec2` architecture with identical settings for fair comparison.

### 1. 🧼 Clean-Only: `Common Voice + FLEURS`
- ✅ Best benchmark accuracy
- ❌ Poor generalization to real-world test set
- **FLEURS WER**: 12.21%  
- **Domain WER**: 69.00%

### 2. 🧩 Domain-Only: `Custom dataset only`
- ✅ Better WER on domain test set  
- ✅ Surprisingly strong results even on FLEURS  
- **FLEURS WER**: 34.00% *(improved from 40.00% baseline)*  
- **Domain WER**: 42.00%

🧠 **Conclusion**: *Our dataset alone taught the model something generalizable.* It has:
- Good acoustic diversity
- Solid label quality
- Enough variation to create useful generalization to clean data

### 3. 🔀 Combined: `CV + FLEURS + Custom`
- ✅ Best generalization across both domains  
- ✅ Slight trade-off on FLEURS, but large gain on domain data  
- **FLEURS WER**: 13.00%  
- **Domain WER**: 31.00%

🧠 **Conclusion**: Combined data improves real-world usability with minimal loss on benchmarks.

---

## 🔍 Analysis: Is Our Dataset Good?

We asked:

> Is our custom data *hurting* or *helping*?

Here’s the evidence that it is **helping**:

- **FLEURS improved from 40% → 34%** just using our data  
- On clean + custom model, FLEURS WER only increased slightly (12 → 13)  
- Domain WER dropped significantly when our data was added (69 → 31)
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
| CV + FLEURS | 12.21% ✅ | 69.00% ❌ |
| Custom only | 34.00% ✅ | 42.00% ✅ |
| All combined | 13.00% ✅ | 31.00% ✅ |

---

## 🤗 Try the Models on Hugging Face

| Model | Training Data | Description | Hugging Face |
|-------|---------------|-------------|---------------|
| `asr-cv-fleurs` | CV + FLEURS | Clean-only, benchmark-centric | [🔗 View](https://huggingface.co/your-org/asr-cv-fleurs) |
| `asr-domain-only` | Custom only | Robust real-world ASR | [🔗 View](https://huggingface.co/your-org/asr-domain-only) |
| `asr-combined` | All datasets | General-purpose ASR | [🔗 View](https://huggingface.co/your-org/asr-combined) |

---

## 🧪 Community Evaluation & Feedback

We’re asking the community to **try these models** and help confirm the core insight:

> 📌 **Benchmark WER is not enough. Real-world data is essential.**

Try your own audio, evaluate model predictions, and tell us:

- Does our custom-trained model work better on your speech?
- Are there accent mismatches or coverage gaps?
- Does benchmark-trained ASR work well in your environment?

💬 Share your insights:

- [GitHub Issues](https://github.com/your-org/your-repo/issues)
- [Model Discussions on Hugging Face](https://huggingface.co/your-org)

---

## 📂 Repository Structure

