# DIAGRAM RECOMMENDATIONS FOR BAB 2
**Date:** 2025-10-28  
**Current Diagrams:** 1 (bert-architecture-diagram.png)  
**Recommended Additional Diagrams:** 4  
**Priority:** FUTURE ENHANCEMENT (Not Critical)

---

## 📊 CURRENT DIAGRAM STATUS

### ✅ Already Referenced (Exists):
1. **bert-architecture-diagram.png** (Line 71)
   - Section: II.2.1 (Fondasi: Arsitektur Transformer dan BERT)
   - Purpose: Illustrate BERT architecture with bidirectional self-attention
   - Status: ✅ Properly referenced

---

## 🎨 RECOMMENDED ADDITIONAL DIAGRAMS

### 1️⃣ NLP Pipeline Overview Diagram
**Filename:** `nlp-pipeline-overview.png`  
**Suggested Location:** End of Section II.2 or Section II.9  
**Estimated Creation Time:** 30-45 minutes  
**Complexity:** Medium

#### Purpose:
Show the complete NLP pipeline flow from raw Telegram messages to final summary.

#### Suggested Content:
```
┌─────────────────────────────────────────────────────────────┐
│                    TELEGRAM MESSAGES                         │
│              (Cuap Cuap / Swing Plan / Advanced)            │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
        ┌────────────────────────────┐
        │   Named Entity Recognition │
        │   (bert-base-indonesian-NER)│
        │   ➜ Extract: Stocks, People │
        └────────────┬───────────────┘
                     │
                     ▼
        ┌────────────────────────────┐
        │    Sentiment Analysis      │
        │ (indonesian-roberta-base-  │
        │  emotion-classifier)       │
        │ ➜ Detect: Fear, Joy, etc.  │
        └────────────┬───────────────┘
                     │
                     ▼
        ┌────────────────────────────┐
        │     Topic Modeling         │
        │        (BERTopic)          │
        │ ➜ Cluster: Discussion Topics│
        └────────────┬───────────────┘
                     │
                     ▼
        ┌────────────────────────────┐
        │   LLM Summarization        │
        │    (Llama 3.1 70B via Groq)│
        │ ➜ Generate: Coherent Summary│
        └────────────┬───────────────┘
                     │
                     ▼
        ┌────────────────────────────┐
        │     FINAL SUMMARY          │
        │  (Delivered via Bot)       │
        └────────────────────────────┘
```

#### LaTeX Integration:
```latex
\begin{figure}[H]
  \centering
  \includegraphics[width=0.75\textwidth]{image/nlp-pipeline-overview.png}
  \caption{Arsitektur \textit{pipeline} NLP untuk sistem rangkuman otomatis, menunjukkan 
           aliran pemrosesan dari pesan Telegram mentah hingga rangkuman akhir melalui 
           empat komponen utama: NER, analisis sentimen, \textit{topic modeling}, dan 
           generasi rangkuman dengan LLM}
  \label{fig:nlp-pipeline}
\end{figure}
```

#### Benefits:
- ✅ Helps readers understand system architecture at a glance
- ✅ Shows integration of multiple NLP components
- ✅ Illustrates sequential processing flow
- ✅ Connects theory (Bab 2) with implementation (Bab 3/4)

---

### 2️⃣ Telegram Community Hierarchy Diagram
**Filename:** `telegram-hierarchy.png`  
**Suggested Location:** Section II.6 (Telegram sebagai Platform Komunitas)  
**Estimated Creation Time:** 20-30 minutes  
**Complexity:** Simple

#### Purpose:
Visualize the hierarchical structure of the three Telegram groups and information flow.

#### Suggested Content:
```
┌─────────────────────────────────────────────────────────────────┐
│                    MICHAEL YEOH'S ECOSYSTEM                      │
│                      (22,000+ members total)                     │
└───────────────────────────┬─────────────────────────────────────┘
                            │
           ┌────────────────┼────────────────┐
           │                │                │
           ▼                ▼                ▼
    ┌──────────┐    ┌──────────┐    ┌──────────┐
    │ Cuap Cuap│    │Swing Plan│    │ Advanced │
    │  (Basic) │    │ (Inter.) │    │ (Expert) │
    ├──────────┤    ├──────────┤    ├──────────┤
    │• Public  │    │• Members │    │• VIP     │
    │• High    │    │• Medium  │    │• Low     │
    │  Volume  │    │  Volume  │    │  Volume  │
    │• Informal│    │• Focused │    │• Deep    │
    │          │    │          │    │  Analysis│
    └──────────┘    └──────────┘    └──────────┘
         │               │                │
         └───────────────┼────────────────┘
                         │
                         ▼
              ┌──────────────────┐
              │  UNIFIED SUMMARY │
              │  (Cross-Group    │
              │   Synthesis)     │
              └──────────────────┘
```

#### LaTeX Integration:
```latex
\begin{figure}[H]
  \centering
  \includegraphics[width=0.8\textwidth]{image/telegram-hierarchy.png}
  \caption{Struktur hierarkis komunitas finansial Telegram Michael Yeoh, menunjukkan 
           tiga tingkat grup dengan karakteristik berbeda yang disintesis oleh sistem 
           rangkuman otomatis}
  \label{fig:telegram-hierarchy}
\end{figure}
```

#### Benefits:
- ✅ Clarifies the three-tier group structure
- ✅ Shows information flow from multiple sources
- ✅ Illustrates the challenge of cross-group synthesis
- ✅ Provides context for weighted sentiment feature

---

### 3️⃣ Real-Time Architecture Diagram
**Filename:** `realtime-architecture.png`  
**Suggested Location:** Section II.7 (Arsitektur Pemrosesan Data Real-Time)  
**Estimated Creation Time:** 45-60 minutes  
**Complexity:** High

#### Purpose:
Illustrate the event-driven architecture and data flow in the system.

#### Suggested Content:
```
┌────────────────────────────────────────────────────────────────┐
│                      TELEGRAM PLATFORM                          │
└────────────────────────┬───────────────────────────────────────┘
                         │
                         │ (Webhook / Polling)
                         ▼
              ┌──────────────────────┐
              │   MESSAGE COLLECTOR   │
              │   (Telegram Bot API)  │
              └──────────┬────────────┘
                         │
                         │ (Event Stream)
                         ▼
              ┌──────────────────────┐
              │   MESSAGE QUEUE       │
              │   (Buffer/Kafka)      │
              └──────────┬────────────┘
                         │
         ┌───────────────┼───────────────┐
         │               │               │
         ▼               ▼               ▼
    ┌────────┐    ┌─────────┐    ┌─────────┐
    │  NER   │    │Sentiment│    │  Topic  │
    │ Module │    │ Analysis│    │Modeling │
    └────┬───┘    └────┬────┘    └────┬────┘
         │             │              │
         └─────────────┼──────────────┘
                       │
                       ▼
           ┌───────────────────────┐
           │ AGGREGATION & SYNTHESIS│
           │    (Hourly Batches)   │
           └───────────┬───────────┘
                       │
                       ▼
           ┌───────────────────────┐
           │   LLM SUMMARIZATION   │
           │   (Groq API - LPU)    │
           └───────────┬───────────┘
                       │
                       ▼
           ┌───────────────────────┐
           │   SUMMARY DELIVERY    │
           │  (Telegram Bot Send)  │
           └───────────────────────┘

[Legend]
→ : Synchronous Flow
⇢ : Asynchronous Event
□ : Processing Component
◇ : External Service
```

#### LaTeX Integration:
```latex
\begin{figure}[H]
  \centering
  \includegraphics[width=0.9\textwidth]{image/realtime-architecture.png}
  \caption{Arsitektur pemrosesan data \textit{event-driven} untuk sistem rangkuman 
           otomatis, menunjukkan aliran data dari pengumpulan pesan hingga pengiriman 
           rangkuman dengan pemrosesan paralel komponen NLP}
  \label{fig:realtime-architecture}
\end{figure}
```

#### Benefits:
- ✅ Shows event-driven architecture principles
- ✅ Illustrates parallel processing of NLP components
- ✅ Demonstrates scalability design
- ✅ Clarifies role of message queuing and batching

---

### 4️⃣ Extractive vs Abstractive Summarization Comparison
**Type:** Table (not diagram, but visual comparison)  
**Suggested Location:** Section II.2.2 (Peringkasan Berbasis Transformer)  
**Estimated Creation Time:** 15 minutes  
**Complexity:** Simple

#### Purpose:
Provide clear comparison of two main summarization approaches.

#### Suggested Content:

```latex
\begin{table}[H]
\centering
\caption{Perbandingan pendekatan peringkasan ekstraktif dan abstraktif}
\label{tab:extractive-vs-abstractive}
\begin{tabular}{|l|p{5cm}|p{5cm}|}
\hline
\textbf{Aspek} & \textbf{Ekstraktif} & \textbf{Abstraktif} \\
\hline
\textbf{Metode} & Memilih kalimat penting dari teks asli & Menghasilkan kalimat baru dengan parafrase \\
\hline
\textbf{Kecepatan} & Cepat (hanya seleksi) & Lambat (memerlukan generasi) \\
\hline
\textbf{Koherensi} & Dapat terputus-putus & Lebih koheren dan naratif \\
\hline
\textbf{Informativeness} & Tinggi (konten asli) & Bervariasi (dapat hilang detail) \\
\hline
\textbf{Fleksibilitas} & Terbatas pada teks asli & Bebas, dapat merangkum ulang \\
\hline
\textbf{Contoh} & BERTSum, TextRank & GPT-4, Llama, BART \\
\hline
\textbf{Aplikasi di Sistem} & BERTopic (ekstraksi topik) & Llama 3.1 70B (generasi rangkuman) \\
\hline
\end{tabular}
\end{table}
```

#### Benefits:
- ✅ Clear side-by-side comparison
- ✅ Helps readers understand trade-offs
- ✅ Justifies hybrid approach in your system
- ✅ Quick reference for reviewers

---

## 📈 PRIORITY RANKING

| Rank | Diagram | Impact | Effort | Priority Score |
|------|---------|--------|--------|----------------|
| 1 | NLP Pipeline Overview | High | Medium | **9/10** |
| 2 | Telegram Hierarchy | Medium | Low | **8/10** |
| 3 | Extractive vs Abstractive Table | Medium | Very Low | **7/10** |
| 4 | Real-Time Architecture | High | High | **6/10** |

**Recommendation:** Create diagrams in this order if time is limited.

---

## 🛠️ CREATION TOOLS

### Recommended Tools:

1. **draw.io (diagrams.net)** - FREE
   - Best for: All technical diagrams
   - Export: PNG, PDF, SVG
   - URL: https://app.diagrams.net/

2. **Microsoft Visio** (if available)
   - Best for: Professional architecture diagrams
   - Export: PNG, PDF

3. **PowerPoint/Google Slides**
   - Best for: Simple hierarchy diagrams
   - Export: PNG, PDF

4. **Lucidchart** (Free with limits)
   - Best for: Clean, professional diagrams
   - URL: https://www.lucidchart.com/

5. **TikZ (LaTeX native)** - For advanced users
   - Best for: Publication-quality diagrams
   - Integrated directly in LaTeX

### Export Settings:
- **Resolution:** 300 DPI minimum
- **Format:** PNG (for bitmap) or PDF (for vector)
- **Background:** Transparent or white
- **Size:** Width ~1200px for full-page diagrams

---

## 📋 IMPLEMENTATION CHECKLIST

### For Each Diagram:

- [ ] Create diagram using chosen tool
- [ ] Export as PNG/PDF at 300+ DPI
- [ ] Save to `image/` folder with descriptive filename
- [ ] Add `\includegraphics` command in .tex file
- [ ] Write descriptive caption with `\caption{}`
- [ ] Add label with `\label{fig:diagram-name}`
- [ ] Compile LaTeX to verify rendering
- [ ] Check that diagram is referenced in text
- [ ] Verify diagram adds value (not just decoration)

---

## 🎯 EXPECTED OUTCOMES

### With All 4 Diagrams Added:

**Before (Current):**
- 1 diagram total
- Limited visual aids
- Text-heavy presentation

**After (With Additions):**
- 5 visual elements total
- Better reader engagement
- Clearer system understanding
- More professional appearance

**Impact on Thesis Quality:**
- Current: 9.2/10
- With diagrams: 9.5-9.7/10
- Enhanced visual communication
- Easier for examiners to grasp complex concepts

---

## ⏰ TIME ESTIMATION

| Diagram | Time | Cumulative |
|---------|------|------------|
| Extractive vs Abstractive Table | 15 min | 15 min |
| Telegram Hierarchy | 30 min | 45 min |
| NLP Pipeline Overview | 45 min | 1h 30min |
| Real-Time Architecture | 60 min | 2h 30min |
| **TOTAL** | **2.5 hours** | - |

**Recommended Schedule:**
- Week 1: Create table + hierarchy (45 min)
- Week 2: Create NLP pipeline (45 min)
- Week 3: Create architecture diagram (60 min)
- OR: Dedicate one afternoon (2.5 hours) to create all at once

---

## 🚀 NEXT STEPS

### Option A: Create Diagrams Yourself
1. Choose tool (recommend draw.io)
2. Follow content suggestions above
3. Export and integrate into LaTeX
4. Compile and verify

### Option B: Request Assistance
If you want, I can:
- ✅ Create ASCII/text versions of diagrams
- ✅ Provide more detailed specifications
- ✅ Generate TikZ code for LaTeX-native diagrams
- ✅ Help troubleshoot LaTeX integration issues

Just say: **"Help me create [diagram name]"**

---

**Status:** RECOMMENDATIONS COMPLETE  
**Priority:** FUTURE ENHANCEMENT (not blocking)  
**Estimated ROI:** High (significant visual improvement for moderate effort)
