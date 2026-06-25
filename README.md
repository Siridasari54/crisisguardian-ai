# CrisisGuardian AI 🛡️

[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.100+-green.svg)](https://fastapi.tiangolo.com/)
[![Streamlit](https://img.shields.io/badge/Streamlit-1.20+-red.svg)](https://streamlit.io/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

CrisisGuardian AI is a premium, multi-agent emergency response assistant designed to guide users safely through natural disasters and domestic hazards. Utilizing **Gemini 2.5 Flash**, **LangGraph**, and **FastAPI**, it routes emergency questions to specialized agents (Flood, Cyclone, Earthquake, Fire) and queries real-time information using built-in crisis tools.

## 🎯 Overview

CrisisGuardian AI acts as a digital first-responder during critical emergencies. The platform aggregates data feeds, evaluates active threat levels, discovers open shelter facilities, and provides clear, authoritative survival guidelines through an intelligent multi-agent pipeline.

### 🌟 Key Features

- **🧠 Supervisor-Led Dispatcher Routing**: Automatically classifies inquiries and delegates response tasks to specialized agents using intelligent parsing
- **🚨 Crisis Specialists**: Four distinct AI agents pre-conditioned with life-saving safety policies (Floods, Cyclones, Earthquakes, Fires)
- **🔧 Integrated Action Tools**: Supports finding shelter locations, querying USGS for live earthquake alerts, retrieving weather bulletins, and triggering SOS emergency broadcasts
- **🎨 Glassmorphic Streamlit UI**: A premium dark-themed dashboard presenting live warnings, simulated SOS triggers, dynamic crisis scenario panels, and interactive chat
- **🛡️ Graceful Offline Fallbacks**: Automatically falls back to mock logic if external APIs are unavailable, ensuring system reliability
- **📊 Real-time Risk Assessment**: Multi-factor threat evaluation using weather data, news feeds, and resource availability
- **📄 Document Analysis**: Upload and analyze emergency protocols using RAG (Retrieval-Augmented Generation) with FAISS
- **📍 Resource Locator**: Automatically indexes safe houses, emergency hospitals, and municipal relief camps using OpenStreetMap

---

## 📂 Project Structure

```
crisisguardian-ai/
├── agents/                 # Specialized LLM Agents (Gemini 2.5 Flash + LangChain)
│   ├── base_agent.py       # Core base class configuration
│   ├── disaster_agents.py  # Flood, Cyclone, Earthquake, Fire & Supervisor agents
│   ├── coordinator_agent.py
│   ├── weather_agent.py
│   ├── news_agent.py
│   ├── resource_agent.py
│   ├── risk_agent.py
│   └── response_agent.py
├── workflows/              # LangGraph multi-agent coordination state chart
│   ├── __init__.py
│   └── crisis_workflow.py  # Sequential agent pipeline
├── tools/                  # Custom tools (Weather, News, Resources, Disaster utils)
│   ├── __init__.py
│   ├── weather_tool.py     # OpenWeatherMap integration
│   ├── news_tool.py        # Emergency news and broadcasts
│   ├── resource_tool.py    # OpenStreetMap resource locator
│   └── disaster_tools.py   # Disaster-specific utilities
├── backend/                # FastAPI backend (entry: backend/api.py)
│   ├── __init__.py
│   ├── app.py              # Legacy entry point
│   └── api.py              # Main FastAPI application
├── frontend/               # Streamlit interactive UI dashboard
│   ├── app.py              # Main Streamlit entry point
│   ├── utils.py            # Shared styling and utilities
│   └── pages/              # 7 multi-page app views
│       ├── 1_Home.py
│       ├── 2_Disaster_Analysis.py
│       ├── 3_Resource_Finder.py
│       ├── 4_Document_Analyzer.py
│       ├── 5_Agent_Monitor.py
│       └── 6_System_Status.py
├── docs/                   # System design, architecture diagrams, and guides
├── tests/                  # Unit tests
│   ├── __init__.py
│   └── test_agents_tools.py
├── logs/                   # Application logs directory
├── screenshots/            # Project screenshots
├── error_handling.py       # Graceful fallbacks and offline mode
├── logging_config.py       # Centralized logging setup
├── verify_setup.py         # Automated setup verification
├── Dockerfile              # Backend container
├── Dockerfile.streamlit    # Frontend container
├── docker-compose.yml      # Multi-container deployment
├── requirements.txt        # Python dependencies
├── .env.template           # Environment config template
├── .gitignore              # Git ignore rules
├── main.py                 # Backend runner entrypoint
├── README.md               # This file
├── GETTING_STARTED.md      # Detailed setup guide
├── IMPLEMENTATION_SUMMARY.md  # Implementation details
└── LICENSE                 # MIT License
```

---

## ⚡ Quickstart Guide

### 1. Prerequisites

- **Python**: 3.10 or higher
- **pip**: Latest version
- **Git**: For cloning the repository
- **Google Gemini API Key**: [Get one here](https://makersuite.google.com/app/apikey)
- **OpenWeatherMap API Key** (Optional): [Get one here](https://openweathermap.org/api)

### 2. Clone the Repository

```bash
git clone <repository-url>
cd crisisguardian-ai
```

### 3. Environment Configuration

```bash
# Copy the environment template
cp .env.template .env

# Edit .env and add your API keys
# Required: GEMINI_API_KEY
# Optional: OPENWEATHER_API_KEY
```

Edit `.env` with your actual API keys:
```env
GEMINI_API_KEY=your_actual_gemini_api_key_here
OPENWEATHER_API_KEY=your_actual_openweather_api_key_here
```

### 4. Install Dependencies

```bash
# Create a virtual environment (recommended)
python -m venv venv

# Activate virtual environment
# Windows:
venv\Scripts\activate
# Linux/Mac:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt
```

### 5. Verify Setup

```bash
python verify_setup.py
```

This will check:
- Python version compatibility
- Required package installation
- API key configuration
- Module import functionality

### 6. Launch the Backend API

```bash
python main.py
```

The API will start on `http://127.0.0.1:8000` with the following endpoints:
- `GET /` - Welcome message
- `GET /health` - Health check
- `POST /analyze` - Disaster analysis endpoint
- `POST /resources` - Resource finder
- `POST /document-analysis` - Document upload and analysis
- `POST /document-query` - Query uploaded documents
- `POST /api/sos` - Emergency SOS alert
- `GET /system-status` - System status
- `GET /agent-status` - Agent status
- `GET /docs` - Interactive API documentation

### 7. Run the Streamlit Interface

In a new terminal:

```bash
# Activate virtual environment if not already active
venv\Scripts\activate  # Windows
# source venv/bin/activate  # Linux/Mac

# Navigate to frontend directory
cd frontend

# Run Streamlit
streamlit run app.py
```

Open your browser and navigate to `http://localhost:8501`

### 8. Docker Deployment (Optional)

```bash
# Build and run with Docker Compose
docker-compose up -d

# Access the application
# Backend: http://localhost:8000
# Frontend: http://localhost:8501
```

---

## 🛠️ Tech Stack

### Core Technologies

- **AI Engine**: Google Gemini 2.5 Flash via `langchain-google-genai`
- **Orchestration**: LangGraph StateGraph for multi-agent coordination
- **Backend**: FastAPI with Uvicorn ASGI server
- **Frontend**: Streamlit Web UI with custom glassmorphic styling
- **Vector Database**: FAISS for document RAG and similarity search
- **External APIs**:
  - OpenWeatherMap - Real-time weather data and alerts
  - OpenStreetMap Nominatim - Geocoding and resource location
  - USGS - Earthquake data (integration ready)

### Key Libraries

- **LangChain**: LLM framework and agent orchestration
- **LangGraph**: Stateful multi-agent workflows
- **Pydantic**: Data validation and settings management
- **Requests**: HTTP client for API integrations
- **PyPDF**: PDF document processing
- **python-dotenv**: Environment variable management

---

## 🚀 Usage Examples

### API Usage

#### Disaster Analysis

```bash
curl -X POST "http://127.0.0.1:8000/analyze" \
  -H "Content-Type: application/json" \
  -d '{
    "user_id": "test_user",
    "message": "There is a flood warning in Mumbai",
    "location": "Mumbai",
    "crisis_type": "flood"
  }'
```

#### Resource Finder

```bash
curl -X POST "http://127.0.0.1:8000/resources" \
  -H "Content-Type: application/json" \
  -d '{
    "location": "Mumbai"
  }'
```

#### SOS Emergency Alert

```bash
curl -X POST "http://127.0.0.1:8000/api/sos" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "John Doe",
    "phone": "1234567890",
    "location": "Mumbai",
    "description": "Need immediate help - water rising"
  }'
```

### Python SDK Usage

```python
import requests

# Initialize backend URL
BACKEND_URL = "http://127.0.0.1:8000"

# Analyze disaster situation
response = requests.post(f"{BACKEND_URL}/analyze", json={
    "user_id": "user123",
    "message": "Cyclone warning in Andhra Pradesh",
    "location": "Andhra Pradesh",
    "crisis_type": "cyclone"
})

result = response.json()
print(f"Threat Level: {result['threat_level']}")
print(f"Risk Score: {result['risk_score']}")
print(f"Guidance: {result['guidance']}")
```

---

## 🏗️ Architecture

### Multi-Agent Pipeline

The system uses a sequential LangGraph workflow:

```
START → Coordinator → Weather → News → Resource → Risk → Response → Checklist → END
```

1. **Coordinator Agent**: Parses user query, extracts location and disaster type
2. **Weather Agent**: Fetches real-time weather data and alerts
3. **News Agent**: Retrieves emergency broadcasts and news
4. **Resource Agent**: Locates nearby shelters, hospitals, and emergency services
5. **Risk Agent**: Computes threat level and risk score using multi-factor analysis
6. **Response Agent**: Generates comprehensive safety guidance
7. **Checklist Generator**: Creates disaster-specific emergency checklist

### Error Handling & Fallbacks

The system includes robust error handling:
- **API Failures**: Automatic fallback to mock data
- **Network Issues**: Graceful degradation with cached responses
- **Invalid Inputs**: Validation with user-friendly error messages
- **Service Unavailability**: Offline mode with essential functionality

---

## 📊 Features in Detail

### 🏠 Home Page
- System metrics and health indicators
- Project overview and architecture visualization
- Technology stack breakdown
- Quick access to all features

### 🚨 Disaster Analysis
- Natural language query input
- Intelligent disaster type detection
- Real-time threat assessment
- Comprehensive safety protocols
- Recommended action items

### 📍 Resource Finder
- Location-based shelter search
- Hospital and medical facility locator
- Emergency services (police, fire) finder
- Distance and availability information

### 📄 Document Analyzer
- PDF document upload for emergency protocols
- RAG-based document analysis
- Natural language querying of uploaded documents
- Summary and recommendation generation

### 🤖 Agent Monitor
- Real-time agent status monitoring
- Execution time metrics
- Success/failure tracking
- Performance analytics

### ⚙️ System Status
- Backend health check
- API availability status
- Service connectivity monitoring
- Configuration overview

---

## 🔧 Configuration

### Environment Variables

| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `GEMINI_API_KEY` | Yes | - | Google Gemini API key for AI agents |
| `OPENWEATHER_API_KEY` | No | - | OpenWeatherMap API key for weather data |
| `BACKEND_HOST` | No | `127.0.0.1` | Backend server host |
| `BACKEND_PORT` | No | `8000` | Backend server port |
| `STREAMLIT_SERVER_PORT` | No | `8501` | Streamlit frontend port |
| `LOG_LEVEL` | No | `INFO` | Logging level (DEBUG, INFO, WARNING, ERROR) |
| `ENABLE_MOCK_DATA` | No | `false` | Force mock data mode |
| `ENABLE_DETAILED_LOGGING` | No | `false` | Enable detailed logging |

---

## 🧪 Testing

```bash
# Run all tests
pytest tests/

# Run specific test file
pytest tests/test_agents_tools.py

# Run with coverage
pytest tests/ --cov=agents --cov=tools --cov=workflows
```

---

## 📖 Documentation

- [Getting Started Guide](GETTING_STARTED.md) - Detailed setup and configuration
- [API Documentation](docs/API_DOCUMENTATION.md) - Complete API reference
- [Deployment Guide](docs/DEPLOYMENT_GUIDE.md) - Production deployment instructions
- [Architecture Documentation](docs/architecture.md) - System architecture details
- [Implementation Summary](IMPLEMENTATION_SUMMARY.md) - Technical implementation details

---

## 🤝 Contributing

Contributions are welcome! Please follow these guidelines:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Development Guidelines

- Follow PEP 8 style guidelines
- Add tests for new features
- Update documentation as needed
- Ensure all tests pass before submitting

---

## 🐛 Troubleshooting

### Common Issues

**Backend won't start**
- Check if port 8000 is already in use
- Verify Python version is 3.10+
- Ensure all dependencies are installed
- Check API keys in `.env` file

**Frontend can't connect to backend**
- Verify backend is running on correct port
- Check `BACKEND_URL` in `.env` matches backend address
- Ensure firewall isn't blocking the connection

**API errors**
- Verify API keys are valid and not expired
- Check internet connection for external API calls
- Review logs in `logs/crisisguardian.log`

**Import errors**
- Ensure virtual environment is activated
- Reinstall dependencies: `pip install -r requirements.txt`
- Check Python path configuration

---

## 🗺️ Roadmap

### Upcoming Features

- [ ] Real-time WebSocket updates for live alerts
- [ ] Mobile-responsive design improvements
- [ ] Additional disaster types (tsunami, landslide, etc.)
- [ ] Multi-language support
- [ ] Voice input and output capabilities
- [ ] Integration with more emergency services APIs
- [ ] User authentication and personalization
- [ ] Historical disaster data and analytics
- [ ] Mobile app (React Native)
- [ ] Advanced ML models for prediction

---

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- Google for Gemini 2.5 Flash API
- LangChain team for the excellent framework
- OpenWeatherMap for weather data
- OpenStreetMap for geocoding services
- The open-source community for amazing tools and libraries

---

## 📞 Support

For issues, questions, or contributions:
- Open an issue on GitHub
- Contact: [your-email@example.com]
- Documentation: [Full Documentation Link]

---

## ⚠️ Disclaimer

**CrisisGuardian AI is designed to assist during emergencies but should not replace official emergency services.** Always follow instructions from local authorities and emergency responders. In life-threatening situations, contact emergency services immediately (112, 911, or your local emergency number).

---

**Built with ❤️ for emergency preparedness and disaster response**
