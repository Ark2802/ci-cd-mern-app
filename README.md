# CI/CD Pipeline for MERN Backend Application

[![CI/CD Pipeline](https://github.com/YOUR_USERNAME/ci-cd-mern-app/actions/workflows/ci-cd.yml/badge.svg)](https://github.com/YOUR_USERNAME/ci-cd-mern-app/actions/workflows/ci-cd.yml)

A production-ready Express.js backend application with automated CI/CD pipeline using GitHub Actions and Docker Hub.

## 🚀 Features

- **Express.js Backend**: Minimal REST API with multiple endpoints
- **Automated Testing**: Jest test suite with coverage reports
- **Docker Support**: Fully containerized application
- **CI/CD Pipeline**: Automated build, test, and deployment
- **Security**: Non-root user in Docker, environment variables
- **Health Checks**: Built-in health monitoring endpoint

## 📋 Prerequisites

- Node.js 18 or higher
- Docker Desktop
- GitHub account
- Docker Hub account

## 🛠️ Installation & Setup

### 1. Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/ci-cd-mern-app.git
cd ci-cd-mern-app
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Configure Environment

Create a `.env` file in the root directory:

```env
PORT=5000
NODE_ENV=development
```

### 4. Run Locally

```bash
# Development mode with auto-reload
npm run dev

# Production mode
npm start
```

The server will start on `http://localhost:5000`

## 🧪 Testing

Run the test suite:

```bash
npm test
```

This will run all tests and generate a coverage report.

## 🐳 Docker Usage

### Build Docker Image Locally

```bash
docker build -t ci-cd-mern-backend .
```

### Run Docker Container

```bash
docker run -p 5000:5000 ci-cd-mern-backend
```

### Test the Container

```bash
# Health check
curl http://localhost:5000/api/health

# Get users
curl http://localhost:5000/api/users
```

## 📡 API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/` | Welcome message and API info |
| GET | `/api/health` | Health check endpoint |
| GET | `/api/users` | Get list of users |
| GET | `/api/status` | Server status information |

### Example Responses

#### GET /
```json
{
  "message": "Welcome to CI/CD MERN Backend API",
  "version": "1.0.0",
  "status": "active"
}
```

#### GET /api/health
```json
{
  "status": "healthy",
  "timestamp": "2025-10-20T10:30:00.000Z",
  "uptime": 123.456
}
```

#### GET /api/users
```json
{
  "success": true,
  "count": 3,
  "data": [
    {
      "id": 1,
      "name": "John Doe",
      "email": "john@example.com"
    }
  ]
}
```

## 🔄 CI/CD Pipeline Setup

### Step 1: Create Docker Hub Account

1. Go to [Docker Hub](https://hub.docker.com/)
2. Sign up or log in
3. Create an access token:
   - Go to Account Settings → Security → Access Tokens
   - Click "New Access Token"
   - Give it a name (e.g., "github-actions")
   - Copy the token (you won't see it again!)

### Step 2: Configure GitHub Secrets

1. Go to your GitHub repository
2. Navigate to Settings → Secrets and variables → Actions
3. Click "New repository secret"
4. Add the following secrets:

   - **DOCKER_USERNAME**: Your Docker Hub username
   - **DOCKER_PASSWORD**: Your Docker Hub access token

### Step 3: Push to GitHub

```bash
# Initialize git (if not already done)
git init

# Add all files
git add .

# Commit changes
git commit -m "Initial commit: CI/CD MERN backend"

# Add remote repository
git remote add origin https://github.com/YOUR_USERNAME/ci-cd-mern-app.git

# Create and push to main branch
git branch -M main
git push -u origin main
```

### Step 4: Verify Pipeline Execution

1. Go to your GitHub repository
2. Click on "Actions" tab
3. You should see the workflow running
4. Wait for all steps to complete (green checkmarks)

### Step 5: Verify Docker Hub

1. Go to [Docker Hub](https://hub.docker.com/)
2. Check your repositories
3. You should see `ci-cd-mern-backend` with the latest image

## 🎯 Pipeline Workflow

The CI/CD pipeline automatically executes on every push to the `main` branch:

1. **Checkout Code**: Retrieves the latest code from the repository
2. **Setup Node.js**: Configures Node.js 18 environment
3. **Install Dependencies**: Installs all required packages
4. **Run Tests**: Executes Jest test suite
   - ⚠️ If tests fail, the pipeline stops here
5. **Setup Docker Buildx**: Prepares Docker build environment
6. **Login to Docker Hub**: Authenticates with Docker Hub
7. **Build Docker Image**: Creates optimized production image
8. **Push to Docker Hub**: Uploads image with tags

## 🔍 Testing the Deployed Image

Pull and run the image from Docker Hub:

```bash
# Pull the image
docker pull YOUR_DOCKERHUB_USERNAME/ci-cd-mern-backend:latest

# Run the container
docker run -d -p 5000:5000 --name mern-backend YOUR_DOCKERHUB_USERNAME/ci-cd-mern-backend:latest

# Test the endpoints
curl http://localhost:5000/
curl http://localhost:5000/api/health
curl http://localhost:5000/api/users

# View logs
docker logs mern-backend

# Stop and remove container
docker stop mern-backend
docker rm mern-backend
```

## 📁 Project Structure

```
ci-cd-mern-app/
├── .github/
│   └── workflows/
│       └── ci-cd.yml          # GitHub Actions workflow
├── .dockerignore              # Docker ignore file
├── .env                       # Environment variables
├── .gitignore                 # Git ignore file
├── Dockerfile                 # Docker configuration
├── jest.config.js             # Jest configuration
├── package.json               # Node.js dependencies
├── server.js                  # Express application
├── server.test.js             # Test suite
└── README.md                  # Documentation
```

## 🔒 Security Features

- **Non-root User**: Docker container runs as unprivileged user
- **Environment Variables**: Sensitive data in .env (not committed)
- **Docker Hub Secrets**: Credentials stored securely in GitHub
- **Health Checks**: Automatic container health monitoring
- **Production Dependencies**: Only necessary packages in container

## 🐛 Troubleshooting

### Tests Failing in CI/CD

- Check test logs in GitHub Actions
- Ensure all tests pass locally first: `npm test`
- Verify Node.js version matches (18)

### Docker Build Failing

- Test Docker build locally: `docker build -t test .`
- Check Dockerfile syntax
- Verify .dockerignore is correct

### Docker Hub Push Failing

- Verify DOCKER_USERNAME and DOCKER_PASSWORD secrets
- Check Docker Hub access token is valid
- Ensure repository name matches workflow

### Container Not Starting

- Check logs: `docker logs CONTAINER_ID`
- Verify port 5000 is available
- Check environment variables

## 📊 Monitoring

The application includes a health check endpoint that can be monitored:

```bash
# Manual health check
curl http://localhost:5000/api/health

# Docker health status
docker ps
```

## 🚢 Deployment

The Docker image can be deployed to various platforms:

- **AWS ECS/EKS**: Elastic Container Service or Kubernetes
- **Azure Container Instances**: Serverless containers
- **Google Cloud Run**: Fully managed serverless platform
- **Heroku**: Container Registry
- **DigitalOcean**: App Platform or Kubernetes

## 📝 License

ISC

## 👨‍💻 Author

Your Name

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature-name`
3. Commit changes: `git commit -am 'Add feature'`
4. Push to branch: `git push origin feature-name`
5. Submit a pull request

## 📧 Support

For issues and questions, please open an issue on GitHub.

---

## 📸 Screenshots

### Successful GitHub Actions Workflow
![GitHub Actions Success](screenshots/github-actions-success.png)

### Docker Hub Repository
![Docker Hub](screenshots/docker-hub-repository.png)

---

**Note**: Remember to replace `YOUR_USERNAME` and `YOUR_DOCKERHUB_USERNAME` with your actual GitHub and Docker Hub usernames throughout this document.
