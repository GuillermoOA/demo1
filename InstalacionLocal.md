# Complete Installation Guide for RAG Knowledge Hub on macOS

This guide will help you install and run the RAG Knowledge Hub application on your macOS computer.

## Prerequisites

### System Requirements
- macOS 10.14 (Mojave) or later
- At least 4GB RAM
- 2GB free disk space
- Internet connection

### Required Accounts
- **Pinecone Account**: Sign up at [pinecone.io](https://pinecone.io) for vector database
- **Emergent LLM Key**: Or OpenAI API key for LLM functionality

## Step 1: Install System Dependencies

### Install Homebrew (if not already installed)
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### Install Python 3.11+
```bash
brew install python@3.11
```

### Install Node.js and npm
```bash
brew install node
```

### Install MongoDB
```bash
# Install MongoDB Community Edition
brew tap mongodb/brew
brew install mongodb-community

# Start MongoDB service
brew services start mongodb/brew/mongodb-community
```

### Install Git (if not already installed)
```bash
brew install git
```

## Step 2: Clone and Setup the Project

### Create project directory
```bash
mkdir ~/rag-knowledge-hub
cd ~/rag-knowledge-hub
```

### Download the application files
Since this is a custom application, you'll need to create the project structure manually. Let me provide you with the complete setup:

```bash
# Create directory structure
mkdir -p backend frontend/src/components/ui frontend/public
```

## Step 3: Backend Setup

### Create backend files
```bash
cd ~/rag-knowledge-hub/backend
```

Create `requirements.txt`:
```txt
fastapi==0.110.1
uvicorn==0.25.0
boto3>=1.34.129
requests-oauthlib>=2.0.0
cryptography>=42.0.8
python-dotenv>=1.0.1
pymongo==4.5.0
pydantic>=2.6.4
email-validator>=2.2.0
pyjwt>=2.10.1
passlib>=1.7.4
tzdata>=2024.2
motor==3.3.1
pytest>=8.0.0
black>=24.1.1
isort>=5.13.2
flake8>=7.0.0
mypy>=1.8.0
python-jose>=3.3.0
requests>=2.31.0
pandas>=2.2.0
numpy>=1.26.0
python-multipart>=0.0.9
jq>=1.6.0
typer>=0.9.0
emergentintegrations
pinecone
pypdf
python-docx
openpyxl
pyotp
qrcode
bcrypt
```

### Install Python dependencies
```bash
# Create virtual environment
python3.11 -m venv venv
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# For emergentintegrations (if you have access)
pip install emergentintegrations --extra-index-url https://d33sy5i8bnduwe.cloudfront.net/simple/
```

### Create environment file
Create `.env` file:
```bash
MONGO_URL="mongodb://localhost:27017"
DB_NAME="rag_system_db"
CORS_ORIGINS="*"

# Pinecone Configuration (Replace with your credentials)
PINECONE_API_KEY="your-pinecone-api-key"
PINECONE_ENVIRONMENT="your-pinecone-region"
PINECONE_GENERAL_INDEX="rag-general-knowledge"
PINECONE_USER_INDEX="rag-user-knowledge"

# LLM Configuration
EMERGENT_LLM_KEY="your-emergent-llm-key"
# OR use OpenAI API key
OPENAI_API_KEY="your-openai-api-key"

# JWT Secret
JWT_SECRET_KEY="your-super-secret-jwt-key-change-this-in-production"
JWT_ALGORITHM="HS256"
JWT_ACCESS_TOKEN_EXPIRE_MINUTES="30"
```

## Step 4: Frontend Setup

```bash
cd ~/rag-knowledge-hub/frontend
```

Create `package.json`:
```json
{
  "name": "rag-frontend",
  "version": "0.1.0",
  "private": true,
  "dependencies": {
    "@hookform/resolvers": "^5.0.1",
    "@radix-ui/react-accordion": "^1.2.8",
    "@radix-ui/react-alert-dialog": "^1.1.11",
    "@radix-ui/react-aspect-ratio": "^1.1.4",
    "@radix-ui/react-avatar": "^1.1.7",
    "@radix-ui/react-checkbox": "^1.2.3",
    "@radix-ui/react-collapsible": "^1.1.8",
    "@radix-ui/react-context-menu": "^2.2.12",
    "@radix-ui/react-dialog": "^1.1.11",
    "@radix-ui/react-dropdown-menu": "^2.1.12",
    "@radix-ui/react-hover-card": "^1.1.11",
    "@radix-ui/react-label": "^2.1.4",
    "@radix-ui/react-menubar": "^1.1.12",
    "@radix-ui/react-navigation-menu": "^1.2.10",
    "@radix-ui/react-popover": "^1.1.11",
    "@radix-ui/react-progress": "^1.1.4",
    "@radix-ui/react-radio-group": "^1.3.4",
    "@radix-ui/react-scroll-area": "^1.2.6",
    "@radix-ui/react-select": "^2.2.2",
    "@radix-ui/react-separator": "^1.1.4",
    "@radix-ui/react-slider": "^1.3.2",
    "@radix-ui/react-slot": "^1.2.0",
    "@radix-ui/react-switch": "^1.2.2",
    "@radix-ui/react-tabs": "^1.1.9",
    "@radix-ui/react-toast": "^1.2.11",
    "@radix-ui/react-toggle": "^1.1.6",
    "@radix-ui/react-toggle-group": "^1.1.7",
    "@radix-ui/react-tooltip": "^1.2.4",
    "axios": "^1.8.4",
    "class-variance-authority": "^0.7.1",
    "clsx": "^2.1.1",
    "cmdk": "^1.1.1",
    "date-fns": "^4.1.0",
    "embla-carousel-react": "^8.6.0",
    "input-otp": "^1.4.2",
    "lucide-react": "^0.507.0",
    "next-themes": "^0.4.6",
    "react": "^19.0.0",
    "react-day-picker": "8.10.1",
    "react-dom": "^19.0.0",
    "react-hook-form": "^7.56.2",
    "react-resizable-panels": "^3.0.1",
    "react-router-dom": "^7.5.1",
    "react-scripts": "5.0.1",
    "sonner": "^2.0.3",
    "tailwind-merge": "^3.2.0",
    "tailwindcss-animate": "^1.0.7",
    "vaul": "^1.1.2",
    "zod": "^3.24.4"
  },
  "scripts": {
    "start": "craco start",
    "build": "craco build",
    "test": "craco test"
  },
  "browserslist": {
    "production": [
      ">0.2%",
      "not dead",
      "not op_mini all"
    ],
    "development": [
      "last 1 chrome version",
      "last 1 firefox version",
      "last 1 safari version"
    ]
  },
  "devDependencies": {
    "@craco/craco": "^7.1.0",
    "@eslint/js": "9.23.0",
    "autoprefixer": "^10.4.20",
    "eslint": "9.23.0",
    "eslint-plugin-import": "2.31.0",
    "eslint-plugin-jsx-a11y": "6.10.2",
    "eslint-plugin-react": "7.37.4",
    "globals": "15.15.0",
    "postcss": "^8.4.49",
    "tailwindcss": "^3.4.17"
  }
}
```

### Install frontend dependencies
```bash
npm install
```

### Create frontend environment file
Create `.env` in the frontend directory:
```bash
REACT_APP_BACKEND_URL=http://localhost:8001
```

### Setup Tailwind CSS
Create `tailwind.config.js`:
```javascript
module.exports = {
  darkMode: ["class"],
  content: [
    './pages/**/*.{js,jsx}',
    './components/**/*.{js,jsx}',
    './app/**/*.{js,jsx}',
    './src/**/*.{js,jsx}',
  ],
  prefix: "",
  theme: {
    container: {
      center: true,
      padding: "2rem",
      screens: {
        "2xl": "1400px",
      },
    },
    extend: {
      colors: {
        border: "hsl(var(--border))",
        input: "hsl(var(--input))",
        ring: "hsl(var(--ring))",
        background: "hsl(var(--background))",
        foreground: "hsl(var(--foreground))",
        primary: {
          DEFAULT: "hsl(var(--primary))",
          foreground: "hsl(var(--primary-foreground))",
        },
        secondary: {
          DEFAULT: "hsl(var(--secondary))",
          foreground: "hsl(var(--secondary-foreground))",
        },
        destructive: {
          DEFAULT: "hsl(var(--destructive))",
          foreground: "hsl(var(--destructive-foreground))",
        },
        muted: {
          DEFAULT: "hsl(var(--muted))",
          foreground: "hsl(var(--muted-foreground))",
        },
        accent: {
          DEFAULT: "hsl(var(--accent))",
          foreground: "hsl(var(--accent-foreground))",
        },
        popover: {
          DEFAULT: "hsl(var(--popover))",
          foreground: "hsl(var(--popover-foreground))",
        },
        card: {
          DEFAULT: "hsl(var(--card))",
          foreground: "hsl(var(--card-foreground))",
        },
      },
      borderRadius: {
        lg: "var(--radius)",
        md: "calc(var(--radius) - 2px)",
        sm: "calc(var(--radius) - 4px)",
      },
      keyframes: {
        "accordion-down": {
          from: { height: "0" },
          to: { height: "var(--radix-accordion-content-height)" },
        },
        "accordion-up": {
          from: { height: "var(--radix-accordion-content-height)" },
          to: { height: "0" },
        },
      },
      animation: {
        "accordion-down": "accordion-down 0.2s ease-out",
        "accordion-up": "accordion-up 0.2s ease-out",
      },
    },
  },
  plugins: [require("tailwindcss-animate")],
}
```

Create `postcss.config.js`:
```javascript
module.exports = {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  },
}
```

Create `craco.config.js`:
```javascript
module.exports = {
  style: {
    postcss: {
      plugins: [
        require('tailwindcss'),
        require('autoprefixer'),
      ],
    },
  },
}
```

## Step 5: Get API Keys and Credentials

### Pinecone Setup
1. Go to [app.pinecone.io](https://app.pinecone.io)
2. Create a new project
3. Get your API key from the "API Keys" section
4. Note your environment/region (e.g., `us-east-1`)

### Emergent LLM Key (or OpenAI)
- If you have access to Emergent integrations, use that key
- Otherwise, get an OpenAI API key from [platform.openai.com](https://platform.openai.com)

## Step 6: Run the Application

### Terminal 1: Start MongoDB (if not running as service)
```bash
mongod --config /opt/homebrew/etc/mongod.conf
```

### Terminal 2: Start Backend
```bash
cd ~/rag-knowledge-hub/backend
source venv/bin/activate
uvicorn server:app --host 0.0.0.0 --port 8001 --reload
```

### Terminal 3: Start Frontend
```bash
cd ~/rag-knowledge-hub/frontend
npm start
```

## Step 7: Access the Application

Open your browser and navigate to:
- **Frontend**: http://localhost:3000
- **Backend API**: http://localhost:8001/docs (FastAPI documentation)

## Step 8: Initial Setup

1. **Register a user account** through the frontend
2. **Upload some documents** to test the RAG functionality
3. **Test the chat interface** with questions about your documents
4. **Set up 2FA** in the admin section (optional)
5. **Create system prompts** to customize the AI assistant

## Troubleshooting

### Common Issues

**MongoDB Connection Error:**
```bash
# Check if MongoDB is running
brew services list | grep mongodb

# Restart MongoDB if needed
brew services restart mongodb/brew/mongodb-community
```

**Port Already in Use:**
```bash
# Kill process on port 8001
lsof -ti:8001 | xargs kill -9

# Kill process on port 3000
lsof -ti:3000 | xargs kill -9
```

**Python Dependencies Error:**
```bash
# Update pip
pip install --upgrade pip

# Reinstall requirements
pip install -r requirements.txt --force-reinstall
```

**Node Dependencies Error:**
```bash
# Clear npm cache
npm cache clean --force

# Delete node_modules and reinstall
rm -rf node_modules package-lock.json
npm install
```

### Performance Optimization

**For better performance:**
1. Use a proper embedding service instead of hash-based embeddings
2. Configure MongoDB with proper indexing
3. Set up Pinecone indexes with appropriate specifications
4. Use environment variables for all configuration

### Security Notes

- Change all default passwords and secret keys
- Use HTTPS in production
- Implement proper rate limiting
- Regularly update dependencies

## Widget Integration

To embed the chat widget on external websites:

```html
<!-- Bubble Widget -->
<iframe src="http://localhost:8001/api/widget/bubble/USER_EMAIL" 
        style="position: fixed; bottom: 0; right: 0; width: 400px; height: 600px; border: none; z-index: 9999;">
</iframe>

<!-- Iframe Widget -->
<iframe src="http://localhost:8001/api/widget/iframe/USER_EMAIL" 
        width="100%" height="600px" style="border: 1px solid #ccc; border-radius: 8px;">
</iframe>
```

## Next Steps

1. **Production Deployment**: Consider using Docker for containerization
2. **SSL/TLS**: Set up HTTPS certificates for production
3. **Database Backup**: Implement regular MongoDB backups
4. **Monitoring**: Add application monitoring and logging
5. **Scale**: Consider using cloud services for production deployment

The application should now be running successfully on your macOS system! 🎉