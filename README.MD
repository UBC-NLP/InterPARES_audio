<center>
<img src="https://dlnlp.ai/img/InterPARES_Audio.jpg" alt="InterPARES_Audio.jpg" width="35%" height="25%"/>
</center>

**InterPARES-Audio** is an automated, end-to-end pipeline that transforms complex, lengthy audio files into structured, insightful text

## Workflow

<img src="IntePARES_Audio_workflow.png" alt="InterPARES_Audio.jpg"/>

## Code
[Jupyter Notebook ](https://github.com/UBC-NLP/InterPARES_audio/blob/main/multilingual_audio_analysis.ipynb)

## Examples
 [Meeting report, Markdown](https://github.com/UBC-NLP/InterPARES_audio/blob/main/meeting_reports/A05195/meeting_analysis_A05195-20251010_174134-English.md)

 [Meeting report, PDF](https://github.com/UBC-NLP/InterPARES_audio/blob/main/meeting_reports/A05195/meeting_analysis_A05195-20251010_174134-English.pdf)



# InterPARES-Audio: Multilingual Audio Analysis

**InterPARES-Audio** is a sophisticated system designed to listen, transcribe, translate, and analyze complex audio recordings. It is built to handle files with multiple speakers conversing in different languages, making it the ideal tool for processing archives of meetings, interviews, and panel discussions.

## Demo & Examples

-   **Live Demo:** [**demos.dlnlp.ai/InterPARES/**](https://demos.dlnlp.ai/InterPARES/ "null")
    
-   **Jupyter Notebook:** [**multilingual_audio_analysis.ipynb**](https://github.com/UBC-NLP/InterPARES_audio/blob/main/multilingual_audio_analysis.ipynb "null")
    
-   **GitHub Repo:** [**UBC-NLP/InterPARES_audio**](https://github.com/UBC-NLP/InterPARES_audio "null")
    

## The Problem & Motivation

This project addresses the challenges found in large-scale digitized collections, such as the **UNESCO Audio Archives**. This historic collection contains:

-   Over 17,000 digitized recordings from 1954 to 1979.
    
-   Highly diverse content, including meetings, radio programs, and interviews.
    
-   Significant obstacles to accessibility and analysis:
    
    -   **Highly Multilingual:** Over 70 languages are present.
        
    -   **Limited Metadata:** Only ~37% of the recordings have any associated metadata.
        

An initial study (RA03A) developed a transcription and summarization pipeline. However, it had several limitations, including a focus on efficiency over quality, errors in multilingual recordings due to a lack of diarization, and an inability to extract speaker-specific information.

**InterPARES-Audio (RA03A Redux)** is an extension of that work, designed to build a top-line system that focuses on:

1.  **Building a Multilingual Benchmark:** To properly evaluate models on this complex data.
    
2.  **A Validated Pipeline:** To perform high-quality summarization and information extraction, especially for multilingual recordings.
    

## Key Features

-   **End-to-End Processing:** Ingests a long audio file and outputs a structured text report.
    
-   **Speaker Diarization:** Determines "who spoke when" by identifying and tagging different speakers.
    
-   **Multilingual Transcription & LID:** Accurately transcribes speech to text while automatically identifying the language being spoken.
    
-   **Advanced LLM Analysis:** Uses a large language model to perform high-level analysis, summarizing content and extracting key information.
    
-   **Structured Multilingual Output:** Generates clean, organized reports in Arabic, English, French, Spanish, German, and Italian. The reports include:
    
    -   An executive summary
        
    -   Speaker profiles (ID, predicted name, role, key contributions)
        
    -   Main topics discussed
        
    -   Decisions made
        
    -   Action items
        
    -   Key insights
        

## Workflow

The pipeline consists of four main stages:

<p align="center"> <!-- NOTE: Replace with the path to the workflow diagram in your repository --> <img src="IntePARES_Audio_workflow.png" alt="InterPARES-Audio Workflow Diagram" width="800"/> </p>

1.  **Speaker Diarization and Segmentation**: The long audio input is processed to identify speaker changes and segment the audio into a sequence of individual utterances, each tagged with a speaker ID.
    
2.  **Multilingual Speech Model**: Each utterance is fed into a speech model that performs both transcription (speech-to-text) and language identification (LID).
    
3.  **Transcription Manager**: This component merges the individual transcribed utterances, saves the full transcript, and creates manageable, contextually coherent chunks of text optimized for the LLM.
    
4.  **LLM Analysis**: The structured text chunks are analyzed by an LLM to transform raw transcript data into a meaningful and actionable structured report.
    

## Technology Stack

The pipeline is built using state-of-the-art models and tools:

Component

Model / Tool

Hardware Requirement

**Speech Diarization**

`pyannote.audio`

1x A100 (80GB)

**LID & Transcription**

`Whisper Large v3`

(Runs on the same A100)

**Analysis LLM**

`GPT-OSS 20B` (OpenAI open weight)

4x MI200 (AMD, 64GB)

**LLM Hosting**

`Ollama`

-

### Chunk Management

To feed the transcript to the LLM, we manage a context window of 8,912 tokens.

-   We reserve 1,500 tokens for the prompt and output report.
    
-   This leaves 6,642 tokens for the input text.
    
-   The input is split into optimal chunks of 3,321 tokens, or approximately **13,284 characters**.
    

## Benchmark Development

A core part of this project was creating a new benchmark from the UNESCO archives to validate our system.

**Data Processing Funnel:**

-   **Start:** 17,054 Digitized Files
    
-   **Filter 1:** 6,411 (Files with metadata)
    
-   **Filter 2:** 205 (Listed as multilingual)
    
-   **Filter 3:** 89 (From Phase 1: 1954-1968)
    
-   **Filter 4:** 68 (Manually validated for quality and multiple languages)
    
-   **Final Split:** 34 files for **Dev** set and 34 files for **Test** set.
    
    -   All audio was resampled to 16 kHz and 16-bit depth.
        
    -   The splits were balanced for English-French content.
        

**Benchmark Statistics**:

Split

Count

Total Duration

Mean Dur.

Median Dur.

Unique Langs.

**Dev**

34

17H 28M

30M

27M

13

**Test**

34

17H 24M

30M

32M

13

## How to Use

1.  **Clone the repository:**
    
    ```
    git clone [https://github.com/UBC-NLP/InterPARES_audio.git](https://github.com/UBC-NLP/InterPARES_audio.git)
    cd InterPARES_audio
    
    ```
    
2.  **Set up your environment:**
    
    -   Ensure you have the required hardware (see [Technology Stack](#technology-stack "null")).
        
    -   Install dependencies from `requirements.txt`.
        
    -   Set up [Ollama](https://ollama.com/ "null") and pull the `GPT-OSS 20B` model.
        
3.  **Run the analysis:** For a complete, end-to-end example, please see the [**multilingual_audio_analysis.ipynb**](https://github.com/UBC-NLP/InterPARES_audio/blob/main/multilingual_audio_analysis.ipynb "null").
