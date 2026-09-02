# Agentic Research Assistant

An AI-powered **Agentic Research Assistant** that automatically researches a given topic across multiple academic, research, educational, and trusted information sources, summarizes the collected content using an LLM, generates structured academic sections, and produces a professionally formatted PDF report.

The application is built with **Python and Streamlit** and combines web scraping, LLM-based summarization, automated report generation, and PDF creation into a single research workflow.

**Author:** Jawaria Tariq

**GitHub:** https://github.com/mjawariatariq/Agentic-Research-Assistant/tree/main

## Features

* **Multi-Source Web Research** — searches predefined academic, research, educational, and knowledge websites
* **Academic Research Support** — includes sources such as arXiv, Semantic Scholar, PubMed, ACL Anthology, and CVF Open Access
* **AI-Powered Summarization** — summarizes collected research content using an LLM
* **Agentic Research Workflow** — automates the process from research topic to final report
* **Structured Academic Report** — generates Abstract, Introduction, Methodology, Findings, Discussion, and Conclusion
* **Streamlit Interface** — provides a simple and interactive research dashboard
* **Source Tracking** — preserves URLs of websites used during research
* **PDF Report Generation** — creates a formatted academic PDF report
* **Fallback Handling** — handles cases where relevant research content cannot be retrieved
* **Web Scraping** — extracts readable text from supported websites using Requests and BeautifulSoup
* **Environment Configuration** — supports secure API-key management through `.env`

## Project Workflow

```text
                    Research Topic
                          │
                          ↓
                Agentic Research Agent
                          │
                          ↓
                Multiple Trusted Sources
                          │
                          ↓
                  Web Scraping Layer
                          │
                          ↓
                 Relevant Web Content
                          │
                          ↓
                 LLM Summarization
                          │
                          ↓
              Academic Report Generation
                          │
          ┌───────────────┼────────────────┐
          ↓               ↓                ↓
      Abstract       Methodology       Findings
          ↓               ↓                ↓
      Discussion      Conclusion      References
          │               │                │
          └───────────────┼────────────────┘
                          ↓
                  Formatted PDF Report
```

## Supported Research Sources

The assistant uses a predefined collection of websites covering multiple categories.

### Academic & Preprint Sources

* arXiv
* Papers With Code
* CVF Open Access
* Semantic Scholar
* PubMed
* ACL Anthology

### AI Research Organizations

* OpenAI
* Google Research
* Google AI
* Hugging Face
* Meta AI
* Allen Institute for AI
* Microsoft Research
* IBM Research
* NVIDIA Research

### General Knowledge & Educational Sources

* Wikipedia
* Simple English Wikipedia
* CIA World Factbook
* NationMaster
* Khan Academy
* Britannica
* Fact Monster
* Ducksters
* OpenStax
* World Bank Open Data

## Project Structure

```text
Agentic-Research-Assistant/
│
├── agents/
│   └── agent.py                 # Agentic research workflow
│
├── utils.py                     # LLM summarization and report generation
├── web_scraper.py               # Website scraping and content extraction
├── app.py                       # Streamlit application
├── requirements.txt             # Project dependencies
├── .env                         # API keys and environment variables
├── .gitignore                   # Files excluded from Git
└── README.md                    # Project documentation
```

> Adjust the structure above if your actual repository uses different filenames or folders.

## How It Works

### 1. User Provides a Research Topic

The Streamlit interface allows the user to enter a research question or topic.

Example:

```text
Impact of AI on student learning outcomes
```

The user can also provide report metadata such as:

* Report title
* Author
* Institution
* Report date
* Subtitle

### 2. Source Selection

The research agent receives the query and predefined list of websites:

```python
pages = scrape_websites(query, SITES)
```

The scraper iterates through the configured sources and attempts to retrieve relevant content.

### 3. Web Scraping

The application uses:

* `requests`
* `BeautifulSoup`
* `fake-useragent`
* Regular expressions

to retrieve and clean webpage content.

Unnecessary HTML elements such as:

```text
script
style
nav
footer
iframe
noscript
```

are removed before extracting readable text.

### 4. Relevant Content Detection

The scraper checks whether the research query or its keywords appear in the extracted webpage text.

Relevant pages are returned in a structured format:

```python
{
    "url": site,
    "text": text
}
```

### 5. AI Summarization

The collected content is combined and passed to the LLM:

```python
summary = summarize(pages, query)
```

The model receives the research topic and retrieved content and generates an academic-style summary.

### 6. Academic Section Generation

The summary is then transformed into structured academic sections:

```text
Abstract
Introduction
Methodology
Findings / Results
Discussion / Analysis
Conclusion
```

Each section is generated independently using dedicated prompts.

### 7. PDF Generation

The completed report is formatted into a PDF using `FPDF`.

The generated report includes:

* Cover page
* Report metadata
* Table of contents
* Academic sections
* References
* Page numbers

## Academic Report Structure

The generated report follows this structure:

```text
Cover Page
     ↓
Table of Contents
     ↓
Abstract
     ↓
Introduction
     ↓
Methodology
     ↓
Findings / Results
     ↓
Discussion / Analysis
     ↓
Conclusion
     ↓
References
```

## Streamlit Interface

The application provides an interactive interface containing:

### Report Information

Users can enter:

* Report title
* Author
* Institution
* Report date
* Subtitle

### Research Topic

Users enter the research question or topic they want the assistant to investigate.

### Start Research

Clicking:

```text
🚀 Start Research
```

starts the research workflow.

The application then:

1. Scrapes configured websites
2. Identifies relevant content
3. Summarizes the retrieved information
4. Generates academic sections
5. Stores the report in Streamlit session state

### PDF Export

After successful research, users can generate a formatted PDF report:

```text
📄 Download Formatted Report as PDF
```

## Error Handling

The application handles several possible failures.

### No Relevant Sources

If no relevant content is found, the application displays:

```text
❌ No relevant topics found on any authentic websites.
```

It also suggests trying broader topics such as:

```text
Climate change
Impact of water pollution
AI in education
```

### Website Request Failures

Individual websites that fail to respond are skipped rather than stopping the complete research process.

### API Failures

If the LLM API request fails, the application returns an error message instead of crashing the entire application.

## LLM Integration

The current implementation uses the **Groq API** with an OpenAI-compatible chat completion endpoint.

The model configured in the code is:

```text
meta-llama/llama-4-scout-17b-16e-instruct
```

The application sends prompts through:

```text
Groq API
    ↓
LLM
    ↓
Generated Summary / Report Section
```

## Environment Variables

For security, API credentials should be stored in a `.env` file.

Example:

```env
GROQ_API_KEY=your_groq_api_key_here
```

Then load it using:

```python
from dotenv import load_dotenv
import os

load_dotenv()

API_KEY = os.getenv("GROQ_API_KEY")
```

### Security Warning

**Never hard-code API keys in Python source code.**

If an API key has already been committed to GitHub, revoke/rotate it and replace it with a new key.

Add the following to `.gitignore`:

```text
.env
__pycache__/
*.pyc
venv/
```

## Installation

### Prerequisites

* Python 3.8+
* Groq API key
* Internet connection for web research

### 1. Clone the Repository

```bash
git clone https://github.com/mjawariatariq/Agentic-Research-Assistant.git
cd Agentic-Research-Assistant
```

### 2. Create a Virtual Environment

```bash
python -m venv venv
```

Activate it on Windows:

```bash
venv\Scripts\activate
```

On macOS/Linux:

```bash
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

Or install manually:

```bash
pip install streamlit google-generativeai requests beautifulsoup4 python-dotenv fake-useragent fpdf
```

## Run the Application

Start the Streamlit application:

```bash
streamlit run app.py
```

The application will open at:

```text
http://localhost:8501
```

## Requirements

The main dependencies are:

```text
streamlit
google-generativeai
requests
beautifulsoup4
python-dotenv
fake-useragent
fpdf
```

## Example

### Research Topic

```text
Impact of Artificial Intelligence on Education
```

### Generated Workflow

```text
Research Topic
      ↓
Academic & Trusted Sources
      ↓
Web Scraping
      ↓
Content Extraction
      ↓
AI Summarization
      ↓
Academic Sections
      ↓
PDF Report
```

### Example Output Sections

```text
Abstract

Introduction

Methodology

Findings / Results

Discussion / Analysis

Conclusion

References
```

## Key Benefits

* Reduces manual research time
* Collects information from multiple sources
* Automates academic report preparation
* Produces structured research content
* Keeps track of research sources
* Provides downloadable PDF reports
* Combines web scraping with generative AI
* Provides a simple Streamlit-based user experience

## Future Improvements

* Add proper search-engine/API-based research instead of scraping only homepage URLs
* Add source relevance ranking
* Add semantic search for retrieved content
* Add RAG using FAISS
* Add document upload support for PDFs and research papers
* Add citation generation
* Add APA/MLA/IEEE citation styles
* Add source credibility scoring
* Add duplicate-source detection
* Add research history
* Add persistent database storage
* Add multi-agent research planning
* Add parallel website research
* Add streaming LLM responses
* Add advanced academic writing controls
* Add export to DOCX and Markdown
* Add automated fact verification

## Limitations

The current implementation primarily scrapes the configured website URLs and checks whether the research query or its keywords appear in the retrieved page content. It does not yet perform full search-engine-style crawling across every individual article or paper.

For high-quality academic research, retrieved information should therefore be reviewed and verified against the original sources.

## License

This project is open-source and available for educational and personal use.

## Author

**Jawaria Tariq**

AI Engineer | LLM Applications | RAG | AI Agents | Automation

GitHub: https://github.com/mjawariatariq

## Acknowledgments

* **Streamlit** — interactive web application framework
* **BeautifulSoup** — HTML parsing and web content extraction
* **Requests** — HTTP requests and website retrieval
* **Groq** — LLM inference API
* **Meta Llama** — language model
* **FPDF** — PDF report generation
* **Python-dotenv** — environment variable management
