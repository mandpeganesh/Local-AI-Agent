# Local-AI-Agent

A local AI-powered question answering system for restaurant reviews using LangChain and Ollama. This project creates a vector database from pizza restaurant reviews and allows you to ask questions about restaurants based on these reviews.

## Features

- Vector embedding storage of restaurant reviews using Chroma DB
- Semantic search to find relevant reviews based on user questions
- Local LLM-powered question answering using Ollama
- No data sent to external APIs - everything runs locally on your machine

## Prerequisites

- Python 3.8+
- [Ollama](https://ollama.ai/) installed locally
- The following Ollama models pulled:
  - `mxbai-embed-large` for embeddings
  - `llama3.2` for question answering

## Installation

1. Clone this repository:

   ```bash
   git clone https://github.com/mandpeganesh/Local-AI-Agent.git
   cd Local-AI-Agent
   ```
2. Install required dependencies:

   ```bash
   pip install -r requirements.txt
   ```
3. Ensure Ollama is running in the background.

## How it Works

1. The [`vector.py`](vector.py) script:

   - Reads restaurant reviews from [`realistic_restaurant_reviews.csv`](realistic_restaurant_reviews.csv)
   - Creates vector embeddings using the Ollama `mxbai-embed-large` model
   - Stores these embeddings in a local Chroma database in the [`chrome_langchain_db`](chrome_langchain_db) directory
   - Sets up a retriever that can find the most relevant reviews for a given query
2. The [`main.py`](main.py) script:

   - Creates a question-answering chain using the Ollama `llama3.2` model
   - Takes user questions as input
   - Retrieves relevant reviews based on the question
   - Uses the LLM to generate answers based on the retrieved reviews

## Usage

1. Run the main script:

   ```bash
   python main.py
   ```
2. Enter your questions about the pizza restaurant when prompted.
3. Type 'q' to quit the application.

## Known Issues

- There's a bug in [`main.py`](main.py) where regardless of user input, the question sent to the LLM is always "What is the best pizza place in town?". To fix this, modify line 21 to use the actual user question.

## Data

The [`realistic_restaurant_reviews.csv`](realistic_restaurant_reviews.csv) file contains 100+ detailed pizza restaurant reviews with ratings, dates, and rich descriptive content. This provides the knowledge base for the AI to answer questions.

## License

[MIT License](LICENSE)
