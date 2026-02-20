# Trend Analyzer Platform

AI-powered trend analysis platform with multi-agent system, web scraping, and comprehensive insights generation.

## Overview

This platform analyzes trends across multiple dimensions (region, domain, audience, demographics) using:
- **Web Scraping**: TikTok Creative Center, Google Trends
- **Multi-Agent AI**: 5 specialized agents for analysis, insights, and brief generation
- **Modern Stack**: Next.js frontend, FastAPI backend, PostgreSQL database
- **Full DevOps**: Docker, Kubernetes, GitHub Actions, ArgoCD

## Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                     Frontend (Next.js)                       │
│  - Multi-field filter form                                   │
│  - Real-time analysis results                                │
│  - AI-generated insights & briefs                            │
└────────────────────┬────────────────────────────────────────┘
                     │
                     ▼
┌─────────────────────────────────────────────────────────────┐
│                    Backend (FastAPI)                         │
│                                                               │
│  ┌──────────────┐  ┌───────────────┐  ┌─────────────────┐  │
│  │ Web Scrapers │  │  Multi-Agent  │  │ Trend Analysis  │  │
│  │  - TikTok    │─▶│   AI System   │─▶│   & Insights    │  │
│  │  - Google    │  │  (5 agents)   │  │   Generation    │  │
│  └──────────────┘  └───────────────┘  └─────────────────┘  │
└────────────────────┬────────────────────────────────────────┘
                     │
          ┌──────────┴──────────┐
          ▼                     ▼
    ┌──────────┐         ┌──────────┐
    │PostgreSQL│         │  Redis   │
    │ Database │         │  Cache   │
    └──────────┘         └──────────┘
```

## Project Structure

```
TikTok analysis/
├── trend-analyzer-backend/      # FastAPI backend
│   ├── app/
│   │   ├── agents/              # Multi-agent AI system
│   │   ├── scrapers/            # Web scraping modules
│   │   ├── api/                 # REST API endpoints
│   │   ├── models/              # Database models
│   │   └── schemas/             # Pydantic schemas
│   ├── Dockerfile
│   └── requirements.txt
│
├── trend-analyzer-frontend/     # Next.js frontend
│   ├── src/
│   │   ├── app/                 # Next.js App Router
│   │   ├── components/          # React components
│   │   ├── services/            # API clients
│   │   └── types/               # TypeScript types
│   ├── Dockerfile
│   └── package.json
│
├── trend-analyzer-infra/        # Infrastructure as Code
│   ├── k8s/                     # Kubernetes manifests
│   │   └── base/
│   ├── argocd/                  # ArgoCD configuration
│   └── README.md
│
├── docker-compose.yaml          # Local development
└── README.md                    # This file
```

## Features

### Core Functionality
- ✅ Multi-dimensional trend filtering (region, domain, audience, demographics)
- ✅ Real-time web scraping (TikTok Creative Center, Google Trends)
- ✅ Multi-agent AI analysis system (5 specialized agents)
- ✅ AI-generated insights and recommendations
- ✅ Comprehensive content brief generation
- ✅ Downloadable reports

### Technical Features
- ✅ RESTful API with OpenAPI documentation
- ✅ Async/await architecture
- ✅ Docker containerization
- ✅ Kubernetes deployment
- ✅ CI/CD with GitHub Actions
- ✅ GitOps with ArgoCD
- ✅ Horizontal pod autoscaling
- ✅ Health checks and monitoring

## Quick Start

### Prerequisites
- **VS Code** (recommended IDE)
- **Docker & Docker Compose** (for running the application)
- **Node.js 20+** (for local development)
- **Python 3.11+** (for local development)
- **Kubernetes cluster** (for production deployment only)
- **OpenAI API key** (required for AI features)

### Step 1: Open the Project Workspace

This project uses a **VS Code multi-root workspace** for better organization.

#### Understanding the Workspace

The workspace shows 4 folders in VS Code:
- **🎯 Root** - Parent folder with docker-compose and docs
- **🐍 Backend (FastAPI)** - Points to `trend-analyzer-backend/` folder
- **⚛️ Frontend (Next.js)** - Points to `trend-analyzer-frontend/` folder  
- **☸️ Infrastructure (K8s)** - Points to `trend-analyzer-infra/` folder

**IMPORTANT**: "Backend (FastAPI)" and "trend-analyzer-backend" are the SAME folder - just different display names!

#### Opening the Workspace

**Option A: From Terminal**
```bash
cd "/Users/dhmnguyen/Documents/TikTok analysis"
code trend-analyzer.code-workspace
```

**Option B: From VS Code**
1. Open VS Code
2. Go to **File → Open Workspace from File...**
3. Navigate to `/Users/dhmnguyen/Documents/TikTok analysis/`
4. Select `trend-analyzer.code-workspace`
5. Click **Open**

#### First-Time Setup

After opening the workspace, VS Code will prompt you to install recommended extensions:
- **Python** - Python language support
- **Pylance** - Python type checking
- **Ruff** - Python linting/formatting
- **ESLint** - JavaScript/TypeScript linting
- **Prettier** - Code formatting
- **Docker** - Docker support
- **Kubernetes** - K8s support

Click **Install All** to get the full development experience.

### Step 2: Run the Project

You have two options for running the project:

#### Option A: Using Docker Compose (Recommended - Easiest)

This runs everything with one command - no manual setup needed!

1. **Create environment file**
```bash
# From the workspace root (🎯 Root folder)
cat > .env << EOF
OPENAI_API_KEY=your-openai-api-key-here
ANTHROPIC_API_KEY=your-anthropic-api-key-here
EOF
```

2. **Start all services**
```bash
docker-compose up -d
```

This will start:
- Frontend (Next.js) on port 3000
- Backend (FastAPI) on port 8000
- PostgreSQL database on port 5432
- Redis cache on port 6379

3. **Access the application**
- **Frontend UI**: http://localhost:3000
- **Backend API**: http://localhost:8000
- **API Documentation**: http://localhost:8000/api/docs
- **API Redoc**: http://localhost:8000/api/redoc

4. **View logs**
```bash
# All services
docker-compose logs -f

# Specific service
docker-compose logs -f backend
docker-compose logs -f frontend
```

5. **Stop services**
```bash
docker-compose down
```

#### Option B: Local Development (Manual Setup)

Use this if you want to develop and debug code directly.

**Backend Setup:**
```bash
# Open terminal in 🐍 Backend (FastAPI) folder
cd trend-analyzer-backend

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On macOS/Linux
# OR
venv\Scripts\activate     # On Windows

# Install dependencies
pip install -r requirements.txt

# Install Playwright browsers
playwright install chromium

# Start database services
docker run -d -p 5432:5432 \
  -e POSTGRES_PASSWORD=postgres \
  -e POSTGRES_DB=trend_analyzer \
  --name trend-analyzer-postgres \
  postgres:15

docker run -d -p 6379:6379 \
  --name trend-analyzer-redis \
  redis:7-alpine

# Create .env file
cp .env.example .env
# Edit .env and add your OPENAI_API_KEY

# Run the backend
uvicorn app.main:app --reload
```

Backend will be available at http://localhost:8000

**Frontend Setup:**
```bash
# Open new terminal in ⚛️ Frontend (Next.js) folder
cd trend-analyzer-frontend

# Install dependencies
npm install

# Create environment file
cp .env.local.example .env.local
# Edit .env.local if needed (default API URL is http://localhost:8000)

# Run the frontend
npm run dev
```

Frontend will be available at http://localhost:3000

### Local Development (Without Docker)

**Backend:**
```bash
cd trend-analyzer-backend
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
playwright install chromium

# Start PostgreSQL and Redis (via Docker)
docker run -d -p 5432:5432 -e POSTGRES_PASSWORD=postgres -e POSTGRES_DB=trend_analyzer postgres:15
docker run -d -p 6379:6379 redis:7-alpine

# Copy and edit .env
cp .env.example .env

# Run the API
uvicorn app.main:app --reload
```

**Frontend:**
```bash
cd trend-analyzer-frontend
npm install
cp .env.local.example .env.local
npm run dev
```

### Step 3: Verify Everything Works

1. **Open Frontend**: http://localhost:3000
2. **Fill out the trend filter form**:
   - Region: Select any region (e.g., "US")
   - Domain: Select a domain (e.g., "Dance")
   - Time Range: Select a timeframe (e.g., "7 days")
3. **Click "Analyze Trends"**
4. **Wait for results** (may take 30-60 seconds)
5. **Review AI-generated insights, recommendations, and brief**

### Where to Write Code

When developing in VS Code:

| VS Code Folder | Actual Folder | What to Code Here |
|---------------|---------------|-------------------|
| 🎯 Root | `.` (current directory) | docker-compose.yaml, documentation |
| 🐍 Backend (FastAPI) | `trend-analyzer-backend/` | Python code, API endpoints, agents, scrapers |
| ⚛️ Frontend (Next.js) | `trend-analyzer-frontend/` | React components, TypeScript, UI |
| ☸️ Infrastructure (K8s) | `trend-analyzer-infra/` | Kubernetes manifests, GitOps config |

**Remember**: "Backend (FastAPI)" in VS Code = `trend-analyzer-backend/` folder on disk (same location!)

## Usage

### 1. Select Filters

Fill in the trend filter form:
- **Region** (required): US, Vietnam, Global, etc.
- **Domain** (required): Dance, Food, Gaming, Fashion, etc.
- **Audience Target** (optional): Gen Z, Millennials, age ranges
- **Time Range**: 24h, 7d, 30d, 90d
- **Sexual Orientation** (optional): Note limited data availability
- **Religion** (optional): Note limited data availability

### 2. Analyze Trends

Click "Analyze Trends" to:
1. Scrape fresh trend data from multiple sources
2. Run multi-agent AI analysis
3. Generate insights and recommendations
4. Create comprehensive brief

### 3. Review Results

Get:
- **Key Insights**: Actionable insights with confidence scores
- **Recommendations**: Prioritized action items with expected impact
- **Content Brief**: Comprehensive brief with strategy and action plan
- **Download**: Export brief as text file

## Multi-Agent System

The platform uses 5 specialized AI agents:

1. **Filter Agent**: Ranks and filters trends by relevance
2. **Analysis Agent**: Performs deep trend analysis using LLM
3. **Insight Agent**: Extracts actionable insights
4. **Recommendation Agent**: Generates specific recommendations
5. **Brief Agent**: Creates comprehensive content brief

Each agent processes the output of the previous one, building a complete analysis pipeline.

## API Endpoints

### Trends
- `POST /api/trends/scrape` - Scrape new trends
- `GET /api/trends/search` - Search existing trends
- `GET /api/trends/{id}` - Get specific trend

### Analysis
- `POST /api/analysis/analyze` - Full trend analysis (scrape + AI)
- `POST /api/analysis/brief` - Quick brief generation
- `GET /api/analysis/{id}` - Retrieve previous analysis

### Health
- `GET /api/health` - Health check
- `GET /api/ready` - Readiness check

Full API documentation: http://localhost:8000/api/docs

## Deployment

### Kubernetes

See [trend-analyzer-infra/README.md](trend-analyzer-infra/README.md) for detailed deployment instructions.

Quick deploy:
```bash
cd trend-analyzer-infra
kubectl apply -f k8s/base/
```

### ArgoCD (GitOps)

```bash
kubectl apply -f trend-analyzer-infra/argocd/project.yaml
kubectl apply -f trend-analyzer-infra/argocd/application.yaml
```

## CI/CD Pipeline

1. **Push Code** → GitHub
2. **GitHub Actions** → Build & Test
3. **Build Docker Image** → Push to Registry
4. **ArgoCD** → Detect Changes
5. **Auto Sync** → Deploy to Kubernetes

## Configuration

### Backend Environment Variables

See `trend-analyzer-backend/.env.example`:
- `OPENAI_API_KEY`: OpenAI API key (required)
- `ANTHROPIC_API_KEY`: Anthropic API key (optional)
- `DATABASE_URL`: PostgreSQL connection string
- `REDIS_URL`: Redis connection string
- `AGENT_MODEL`: LLM model for agents (default: gpt-4-turbo-preview)

### Frontend Environment Variables

See `trend-analyzer-frontend/.env.local.example`:
- `NEXT_PUBLIC_API_URL`: Backend API URL

## Development

### Adding a New Scraper

1. Create scraper in `trend-analyzer-backend/app/scrapers/`
2. Inherit from `BaseScraper`
3. Implement `scrape()` method
4. Add to `ScraperOrchestrator`

### Adding a New Agent

1. Add agent method in `TrendAnalysisAgents` class
2. Update workflow graph in `_build_graph()`
3. Define agent's input/output in `AgentState`

### Modifying Filters

1. Update `TrendFilters` schema in `app/schemas/trend.py`
2. Update form in `src/components/TrendFilterForm.tsx`
3. Update database model if persisting

## Monitoring

```bash
# Check pod status
kubectl get pods -n trend-analyzer

# View logs
kubectl logs -f deployment/backend -n trend-analyzer

# Check metrics
kubectl top pods -n trend-analyzer
```

## Troubleshooting

### VS Code and Workspace Issues

**Q: I see "Backend (FastAPI)" and "trend-analyzer-backend" - which one is real?**
- They are THE SAME folder! "Backend (FastAPI)" is just a display name in VS Code
- Write your code in either - they point to the same `trend-analyzer-backend/` folder

**Q: LSP errors showing "Import could not be resolved"**
- This is normal before installing dependencies
- Fix: Install Python dependencies in virtual environment
```bash
cd trend-analyzer-backend
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

**Q: Workspace not opening correctly**
- Make sure you open `trend-analyzer.code-workspace` file, not the folder
- Go to File → Open Workspace from File → Select `trend-analyzer.code-workspace`

### Docker Issues

**Q: "Port already in use" error**
```bash
# Find what's using the port
lsof -i :3000  # or :8000, :5432, :6379

# Stop conflicting containers
docker stop $(docker ps -q)

# Or change port in docker-compose.yaml
```

**Q: Database connection failed**
```bash
# Check if PostgreSQL container is running
docker ps | grep postgres

# Restart PostgreSQL
docker-compose restart postgres

# Check logs
docker-compose logs postgres
```

### Web Scraping Issues
- TikTok Creative Center may change HTML structure
- Google Trends API limits may apply
- Check scraper logs for details
```bash
docker-compose logs backend | grep scraper
```

### AI Analysis Fails
- Verify API keys are set correctly in `.env`
- Check rate limits on OpenAI/Anthropic
- Review agent logs for specific errors
```bash
docker-compose logs backend | grep agent
```

### Performance Issues

**Q: Analysis taking too long**
- First run installs Playwright browsers (1-2 minutes)
- Subsequent runs should take 30-60 seconds
- Check your internet connection for web scraping

**Q: High memory usage**
- Playwright browsers can use 500MB-1GB RAM
- Close unused containers: `docker-compose stop <service-name>`

### Database Connection
```bash
# Test PostgreSQL connection
docker exec -it trend-analyzer-postgres psql -U postgres -d trend_analyzer

# View all tables
\dt

# Exit
\q
```

### Getting Help

If you're still stuck:
1. Check service logs: `docker-compose logs -f <service-name>`
2. Verify environment variables in `.env` file
3. Make sure all prerequisites are installed
4. Try restarting: `docker-compose down && docker-compose up -d`

## Contributing

1. Fork the repository
2. Create feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open Pull Request

## License

MIT License - feel free to use this project for your own purposes.

## Support

For issues, questions, or contributions:
- Open an issue on GitHub
- Check existing documentation
- Review API docs at `/api/docs`

## Roadmap

- [ ] Additional scrapers (Twitter/X, Instagram, YouTube)
- [ ] Advanced demographic filtering with more data sources
- [ ] Trend forecasting with ML models
- [ ] Competitor analysis
- [ ] Content calendar generation
- [ ] Multi-language support
- [ ] MCP server for trend data access
- [ ] Real-time trend monitoring webhooks
- [ ] Export to multiple formats (PDF, CSV, JSON)

---

Built with ❤️ using Next.js, FastAPI, and AI
