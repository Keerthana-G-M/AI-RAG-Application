# AI RAG (Retrieval-Augmented Generation) Application

A full-stack application that enables users to upload PDF documents and ask questions about their content using AI-powered chat functionality. Built with Next.js, LangChain, OpenAI, and Qdrant vector database.

## 🌟 Features

- **PDF Upload**: Upload and process PDF documents
- **AI-Powered Chat**: Ask questions about uploaded PDF content
- **Vector Search**: Semantic search through document content using embeddings
- **Real-time Processing**: Background job processing for document ingestion
- **Modern UI**: Clean and responsive interface with Tailwind CSS
- **Authentication**: Integrated with Clerk for user management

## 🏗️ Architecture

- **Frontend**: Next.js 15 with React 19, TypeScript, and Tailwind CSS
- **Backend**: Express.js API server with background job processing
- **Vector Database**: Qdrant for storing and searching document embeddings
- **Message Queue**: BullMQ with Redis (Valkey) for background job processing
- **AI/ML**: OpenAI GPT-4 for chat responses and text-embedding-3-small for embeddings
- **Document Processing**: LangChain for PDF processing and text splitting

## 🚀 Quick Start

### Prerequisites

- Node.js (v18 or higher)
- Docker and Docker Compose
- OpenAI API key
- pnpm (recommended) or npm

### 1. Clone the Repository

```bash
git clone https://github.com/Keerthana-G-M/AI-RAG-Application.git
cd AI RAG Application
```

### 2. Start Infrastructure Services

```bash
docker-compose up -d
```

This starts:
- **Valkey** (Redis-compatible) on port 6379
- **Qdrant** vector database on port 6333

### 3. Configure Environment Variables

#### Server Configuration
Create a `.env` file in the `server/` directory:

```env
OPENAI_API_KEY=your_openai_api_key_here
REDIS_HOST=localhost
REDIS_PORT=6379
QDRANT_URL=http://localhost:6333
```

#### Client Configuration
Create a `.env.local` file in the `client/` directory:

```env
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=your_clerk_publishable_key
CLERK_SECRET_KEY=your_clerk_secret_key
```

### 4. Install Dependencies

```bash
# Install server dependencies
cd server
pnpm install

# Install client dependencies
cd ../client
pnpm install
```

### 5. Run the Application

#### Terminal 1: Start the API Server
```bash
cd server
pnpm dev
```

#### Terminal 2: Start the Background Worker
```bash
cd server
pnpm dev:worker
```

#### Terminal 3: Start the Frontend
```bash
cd client
pnpm dev
```

The application will be available at `http://localhost:3000`

## 📝 Usage

1. **Upload PDF**: Click the upload area and select a PDF file
2. **Wait for Processing**: The system will process and index your document
3. **Ask Questions**: Use the chat interface to ask questions about the PDF content
4. **Get AI Responses**: Receive contextual answers based on your document

## 🛠️ API Endpoints

### `POST /upload/pdf`
Upload a PDF file for processing
- **Body**: `multipart/form-data` with `pdf` file
- **Response**: `{ message: "uploaded" }`

### `GET /chat?message=your_question`
Ask questions about uploaded documents
- **Query**: `message` - Your question
- **Response**: `{ message: "AI response", docs: [...] }`

## 📦 Tech Stack

### Frontend
- **Framework**: Next.js 15 with Turbopack
- **Language**: TypeScript
- **Styling**: Tailwind CSS
- **UI Components**: Radix UI primitives
- **Icons**: Lucide React
- **Authentication**: Clerk

### Backend
- **Runtime**: Node.js
- **Framework**: Express.js
- **File Upload**: Multer
- **Job Queue**: BullMQ
- **PDF Processing**: LangChain Community loaders
- **Text Splitting**: LangChain Text Splitters

### AI & Vector Search
- **LLM**: OpenAI GPT-4
- **Embeddings**: OpenAI text-embedding-3-small
- **Vector Database**: Qdrant
- **AI Framework**: LangChain

### Infrastructure
- **Message Queue**: Redis (Valkey)
- **Containerization**: Docker Compose

## 🔧 Configuration

### Qdrant Collection Setup

The application uses a Qdrant collection named `langchainjs-testing`. Ensure this collection exists in your Qdrant instance before starting the application.

### OpenAI API Keys

Make sure to replace the empty `apiKey` strings in `server/index.js` and `server/worker.js` with your actual OpenAI API key.

## 📁 Project Structure

```
AI RAG Application/
├── client/                 # Next.js frontend
│   ├── app/
│   │   ├── components/     # React components
│   │   │   ├── chat.tsx
│   │   │   └── file-upload.tsx
│   │   ├── layout.tsx
│   │   └── page.tsx
│   ├── components/ui/      # UI components
│   └── lib/
├── server/                 # Express.js backend
│   ├── index.js           # API server
│   ├── worker.js          # Background job processor
│   └── uploads/           # Uploaded PDF files
└── docker-compose.yml     # Infrastructure services
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## ⚠️ Important Notes

- Make sure to add your OpenAI API key before running the application
- The application requires active Qdrant and Redis services
- PDF processing happens asynchronously in the background
- Ensure sufficient disk space for uploaded PDF files

## 🆘 Troubleshooting

### Common Issues

1. **Connection refused errors**: Ensure Docker services are running
2. **OpenAI API errors**: Verify your API key is valid and has `sufficient credits`
3. **File upload issues**: Check the `uploads/` directory permissions
4. **Chat not working**: Ensure documents are processed and indexed in Qdrant

### Support

If you encounter any issues, please check the existing issues or create a new one in the GitHub repository.
