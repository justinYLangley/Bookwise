# Bookwise 📖✨

An intelligent macOS & iPadOS reading companion that transforms technical books, study guides, and PDF documents into an interactive, multi-modal learning experience. Bookwise extracts current page text, synthesizes high-impact insights via Apple Intelligence (with smart local heuristic NLP fallback), and reads lessons aloud with synchronized real-time word highlighting.

> This repository currently includes project information and a starter page. Source code is not included yet.

## ✨ Features

### 🧠 Multi-Mode Insight Engine

- **Tutor Lesson:** Pedagogical breakdown for complex concepts, mental models, architectural rationale, and step-by-step technical explanations.
- **Key Summary:** High-density executive overview for quick retention.
- **Deep Dive:** In-depth analysis of technical patterns and underlying mechanisms.
- **Takeaways:** Actionable points, best practices, and core mechanics with noise and header filtering.

### 💬 Interactive Document Chat

- Ask natural language questions about the current page or entire document.
- Hybrid RAG combining PDFKit search and Apple NaturalLanguage embeddings.
- Toggle context scope between **Current Page** and **Whole Document**.
- Grounded on-device responses via Apple Intelligence FoundationModels.

### 🎨 Customizable AI Prompts (Per-Document or Global)

- Edit system instructions and user prompt templates for each insight mode and chat.
- Save prompt customizations for one document or all documents.
- Live prompt status badges (🟣 document override / 🔵 global custom / gray default).
- Restore defaults per mode or in bulk.

### 🎙️ Synchronized Real-Time Narration

- System speech synthesis for lessons and summaries.
- Real-time word highlighting synchronized to narration.
- Auto-next playback for continuous page-by-page narration.

### 👁️ On-Device Vision Intelligence (Charts & Diagram OCR)

- High-DPI rendering + Apple Vision OCR for diagrams, charts, and image-heavy pages.
- Extracts text missed by standard PDF text streams.
- Supports scanned and image-only PDFs.
- Injects visual context into AI tutor explanations and takeaways.

### 📖 Clean & Flexible Reader Interface

- Direct page jump and navigation shortcuts.
- Smooth resizable split between document and insights panel.
- Adjustable typography controls with persisted preferences.
- Sidebar toggle and quick copy for generated notes.

### 📚 Recent Books Library

- Shows 12 most recently opened books with metadata.
- One-click reopen from local copy.
- Remove individual entries or clear all history.

### ⚡ Apple Intelligence & Local Fallback

- Uses Apple Foundation Models on supported Apple Silicon devices.
- Includes local heuristic NLP fallback for reliable offline summaries.

## 📥 Download

Pre-built binaries are available on the Releases page.

1. Download **Bookwise-macOS.zip** from the latest release.
2. Unzip and drag **Bookwise.app** to `/Applications`.
3. Launch Bookwise and open any PDF or text document.

## 🛠️ Building from Source

### Requirements

- macOS 14.0 (Sonoma) or later
- Xcode 26 Beta (Apple Intelligence / FoundationModels support)
- Swift 6+

### Build Steps

```bash
# Clone the repository
git clone https://github.com/ampclaw/Bookwise.git
cd Bookwise

# Open in Xcode
open Bookwise.xcodeproj

# Or build from terminal
xcodebuild -scheme Bookwise -configuration Release -destination 'platform=macOS' build
```

## 📜 Architecture Overview

- `Views/ReaderView.swift`: Reading pane, document rendering, page controls, and resizable split layout.
- `Views/SummarySidebarView.swift`: Insight modes, typography controls, playback controls, and prompt status.
- `Views/DocumentChatView.swift`: Hybrid RAG chat with scope selector and prompt indicators.
- `Views/PromptEditorView.swift`: Prompt editor with document/global scope saving and restore tools.
- `Services/InsightService.swift`: Apple Intelligence orchestration + local NLP fallback and caching.
- `Services/PromptStore.swift`: Prompt persistence for global and document overrides.
- `Services/AppleIntelligenceSummarizer.swift`: Context window management and safe retry pipeline.
- `Services/DocumentChatService.swift`: Retrieval and grounded on-device generation pipeline.
- `Services/SpeechService.swift`: Speech synthesis wrapper with character-range sync updates.
- `Services/LocalInsightGenerator.swift`: Local sentence ranking and noise filtering for takeaways.