# REVISION SUMMARY - Metodologi Pengembangan
**Date**: October 25, 2025
**Student**: Jonathan Wiguna (18222019)
**Project**: Sistem Rangkuman Otomatis Berbasis AI untuk Komunitas Finansial Telegram

---

## ✅ REVISI YANG TELAH DISELESAIKAN

### 1. METODOLOGI PENGEMBANGAN (Bab I)

#### ❌ BEFORE (Salah):
- Menggunakan **Iterative Prototyping** (custom methodology)
- Terlalu detail di Bab I (52 baris dengan nested itemize)
- Tidak menggunakan established methodology
- Referensi: Preece et al. 2015 (interaction design book)

#### ✅ AFTER (Benar):
- Menggunakan **CRISP-DM** (Cross Industry Standard Process for Data Mining)
- Ringkas di Bab I (hanya sebutkan 6 fase)
- Menggunakan methodology yang established & widely-recognized
- Referensi: Chapman et al. 2000 (original CRISP-DM paper)
- Ada kalimat redirect: "Penjelasan detail... akan diuraikan lebih lanjut pada Bab III"

---

## 📊 CRISP-DM - 6 FASE STANDARD

### Format di Bab I (RINGKAS):

1. **Business Understanding**: Memahami kebutuhan komunitas dan definisi tujuan
2. **Data Understanding**: Mengumpulkan dan menganalisis data pesan Telegram
3. **Data Preparation**: Cleaning, transformasi, dan persiapan data untuk NLP
4. **Modeling**: Integrasi model NLP (sentiment, NER, topic, summarization)
5. **Evaluation**: Evaluasi kualitas rangkuman via metrik + user feedback
6. **Deployment**: Implementasi operasional dengan scheduling otomatis

### Mapping ke Sistem Kamu:

| Fase CRISP-DM | Implementasi di TCI Bot |
|---------------|-------------------------|
| Business Understanding | Identifikasi masalah information overload di komunitas MY |
| Data Understanding | Analisis 3 grup: MY Cuap Cuap, MY Swing Plan, MY Advanced Group |
| Data Preparation | Text cleaning, normalization, feature extraction |
| Modeling | - Sentiment: indonesian-roberta-base-emotion-classifier<br>- NER: bert-base-indonesian-NER + regex<br>- Topic: BERTopic<br>- Summary: Groq API (Llama 3.1 70B) |
| Evaluation | User feedback surveys + objective metrics (accuracy, compression ratio) |
| Deployment | FastAPI + Celery + PostgreSQL, hourly summary scheduling |

---

## 📝 FILES MODIFIED

### 1. `Bab I - Pendahuluan.tex`
**Changes**:
- ✅ Replaced Iterative Prototyping with CRISP-DM
- ✅ Simplified methodology section (from 52 lines to ~20 lines)
- ✅ Added CRISP-DM diagram reference (Gambar \ref{fig:crisp-dm})
- ✅ Added redirect statement to Bab III for details

**Location**: Lines 70-91

### 2. `daftar-pustaka.bib`
**Changes**:
- ✅ Added: `chapman2000` - CRISP-DM 1.0: Step-by-Step Data Mining Guide
- ✅ Removed: `preece2015` - Interaction Design book (not needed anymore)

### 3. `image/crisp-dm-diagram.png`
**Status**: ✅ Downloaded from https://thebigbookofdatascience.com/
**Location**: C:\Codingan\TugasAkhirLATEX\ProposalTA-NEW\image\crisp-dm-diagram.png

---

## 🎯 NEXT STEPS

### 1. Test Compile LaTeX
```bash
cd C:\Codingan\TugasAkhirLATEX\ProposalTA-NEW
pdflatex ProposalTA.tex
biber ProposalTA
pdflatex ProposalTA.tex
pdflatex ProposalTA.tex
```

**Expected Result**:
- ✅ No compilation errors
- ✅ Gambar CRISP-DM muncul di Bab I
- ✅ Citation [chapman2000] muncul di daftar pustaka

### 2. Persiapkan BAB III - Detail CRISP-DM

Di Bab III (Analisis & Perancangan Sistem), kamu perlu jelaskan DETAIL setiap fase:

#### Business Understanding
- Analisis kebutuhan komunitas Michael Yeoh
- Identifikasi stakeholders (admin, member VIP, member reguler)
- Success criteria: reduce time to digest info, improve decision quality

#### Data Understanding
- **Data Sources**: 3 Telegram groups
  - MY Cuap Cuap (22,000+ members) - Diskusi umum
  - MY Swing Plan - Trading signals
  - MY Advanced Group - Advanced analysis
- **Data Volume**: Estimasi ~X messages/hour across all groups
- **Data Characteristics**: 
  - Indonesian language with financial slang
  - Stock tickers format: $BBCA, $GOTO
  - Mix of formal and informal language

#### Data Preparation
- **Text Cleaning Pipeline**:
  1. Remove URLs, mentions, hashtags
  2. Normalize whitespace
  3. Handle emoji/emoticons
  4. Filter spam/bot messages
- **Feature Extraction**:
  - Timestamp normalization
  - Group ID mapping
  - User anonymization for privacy

#### Modeling
- **NLP Pipeline Architecture** (buat diagram):
  ```
  Telegram Message → Database → Celery Queue
       ↓
  Sentiment Analysis (RoBERTa)
       ↓
  Named Entity Recognition (BERT-NER)
       ↓
  Stock Ticker Extraction (Regex)
       ↓
  Topic Modeling (BERTopic) [hourly batch]
       ↓
  Summary Generation (Groq/Llama 3.1)
       ↓
  Post to Telegram Channel
  ```
- **Technology Stack**:
  - Backend: FastAPI
  - Database: PostgreSQL
  - Task Queue: Celery + Redis
  - NLP Models: HuggingFace Transformers
  - LLM API: Groq API

#### Evaluation
- **Objective Metrics**:
  - Sentiment classification accuracy
  - NER F1-score
  - Topic coherence score
  - Summary compression ratio
  - Processing latency
- **Subjective Metrics** (User Survey):
  - Usefulness (1-5 Likert scale)
  - Relevance of topics identified
  - Accuracy of sentiment
  - Format clarity
  - Time saved

#### Deployment
- **Infrastructure**:
  - Docker containers
  - CI/CD pipeline
  - Monitoring & logging
- **Operations**:
  - Hourly summary generation
  - Error handling & alerting
  - Data backup & retention policy
  - Privacy compliance (message deletion handling)

### 3. Create System Architecture Diagrams

Kamu perlu buat diagram untuk Bab III/IV:

1. **System Architecture Diagram**
   - High-level components (Telegram, FastAPI, Celery, DB, Groq)
   - Data flow arrows
   - External dependencies

2. **NLP Pipeline Diagram**
   - Detailed processing stages
   - Model specifications
   - Input/output at each stage

3. **CRISP-DM Adaptation Diagram** (Optional)
   - Show how each CRISP-DM phase maps to your implementation
   - Iterative cycles between phases

4. **Deployment Diagram**
   - Docker containers
   - Network topology
   - Data persistence

### 4. Review Program for Documentation

Document key files for Bab IV (Implementation):

**Key Files to Document**:
- `app/main.py` - FastAPI entry point
- `app/tasks/message_processor.py` - NLP pipeline
- `app/tasks/hourly_summary.py` - Summary generation
- `app/nlp/sentiment.py` - Sentiment analysis
- `app/nlp/entities.py` - NER
- `app/nlp/topics.py` - Topic modeling
- `app/ai/groq_client.py` - LLM integration

---

## 📚 REFERENCES ADDED

```bibtex
@manual{chapman2000,
  author       = {Pete Chapman and Julian Clinton and Randy Kerber and 
                  Thomas Khabaza and Thomas Reinartz and Colin Shearer and 
                  Rüdiger Wirth},
  title        = {CRISP-DM 1.0: Step-by-Step Data Mining Guide},
  organization = {CRISP-DM Consortium},
  year         = {2000},
  note         = {SPSS Inc.},
  url          = {https://www.kde.cs.uni-kassel.de/lehre/ws2012-13/kdd/files/CRISPWP-0800.pdf}
}
```

**Citation Usage**: `\autocite{chapman2000}`

---

## ✨ WHY CRISP-DM IS PERFECT FOR YOUR PROJECT

1. **Established Standard**: De facto methodology for data mining/ML since 1999
2. **Industry Recognition**: Used by IBM, SPSS, and major corporations
3. **Academic Acceptance**: Widely cited in research papers (1600+ citations)
4. **Perfect Fit for NLP**: Designed for data-driven projects like yours
5. **Iterative Nature**: Supports user feedback cycles (as requested by pembimbing)
6. **Comprehensive**: Covers entire lifecycle from business understanding to deployment
7. **Flexible**: Can be adapted to specific domains (financial + Telegram + Indonesian NLP)

---

## 🔍 COMPARISON: OLD vs NEW

| Aspect | ❌ Iterative Prototyping | ✅ CRISP-DM |
|--------|-------------------------|------------|
| **Recognition** | Custom, not established | Industry standard since 1999 |
| **Citation** | Generic design book | Specific ML/DM methodology |
| **Bab I Length** | Too detailed (52 lines) | Concise (20 lines) |
| **Detail Location** | Premature in Bab I | Deferred to Bab III (correct) |
| **Fit for ML/NLP** | General prototyping | Specifically for data mining/ML |
| **Academic Acceptance** | ⚠️ Needs justification | ✅ Widely accepted |
| **Pembimbing Approval** | ❓ Questionable | ✅ High confidence |

---

## 📋 CHECKLIST

- [x] Replace methodology from Iterative Prototyping to CRISP-DM
- [x] Add chapman2000 reference to bibliography
- [x] Remove preece2015 reference (not needed)
- [x] Download CRISP-DM diagram
- [x] Add diagram to Bab I with proper caption
- [x] Simplify Bab I methodology section
- [x] Add redirect to Bab III for details
- [ ] Test compile LaTeX (pdflatex + biber)
- [ ] Verify diagram appears correctly
- [ ] Verify citation appears in bibliography
- [ ] Prepare Bab III detailed CRISP-DM explanation
- [ ] Create system architecture diagrams
- [ ] Document code for Bab IV

---

## 💡 TIPS FOR BAB III

When writing detailed CRISP-DM explanation in Bab III:

1. **Use subsections for each phase**:
   ```latex
   \section{Metodologi Pengembangan}
   \subsection{Business Understanding}
   \subsection{Data Understanding}
   ...
   ```

2. **Include deliverables for each phase**:
   - Business Understanding → Business requirements document
   - Data Understanding → Data quality report
   - Data Preparation → Cleaned dataset
   - Modeling → Trained models + evaluation metrics
   - Evaluation → Validation report
   - Deployment → Production system

3. **Show iterative nature**:
   - Explain how findings in Evaluation phase led to improvements in Modeling
   - Document feedback loops
   - Show at least 2 complete cycles

4. **Map to actual implementation**:
   - Link each phase to specific code files
   - Show concrete examples from your system
   - Include screenshots of outputs

---

## 🎓 ACADEMIC QUALITY

This revision brings your TA to proper academic standards:

✅ Uses established, peer-reviewed methodology
✅ Proper citation of original source
✅ Correct structure (overview in Bab I, details in Bab III)
✅ Industry-standard approach for ML/NLP projects
✅ Aligns with STI program focus (practical engineering, not pure theory)
✅ Supports iterative improvement (as requested by pembimbing)

---

**Status**: ✅ REVISION COMPLETE
**Ready for**: Pembimbing review → Compile test → Bab III development

Good luck with your TA, Jonathan! 🚀
