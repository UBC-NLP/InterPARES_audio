<center>
<img src="https://dlnlp.ai/img/InterPARES_Audio.jpg" alt="InterPARES_Audio.jpg" width="35%" height="25%" align="right"/>
</center>

# Multilingual Audio Analysis

**InterPARES-Audio** is a sophisticated system designed to listen, transcribe, translate, and analyze complex audio recordings. It is built to handle files with multiple speakers conversing in different languages, making it the ideal tool for processing archives of meetings, interviews, and panel discussions.

## Demo

-   **Live Demo:** [**demos.dlnlp.ai/InterPARES/**](https://demos.dlnlp.ai/InterPARES/ "null")
    
-   **Jupyter Notebook:** [**multilingual_audio_analysis.ipynb**](https://github.com/UBC-NLP/InterPARES_audio/blob/main/multilingual_audio_analysis.ipynb "null")


**InterPARES-Audio** designed to build a top-line system that focuses on:

- **Speaker Diarization:** To identify and separate different speakers in an audio recording, even when they switch languages.</li>

- **Robust Transcription and Translation:** To accurately transcribe spoken words and translate them into a target language, preserving meaning across linguistic boundaries.</li>

- **Summarization:** To generate concise summaries that capture the essence of multi-speaker conversations, highlighting key points and decisions made.</li>       

## Key Features

-   **End-to-End Processing:** Ingests a long audio file and outputs a structured text report.
    
-   **Speaker Diarization:** Determines "who spoke when" by identifying and tagging different speakers.
    
-   **Multilingual Transcription & LID:** Accurately transcribes speech to text while automatically identifying the language being spoken.
    
-   **Advanced LLM Analysis:** Uses a large language model to perform high-level analysis, summarizing content and extracting key information.
    
-   **Structured Multilingual Output:** Generates clean, organized reports in Arabic, English, French, Spanish, German, and Italian. The reports include:
    
      - Speaker profiles with predicted names and roles

      - Main topics discussed

      - Decisions made during the conversation

      - Action items assigned to participants

      - Key insights and takeaways from the discussion

## Workflow

The pipeline consists of four main stages:

<p align="center"> <!-- NOTE: Replace with the path to the workflow diagram in your repository --> <img src="IntePARES_Audio_workflow.png" alt="InterPARES-Audio Workflow Diagram" width="800"/> </p>

1.  **Speaker Diarization and Segmentation**: The long audio input is processed to identify speaker changes and segment the audio into a sequence of individual utterances, each tagged with a speaker ID.
    
2.  **Multilingual Speech Model**: Each utterance is fed into a speech model that performs both transcription (speech-to-text) and language identification (LID).
    
3.  **Transcription Manager**: This component merges the individual transcribed utterances, saves the full transcript, and creates manageable, contextually coherent chunks of text optimized for the LLM.
    
4.  **LLM Analysis**: The structured text chunks are analyzed by an LLM to transform raw transcript data into a meaningful and actionable structured report.
    

## Models & Technologies

This pipeline integrates state-of-the-art deep learning models to handle the complexity of multilingual, multi-speaker audio environments.

### 1. Speaker Diarization
* **Model:** [Pyannote Audio](https://huggingface.co/pyannote/speaker-diarization-3.1) (e.g., `pyannote/speaker-diarization-3.1`)
* **Function:** Responsible for the "Who Spoke When" task. It generates time-stamped speaker segments, distinguishing between different participants in the meeting even amidst interruptions or overlaps.
* **Why it's used:** Pyannote is currently the industry standard for open-source diarization, offering high accuracy in clustering speaker embeddings.

### 2. Multilingual ASR & LID (Language Identification)
* **Model:** [OpenAI Whisper](https://huggingface.co/openai/whisper-large-v3) (e.g., `large-v3` architecture)
* **Function:** Performs robust Speech-to-Text (STT) transcription and automatic Language Identification (LID). 
* **Capabilities:** * Handles noisy audio effectively.
    * Automatically detects language switches (e.g., switching from English to Arabic or French).
    * Provides timestamps that align with the diarization segments.

### 3. LLM Analysis & Summarization
* **Model:** Large Language Models ([openai/gpt-oss-20b](https://huggingface.co/openai/gpt-oss-20b))
* **Function:** Processes the raw, diarized transcripts to generate structured outputs.
* **Output Generation:** * Contextualizes the conversation.
    * Extracts action items, decisions, and summaries.
    * Translates the final report into the user's requested target language (Arabic, English, French, Spanish, German, Italian) while preserving the nuance of the original discussion.

## Online Demo

**Live Demo:** [**demos.dlnlp.ai/InterPARES/**](https://demos.dlnlp.ai/InterPARES/ "null")
<img src="https://demos.dlnlp.ai/InterPARES/interpars_audio_demo.png">
            

## Examples
 [Meeting report, Markdown](https://github.com/UBC-NLP/InterPARES_audio/blob/main/meeting_reports/A05195/meeting_analysis_A05195-20251010_174134-English.md)

 [Meeting report, PDF](https://github.com/UBC-NLP/InterPARES_audio/blob/main/meeting_reports/A05195/meeting_analysis_A05195-20251010_174134-English.pdf)
