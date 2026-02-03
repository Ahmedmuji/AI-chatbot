# AI Chatbot with RAG & Voice Input

A powerful AI-powered chatbot built with Streamlit that supports document querying, data analysis, voice input, and intelligent conversation management. This chatbot leverages Retrieval-Augmented Generation (RAG) to provide context-aware responses from uploaded documents and uses advanced LLMs for natural language processing.

## Features

### Core Capabilities
- **Retrieval-Augmented Generation (RAG)**: Query and extract information from uploaded documents using FAISS vector database
- **Voice Input Support**: Convert speech to text using Google Speech Recognition
- **Multi-Format File Support**: Upload and analyze PDF, DOCX, TXT, CSV, and XLSX files
- **Data Analysis**: Intelligent data querying and visualization for CSV/Excel files using PandasAI
- **Chat History Management**: Persistent chat sessions stored in SQLite database
- **Session Management**: Create, switch between, and manage multiple chat sessions

### Conversation Features
- **Context-Aware Responses**: Maintains conversation context across messages
- **General Query Support**: Handle both document-specific and general conversational queries
- **Smart Response Types**: Automatically detects whether to use RAG or general LLM responses
- **Image & Chart Generation**: Automatically generates and displays charts from data queries

## Technology Stack

- **Frontend**: Streamlit
- **LLM Provider**: Groq API (Mixtral-8x7b-32768 model)
- **Embeddings**: HuggingFace (sentence-transformers/all-MiniLM-L6-v2)
- **Vector Database**: FAISS
- **Framework**: LangChain
- **Data Analysis**: PandasAI
- **Database**: SQLite
- **Speech Recognition**: Google Speech Recognition API
- **Document Processing**: PyPDF2, python-docx, pandas

## Prerequisites

- Python 3.8 or higher
- Microphone (for voice input feature)
- Internet connection (for API calls)

## Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/Ahmedmuji/AI-chatbot.git
   cd AI-chatbot
   ```

2. **Install required dependencies**
   ```bash
   pip install streamlit groq langchain langchain-community langchain-groq langchain-huggingface
   pip install faiss-cpu PyPDF2 python-docx pandas openpyxl
   pip install pandasai speechrecognition pyaudio python-dotenv
   pip install matplotlib seaborn regex
   ```

3. **Set up environment variables**
   
   Create a `.env` file in the project root directory:
   ```env
   GROQ_API_KEY=your_groq_api_key_here
   PANDASAI_API_KEY=your_pandasai_api_key_here
   OPENAI_API_KEY=your_openai_api_key_here
   ```

   **How to get API keys:**
   - **Groq API**: Sign up at [https://console.groq.com](https://console.groq.com)
   - **PandasAI**: Get your key from [https://pandabi.ai](https://pandabi.ai)
   - **OpenAI** (optional): Get from [https://platform.openai.com](https://platform.openai.com)

## Usage

1. **Start the application**
   ```bash
   streamlit run chatbot.py
   ```

2. **Access the chatbot**
   - The application will open in your default browser
   - Default URL: `http://localhost:8501`

### Using the Chatbot

#### Text Input
1. Type your message in the chat input box at the bottom
2. Press Enter to send

#### Voice Input
1. Click the 🎤 microphone button
2. Speak your query clearly
3. The chatbot will transcribe and process your speech

#### File Upload
1. Click the upload icon (📎)
2. Select a file (PDF, DOCX, TXT, CSV, or XLSX)
3. Choose response type:
   - **File_Query**: Query the uploaded document/data
   - **Normal_Query**: General conversation (ignores uploaded file)

#### Session Management
- **New Chat**: Click "New Chat" in the sidebar to start a fresh conversation
- **Switch Sessions**: Click on any previous chat in the sidebar to resume
- **Clear History**: Click "Clear All History" to delete all sessions

## Supported File Types

| File Type | Extension | Use Case |
|-----------|-----------|----------|
| PDF | `.pdf` | Document querying with RAG |
| Word Document | `.docx` | Document querying with RAG |
| Text File | `.txt` | Document querying with RAG |
| CSV | `.csv` | Data analysis and visualization |
| Excel | `.xlsx` | Data analysis and visualization |

## Project Structure

```
AI-chatbot/
├── chatbot.py              # Main application file
├── .env                    # Environment variables (not in repo)
├── .devdbrc               # Database configuration
├── chat_sessions.db       # SQLite database for chat history
├── faiss_index/           # FAISS vector database storage
├── cache/                 # Application cache
├── exports/               # Generated charts and exports
├── image.png              # Chatbot logo/icon
└── README.md              # This file
```

## Configuration

### FAISS Database
- **Path**: `faiss_index/`
- **Embedding Model**: sentence-transformers/all-MiniLM-L6-v2
- **Automatically recreated** when new documents are uploaded

### Chat Database
- **Database**: SQLite (`chat_sessions.db`)
- **Tables**: 
  - `sessions`: Stores chat session metadata
  - `messages`: Stores all messages with timestamps

### LLM Configuration
- **Model**: Mixtral-8x7b-32768
- **Temperature**: 0 (deterministic responses)
- **Max Tokens**: 1024
- **Context Window**: 32,768 tokens

## Features in Detail

### Retrieval-Augmented Generation (RAG)
The chatbot uses RAG to provide accurate, context-aware responses from your documents:
1. Documents are split into chunks using RecursiveCharacterTextSplitter
2. Chunks are embedded using HuggingFace embeddings
3. Embeddings are stored in FAISS vector database
4. User queries are matched against relevant document chunks
5. LLM generates responses based on retrieved context

### Data Analysis with PandasAI
For CSV and Excel files:
- Natural language queries on data
- Automatic chart generation
- Statistical analysis
- Data filtering and aggregation

### Voice Recognition
- Uses Google Speech Recognition API
- Adjusts for ambient noise
- 5-second timeout for speech detection
- Automatic transcription to text

## Troubleshooting

### Common Issues

**1. Microphone not working**
- Ensure microphone permissions are granted
- Check if PyAudio is properly installed
- On Windows: May need to install PyAudio from wheel file

**2. API Rate Limits**
- The chatbot implements exponential backoff for rate limits
- Wait a few minutes if you hit rate limits
- Consider upgrading your Groq API plan

**3. File Upload Issues**
- Ensure file is not corrupted
- Check file size (very large files may cause issues)
- Verify file format is supported

**4. FAISS Index Errors**
- Delete the `faiss_index/` folder and re-upload your document
- Ensure sufficient disk space

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

This project is open source and available under the [MIT License](LICENSE).

## Author

**Ahmed Muji**
- GitHub: [@Ahmedmuji](https://github.com/Ahmedmuji)

## Acknowledgments

- [Streamlit](https://streamlit.io/) for the amazing web framework
- [Groq](https://groq.com/) for fast LLM inference
- [LangChain](https://langchain.com/) for the RAG framework
- [FAISS](https://github.com/facebookresearch/faiss) for vector similarity search
- [PandasAI](https://pandas-ai.com/) for natural language data analysis

## Support

If you encounter any issues or have questions, please:
1. Check the [Issues](https://github.com/Ahmedmuji/AI-chatbot/issues) page
2. Create a new issue if your problem isn't already listed
3. Provide detailed information about your environment and the error

---

**If you find this project useful, please consider giving it a star!**
