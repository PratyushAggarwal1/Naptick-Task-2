# Naptick-Task-2
# NapCoach AI: Your Fine-Tuned Sleep Assistant

This repository contains the Python script for NapCoach AI, a voice-enabled sleep coaching assistant powered by a fine-tuned Mistral-7B model. This guide explains how to run it using Google Colab.

## Prerequisites

1.  **Google Account**: Required for Google Colab.
2.  **Hugging Face Account & Access Token**:
    *   Sign up at [huggingface.co](https://huggingface.co/).
    *   Create an Access Token: Go to your Hugging Face Profile -> Settings -> Access Tokens -> New token (give it "read" or "write" role).
3.  **GitHub Repository**: You need this file (`your_script_name.py`) from the repository.

## How to Run in Google Colab

1.  **Open Google Colab**: Go to [colab.research.google.com](https://colab.research.google.com/).
2.  **Upload from GitHub**:
    *   In Colab, go to **File -> Upload notebook**.
    *   Switch to the **GitHub** tab.
    *   Paste the URL of your Python file from this GitHub repository (e.g., `https://github.com/YOUR_USERNAME/YOUR_REPOSITORY/blob/main/your_script_name.py`).
    *   Click the search icon and select the file. Colab will open it as a notebook.
    *   *(Alternatively, you can download the `.py` file and then use "File -> Upload notebook" and select the downloaded file from your computer.)*
3.  **Set Up GPU Runtime**:
    *   In Colab, go to **Runtime -> Change runtime type**.
    *   Select **T4 GPU** (or other available GPU) from the "Hardware accelerator" dropdown.
    *   Click **Save**.
4.  **Add Hugging Face Token as Secret**:
    *   In the Colab notebook, click the **🔑 (Key) icon** on the left sidebar.
    *   Click **+ Add new secret**.
    *   **Name**: `HF_TOKEN`
    *   **Value**: Paste your Hugging Face Access Token.
    *   Make sure "Notebook access" is toggled ON for this secret.
5.  **Run the Cells Sequentially**:
    *   Your Python script will be loaded into a Colab notebook, likely as one large code cell or divided if it had special `# %%` or `# @title` comments.
    *   **If it's one large cell**: You'll need to manually divide it into logical blocks (like installations, model loading, function definitions, fine-tuning, Gradio app launch) to run them step-by-step. This is crucial as some steps (like fine-tuning) depend on previous ones and can take a long time.
    *   **If it's already divided (ideal)**: Run each cell in order from top to bottom by clicking the "play" button next to each cell or using `Shift+Enter`.
6.  **Execution Order & Key Steps**:
    *   **Cell 1 (Installations)**: Installs necessary libraries. This will take several minutes.
    *   **GPU Check & Model Loading**: Subsequent cells will verify GPU, load STT, TTS, and the base LLM (Mistral-7B). The LLM download is large and will take time.
    *   **Hugging Face Login**: Ensure the cell that uses `userdata.get('HF_TOKEN')` runs successfully.
    *   **Function Definitions**: Cells defining `transcribe_audio`, `get_llm_response`, etc., will just define these functions.
    *   **Fine-Tuning Data & Process**: The cell that prepares the dataset and runs `trainer.train()` is the fine-tuning step. This is **very time-consuming** (can be 30 minutes to hours).
    *   **Load Fine-Tuned Model**: Applies the trained adapter to the base model.
    *   **Gradio App Launch**: The final cell launches the Gradio web interface. Look for a public URL (ending in `.gradio.live`) in the cell output and click it to open the NapCoach AI in your browser.

## Important Notes

*   **Cell Division**: If your `.py` file loads as a single cell in Colab, it's **highly recommended** to manually split it into smaller, manageable cells based on the logical steps (installations, model loading, fine-tuning, UI launch). This makes debugging and execution control much easier. You can add new code cells above/below existing code.
*   **Time**: Full execution, including model downloads and fine-tuning, can take a significant amount of time.
*   **Colab Resources**: Free Colab has resource limits. If you face "Out of Memory" errors, try "Runtime -> Disconnect and delete runtime", then reconnect and run cells again.
*   **Saving Trained Adapters**: The fine-tuned model adapter is saved within the Colab environment. If you want to keep it permanently, download it from Colab's file browser (left sidebar, folder icon) before the runtime disconnects.

## Interacting with NapCoach AI

Once the final Gradio cell is running and you've opened the public URL:
*   Use the microphone or upload audio for voice input.
*   Type your questions in the text box.
*   The assistant will reply with text and autoplaying voice.

Enjoy your personalized sleep coach!
