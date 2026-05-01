# Music Performance Evaluation Pipeline

## Overview
This Jupyter Notebook contains a Music Information Retrieval (MIR) pipeline designed to evaluate a student's MIDI piano performance against a ground-truth sheet music file (MusicXML or PDF). 

It uses structural alignment (FastDTW) and combinatorial graph matching to assess pitch accuracy, rhythmic timing, articulation, and dynamics. Finally, it passes the mathematical metrics into a Generative AI model (Google Gemini) to produce conversational, pedagogical feedback as an "AI Teacher."

## Key Features
* **Optional OMR:** Converts sheet music PDFs to MusicXML using Audiveris (can be bypassed if you already have the XML).
* **Music21 Parsing:** Extracts notes, chords, dynamics, and slurs onto a rigid mathematical grid.
* **Algorithmic Evaluation:** Uses FastDTW for macro-alignment and median Inter-Onset Intervals (IOI) for tempo normalization.
* **Diagnostic Reporting:** Outputs a highly structured JSON report detailing specific bar-by-bar mistakes (rushing, dragging, missed accents, wrong pitches, etc.).
* **Generative AI Feedback:** Translates raw data into a warm, constructive "Feedback Sandwich" for the student.

## Setup & Prerequisites
This pipeline is designed to run in a Jupyter/Google Colab environment. 

The environment setup block (Cell 2) automatically installs the necessary Python libraries, including:
* `music21`
* `fastdtw`
* `scipy`
* `google-generativeai`
* `pandas`, `numpy`, `plotly`, `matplotlib`

*Note: Headless MuseScore 3 is used for visual rendering, and Audiveris/Java/Tesseract are installed if OMR is enabled.*

## How to Use

**1. Upload Your Files**
Upload your reference sheet music (`.mxl` or `.pdf`) and the student's performance (`.mid`) into your working directory.

**2. Configure the Pipeline (Cell 1)**
In the first cell under **Global Configurations**, update the file paths to point to your uploaded files:
```python
PDF_PATH              = '/path/to/your/sheet_music.pdf'
MIDI_PATH             = '/path/to/your/performance.mid'
GROUND_TRUTH_XML_PATH = '/path/to/your/ground_truth.mxl'
