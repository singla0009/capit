# Supported NeMo STT Models for Conversion to GGUF

This document contains a curated list of Automatic Speech Recognition (ASR) models hosted on Hugging Face that are compatible with the local C++ engine (`parakeet-cli` / `parakeet.cpp`). 

To use any of these models in the app, you must:
1. Download the `.nemo` file from the respective Hugging Face repository.
2. Run the NeMo python conversion script to extract the **CTC Head** and convert it into a `.gguf` file.

> **Why these models?**  
> The local C++ engine natively supports **CTC (Connectionist Temporal Classification)** decoding. It does *not* support Seq2Seq (Canary), TDT, or pure RNNT models. The models listed here are either **pure Conformer-CTC** models or **FastConformer-Hybrid (Transducer + CTC)** models. In hybrid models, the conversion script easily discards the incompatible Transducer head and preserves the compatible CTC head.

---

## 1. Official NVIDIA Models (European & Global)

NVIDIA maintains a rich library of FastConformer and Conformer models. The `_pc` suffix means the model automatically predicts punctuation and capitalization.

### Western European
*   **English:** 
    *   `nvidia/stt_en_fastconformer_hybrid_large_pc` (115M params, Punctuation/Capitalization)
    *   `nvidia/stt_en_conformer_ctc_large` (120M params, Pure CTC)
*   **French:** 
    *   `nvidia/stt_fr_fastconformer_hybrid_large_pc` (115M params)
    *   `nvidia/stt_fr_conformer_ctc_large` (120M params, trained on 1500+ hours)
*   **German:** 
    *   `nvidia/stt_de_fastconformer_hybrid_large_pc` (115M params)
    *   `nvidia/stt_de_conformer_ctc_large` (120M params)
*   **Spanish:** 
    *   `nvidia/stt_es_fastconformer_hybrid_large_pc`
*   **Italian:** 
    *   `nvidia/stt_it_fastconformer_hybrid_large_pc`
*   **Portuguese:** 
    *   `nvidia/stt_pt_fastconformer_hybrid_large_pc`
*   **Dutch:** 
    *   `nvidia/stt_nl_fastconformer_hybrid_large_pc` (115M params)
*   **Polish:** 
    *   `nvidia/stt_pl_fastconformer_hybrid_large_pc` (115M params)

### Eurasian & Middle Eastern
*   **Russian & Kazakh:** 
    *   `nvidia/stt_kk_ru_fastconformer_hybrid_large` (Bilingual model)
*   **Arabic:** 
    *   `nvidia/stt_ar_fastconformer_hybrid_large_pcd_v1.0` (Includes Diacritics)
*   **Persian:** 
    *   `nvidia/stt_fa_fastconformer_hybrid_large`
*   **Georgian:** 
    *   `nvidia/stt_ka_fastconformer_hybrid_large_pc`

---

## 2. Official AI4Bharat Models (Indic Languages)

AI4Bharat built the "MahaDhwani" and "IndicConformer" projects. All their models use the **Hybrid (CTC + RNNT)** architecture, making them perfectly compatible with our conversion script.

### The Master Multilingual Model
*   **22 Languages (All-in-one):** 
    *   `ai4bharat/indic-conformer-600m-multilingual` (600M parameters. Supports Assamese, Bengali, Bodo, Dogri, Gujarati, Hindi, Kannada, Kashmiri, Konkani, Maithili, Malayalam, Manipuri, Marathi, Nepali, Odia, Punjabi, Sanskrit, Santali, Sindhi, Tamil, Telugu, and Urdu).

### Individual Language Models (Smaller & Faster)
These individual models are around 120M parameters and are much faster for specific single-language workflows.
*   **Hindi:** `ai4bharat/indicconformer_stt_hi_hybrid_ctc_rnnt_large`
*   **Punjabi:** `ai4bharat/indicconformer_stt_pa_hybrid_ctc_rnnt_large`
*   **Tamil:** `ai4bharat/indicconformer_stt_ta_hybrid_ctc_rnnt_large`
*   **Gujarati:** `ai4bharat/indicconformer_stt_gu_hybrid_ctc_rnnt_large`
*   **Kannada:** `ai4bharat/indicconformer_stt_kn_hybrid_ctc_rnnt_large`
*   **Kashmiri:** `ai4bharat/indicconformer_stt_ks_hybrid_ctc_rnnt_large`
*   **Urdu:** `ai4bharat/indicconformer_stt_ur_hybrid_ctc_rnnt_large`
*(AI4Bharat hosts similar repositories for the rest of the 22 Indic languages under the same naming convention).*

---

## 3. Community & Independent Organizations

Because the NVIDIA NeMo toolkit is open-source, researchers around the world train custom `.nemo` models. Below are examples of verified community NeMo models that use the FastConformer architecture.

*   **French (by Bofeng Huang):** 
    *   `bofenghuang/stt_fr_fastconformer_hybrid_large`
    *   *Description:* Trained by an independent AI researcher on over 2500 hours of open-source French data. Highly optimized for predicting hyphens and apostrophes natively.
*   **French (by LINAGORA):** 
    *   `linagora/linto_stt_fr_fastconformer`
    *   *Description:* An open-source model trained by a French open-source software company, specialized for various French dialects and audio sources.

---

### How to Find More Community Models
You can discover hundreds more by navigating to Hugging Face and searching:
1. Under **Tasks**, select `Automatic Speech Recognition`.
2. Under **Libraries**, select `NeMo`.
3. Type `"conformer ctc"` or `"fastconformer"` in the search bar. 

**Important:** Ignore models from frameworks like `icefall` or `sherpa-onnx`. Ensure the repository provides a `.nemo` file so the Python conversion script can successfully parse it into `.gguf`.

---

## 4. Additional Independent Developers & Orgs
Here are some specialized Conformer-CTC models built by the wider community:

*   **Kinyarwanda (by mbazaNLP):** 
    *   `mbazaNLP/Kinyarwanda_nemo_stt_conformer_model`
    *   *Description:* An ASR model specifically tuned for Kinyarwanda, built by an African NLP research group.
*   **Persian (by Ali Farokh):** 
    *   `alifarokh/nemo-conformer-medium-fa`
    *   *Description:* An independently trained, lightweight medium Conformer model for Persian.
*   **Vietnamese (by Quan Hoang Ngoc):**
    *   `QuanHoangNgoc/conformer-nemo`
    *   *Description:* A Conformer-based STT model optimized for Vietnamese.
*   **Medical Dictation (by Various Orgs):**
    *   *Search HuggingFace for tags like `nemo medical` or `nemo-stt-medical` to find models fine-tuned specifically on medical terminology and physician dictations.*
