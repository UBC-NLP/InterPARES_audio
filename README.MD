<center>
<img src="https://dlnlp.ai/img/InterPARES_Audio.jpg" alt="InterPARES_Audio.jpg" width="35%" height="25%" align="right"/>
</center>

# Multilingual Audio Analysis

**InterPARES-Audio** is a sophisticated system designed to listen, transcribe, translate, and analyze complex audio recordings. It is built to handle files with multiple speakers conversing in different languages, making it the ideal tool for processing archives of meetings, interviews, and panel discussions.

## Demo

-   **Live Demo:** [**demos.dlnlp.ai/InterPARES/**](https://demos.dlnlp.ai/InterPARES/ "null")
    
-   **Jupyter Notebook:** [**multilingual_audio_analysis.ipynb**](https://github.com/UBC-NLP/InterPARES_audio/blob/main/multilingual_audio_analysis.ipynb "null")
        
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
    


## Examples
 [Meeting report, Markdown](https://github.com/UBC-NLP/InterPARES_audio/blob/main/meeting_reports/A05195/meeting_analysis_A05195-20251010_174134-English.md)

 [Meeting report, PDF](https://github.com/UBC-NLP/InterPARES_audio/blob/main/meeting_reports/A05195/meeting_analysis_A05195-20251010_174134-English.pdf)
