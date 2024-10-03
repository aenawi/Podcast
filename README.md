# AI-Powered Podcast Creation and Optimization System

This project implements an automated workflow for creating engaging podcasts from academic texts using AI-powered agents. The system takes a PDF file as input, processes its content, and generates an audio podcast with playful banter between a host and a guest. It also includes a self-improving mechanism that optimizes the prompts used in the podcast creation process based on user feedback.

## Key Components

1. **Podcast Creation (paudio.py)**
   - Extracts text from PDF files
   - Utilizes AI agents for summarization, script writing, and script enhancement
   - Generates audio using text-to-speech technology
   - Creates a complete podcast from academic content

2. **Prompt Optimization (src/utils/textGDwithWeightClipping.py)**
   - Uses TextGrad for gradient-based optimization of prompts
   - Implements a WeightClippingAgent to maintain prompt generality
   - Continuously improves the system based on user feedback

3. **Simulation and Evaluation**
   - Simulates the podcast creation and improvement process
   - Evaluates the quality of generated podcasts over time

4. **Web Interface**
   - React-based frontend for user interaction
   - FastAPI backend for handling requests and managing the podcast creation process

## How It Works

1. **Podcast Creation:**
   - The system reads a PDF file and extracts its content.
   - AI agents summarize the content, create a script, and enhance it with engaging dialogue.
   - Text-to-speech technology converts the script into audio.

2. **Prompt Optimization:**
   - User feedback is collected on generated podcasts.
   - TextGrad optimizes the prompts used by AI agents based on this feedback.
   - The WeightClippingAgent ensures prompts remain general and applicable across topics.

3. **Continuous Improvement:**
   - Each podcast creation cycle contributes to the system's learning.
   - Prompts evolve over time, stored with timestamps for version control.
   - The system uses the most recent optimized prompts for each new podcast creation.

## Timestamps

Timestamps are used in this project to version control the prompts used by the AI agents. Each time the system generates a podcast and receives feedback, it optimizes the prompts and saves them with a new timestamp. This allows the system to track the evolution of prompts over time and use the most recent or specific versions when creating new podcasts.

## Usage

1. **Generate a Podcast:**
   ```
   python src/paudio.py <path_to_pdf_file> [--timestamp YYYYMMDD_HHMMSS]
   ```
   Options:
   - `<path_to_pdf_file>`: Path to the PDF file you want to convert into a podcast.
   - `--timestamp YYYYMMDD_HHMMSS`: (Optional) Use prompts from a specific timestamp. If not provided, it uses the most recent prompts.
   - `--timestamp last`: Use the most recent timestamp (same as not providing a timestamp).

   Examples:
   ```
   python src/paudio.py path/to/your/file.pdf
   python src/paudio.py path/to/your/file.pdf --timestamp 20230615_120000
   python src/paudio.py path/to/your/file.pdf --timestamp last
   ```

2. **Generate a Podcast with Feedback:**
   ```
   python src/paudiowithfeedback.py <path_to_pdf_file> [--timestamp YYYYMMDD_HHMMSS]
   ```
   This script creates a podcast and allows you to provide feedback, which is then used to optimize the prompts.

   Options:
   - `<path_to_pdf_file>`: Path to the PDF file you want to convert into a podcast.
   - `--timestamp YYYYMMDD_HHMMSS`: (Optional) Use prompts from a specific timestamp.
   - `--timestamp last`: Use the most recent timestamp (default behavior if no timestamp is provided).

   The script will:
   - Create a podcast using the specified or most recent prompts
   - Save the audio and dialogue text with a new timestamp
   - Ask for your feedback
   - Add the feedback to the podcast state with the new timestamp
   - Use the feedback to optimize the prompts for future use, creating a new set of prompts with the new timestamp

   How it works with timestamps:
   - If no timestamp is provided or 'last' is specified, it uses the most recent set of prompts
   - It generates a new timestamp for the created podcast
   - Feedback and optimized prompts are associated with this new timestamp
   - This allows for tracking the evolution of prompts over time and using specific versions when needed

   Examples:
   ```
   python src/paudiowithfeedback.py path/to/your/file.pdf
   python src/paudiowithfeedback.py path/to/your/file.pdf --timestamp 20230615_120000
   python src/paudiowithfeedback.py path/to/your/file.pdf --timestamp last
   ```

3. **Run Self-Improving Simulation:**
   ```
   python src/simulation.py
   ```
   This script runs a simulation of the podcast creation and prompt optimization process:
   - It randomly selects PDF files from the `arxiv_papers` folder in the project root directory.
   - For each selected PDF, it generates a podcast using the current prompts.
   - An AI agent provides feedback on the generated podcast, simulating human feedback.
   - Based on this feedback, the system optimizes the prompts for future use.
   - This process repeats, simulating the improvement of the system over time without human intervention.
   
   Note: Before running the simulation, make sure to add PDF files to the `arxiv_papers` folder.

4. **Evaluate Self-Improvement Process:**
   ```
   python src/evaluation.py
   ```
   This script evaluates the quality of generated podcasts over time:
   - It randomly selects PDF files from the `arxiv_papers` folder.
   - For each selected PDF, it generates two podcasts:
     1. One using randomly selected prompts from different timestamps.
     2. Another using the most recent prompts.
   - An AI evaluator then compares these two podcasts and chooses the better one.
   - This process helps assess whether the system's prompts are improving over time.

5. **Web Interface:**
   - Start the backend:
     ```
     uvicorn backend.fast_api_app:app --reload
     ```
   - Start the frontend:
     ```
     cd frontend
     npm start
     ```
   - Access the interface at `http://localhost:3000`

## Requirements

- Python 3.7+
- OpenAI API key
- Required Python packages (install via `pip install -r requirements.txt`)
- Node.js and npm for the frontend

### Installing Node.js and npm

Node.js and npm are required for the frontend. Here's how to install them on different operating systems:

#### Windows:
1. Download the installer from the official Node.js website: https://nodejs.org/
2. Run the installer and follow the installation wizard.
3. Restart your computer after installation.

#### macOS:
1. Using Homebrew (recommended):
   ```
   brew install node
   ```
2. Alternatively, download the macOS installer from https://nodejs.org/ and run it.

#### Linux:
For Ubuntu or Debian-based distributions:
```
sudo apt update
sudo apt install nodejs npm
```

For other distributions, refer to your package manager or the official Node.js documentation.

Verify the installation by running:
```
node --version
npm --version
```

## Project Structure

- `src/paudio.py`: Main script for podcast creation
- `src/utils/textGDwithWeightClipping.py`: Prompt optimization script
- `src/simulation.py`: Simulation of the self-improvement process
- `src/evaluation.py`: Evaluation script for generated podcasts
- `backend/fast_api_app.py`: FastAPI backend application
- `frontend/`: React-based frontend application

## Note

This project uses OpenAI's GPT models, which require an API key and may incur costs. Ensure you have appropriate credits or billing set up with OpenAI.

For detailed information on setup, usage, and the self-improvement mechanism, please refer to the sections below.
