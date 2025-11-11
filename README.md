# Sample Project Starter - Codebase Structure Guide

## Overview

This is a full-stack application starter template designed with a modern architecture separating frontend and backend concerns. The project follows industry best practices with a clear separation between the client (React TypeScript) and server (Flask) layers.

## Project Architecture

```
sample-project-starter/
├── sample-backend/          # Flask Backend API
├── sample-client/           # React + TypeScript Frontend
└── doot/                    # Documentation folder
```

---

## 📁 Directory Structure

### Root Level

The project is organized as a monorepo-style structure with two main directories:

- **`sample-backend/`** - Backend API server (Flask)
- **`sample-client/`** - Frontend application (React + TypeScript + Vite)
- **`doot/`** - Documentation and guides

---

## 🎨 Frontend: `sample-client/`

### Technology Stack
- **Framework**: React 19.2.0
- **Language**: TypeScript 5.9.3
- **Build Tool**: Vite 7.2.2
- **Linting**: ESLint 9.39.1
- **Styling**: CSS Modules

### Directory Structure

```
sample-client/
├── public/                  # Static assets
│   └── vite.svg            # Vite logo
├── src/                     # Source code
│   ├── assets/             # Image and media assets
│   │   └── react.svg       # React logo
│   ├── App.tsx             # Root application component
│   ├── App.css             # Application styles
│   ├── main.tsx            # Application entry point
│   └── index.css           # Global styles
├── node_modules/           # Dependencies (gitignored)
├── eslint.config.js        # ESLint configuration
├── index.html              # HTML template
├── package.json            # Project dependencies & scripts
├── package-lock.json       # Locked dependency versions
├── tsconfig.json           # TypeScript base configuration
├── tsconfig.app.json       # TypeScript app configuration
├── tsconfig.node.json      # TypeScript Node.js configuration
├── vite.config.ts          # Vite build configuration
└── README.md               # Frontend documentation
```

### Key Files Explained

#### Configuration Files

| File | Purpose |
|------|---------|
| `vite.config.ts` | Vite bundler configuration, plugins, and build settings |
| `tsconfig.json` | Base TypeScript compiler options |
| `tsconfig.app.json` | TypeScript config specific to application code |
| `tsconfig.node.json` | TypeScript config for Node.js files (like config files) |
| `eslint.config.js` | Code quality and linting rules |
| `package.json` | Project metadata, dependencies, and npm scripts |

#### Source Code Structure

**`src/main.tsx`** - Application Entry Point
- Renders the root React component
- Imports global styles
- Mounts the app to the DOM

**`src/App.tsx`** - Root Component
- Main application component
- Contains routing logic (to be implemented)
- Manages global state (to be implemented)

**`src/App.css`** - Component Styles
- Styles specific to the App component
- Can be extended or replaced with CSS-in-JS solutions

**`src/index.css`** - Global Styles
- Application-wide styles
- CSS resets and variables
- Typography and base styles

### Available Scripts

```bash
# Development server with hot reload
npm run dev

# Production build with TypeScript compilation
npm run build

# Lint code for quality issues
npm run lint

# Preview production build locally
npm run preview
```

### Dependencies Overview

#### Production Dependencies
- `react` (^19.2.0) - Core React library
- `react-dom` (^19.2.0) - React DOM rendering

#### Development Dependencies
- `@vitejs/plugin-react` - Vite plugin for React Fast Refresh
- `typescript` - Static type checking
- `eslint` - Code linting and quality
- `@types/*` - TypeScript type definitions

### Frontend Architecture Patterns

#### Component Organization (Recommended)
```
src/
├── components/           # Reusable UI components
│   ├── common/          # Shared components (Button, Input, etc.)
│   ├── layout/          # Layout components (Header, Footer, Sidebar)
│   └── features/        # Feature-specific components
├── hooks/               # Custom React hooks
├── services/            # API client and external services
├── utils/               # Helper functions and utilities
├── types/               # TypeScript type definitions
├── contexts/            # React Context providers
├── pages/               # Page/Route components
└── assets/              # Static assets (images, fonts, etc.)
```

#### State Management (To Be Implemented)
Consider adding:
- **Context API** - For simple global state
- **Redux Toolkit** - For complex state management
- **Zustand** - For lightweight state management
- **React Query** - For server state management

---

## 🔧 Backend: `sample-backend/`

### Technology Stack (Intended)
- **Framework**: Flask (Python)
- **Expected Structure**: RESTful API

### Current Status
⚠️ **Note**: The backend directory is currently empty and needs to be scaffolded.

### Recommended Backend Structure

```
sample-backend/
├── app/                     # Application package
│   ├── __init__.py         # App factory
│   ├── config.py           # Configuration settings
│   ├── models/             # Database models (SQLAlchemy)
│   │   ├── __init__.py
│   │   └── user.py
│   ├── routes/             # API routes/blueprints
│   │   ├── __init__.py
│   │   ├── auth.py
│   │   └── api.py
│   ├── services/           # Business logic layer
│   │   ├── __init__.py
│   │   └── user_service.py
│   ├── schemas/            # Pydantic/Marshmallow schemas
│   │   ├── __init__.py
│   │   └── user_schema.py
│   └── utils/              # Helper functions
│       ├── __init__.py
│       └── validators.py
├── migrations/             # Database migrations (Alembic)
├── tests/                  # Unit and integration tests
│   ├── __init__.py
│   ├── conftest.py        # Pytest fixtures
│   └── test_api.py
├── .env.example           # Environment variables template
├── .gitignore            # Git ignore rules
├── requirements.txt      # Python dependencies
├── run.py               # Application runner
└── README.md            # Backend documentation
```

### Recommended Flask Dependencies

```txt
# Core Framework
Flask==3.0.0
Flask-CORS==4.0.0

# Database
Flask-SQLAlchemy==3.1.1
Flask-Migrate==4.0.5
psycopg2-binary==2.9.9  # PostgreSQL adapter

# Authentication & Security
Flask-JWT-Extended==4.6.0
Flask-Bcrypt==1.0.1
python-dotenv==1.0.0

# Validation & Serialization
marshmallow==3.20.1
Flask-Marshmallow==0.15.0

# API Documentation
Flask-Swagger-UI==4.11.1
flasgger==0.9.7.1

# Testing
pytest==7.4.3
pytest-flask==1.3.0
pytest-cov==4.1.0
```

### Flask Application Factory Pattern

```python
# app/__init__.py
from flask import Flask
from flask_cors import CORS
from flask_sqlalchemy import SQLAlchemy
from flask_migrate import Migrate

db = SQLAlchemy()
migrate = Migrate()

def create_app(config_name='development'):
    app = Flask(__name__)
    app.config.from_object(f'app.config.{config_name.capitalize()}Config')
    
    # Initialize extensions
    db.init_app(app)
    migrate.init_app(app, db)
    CORS(app)
    
    # Register blueprints
    from app.routes import api_bp, auth_bp
    app.register_blueprint(api_bp, url_prefix='/api')
    app.register_blueprint(auth_bp, url_prefix='/auth')
    
    return app
```

### API Design Principles

#### RESTful Endpoints Structure
```
/api/v1/users          # User resources
  GET     - List users
  POST    - Create user
  
/api/v1/users/:id      # Specific user
  GET     - Get user
  PUT     - Update user
  DELETE  - Delete user

/api/v1/auth
  POST /login          - User login
  POST /register       - User registration
  POST /refresh        - Refresh token
  POST /logout         - User logout
```

#### Response Format Standard
```json
{
  "success": true,
  "data": {},
  "message": "Operation successful",
  "errors": []
}
```

---

## 🔄 Development Workflow

### Getting Started

#### Frontend Setup
```bash
# Navigate to frontend
cd sample-client

# Install dependencies
npm install

# Start development server
npm run dev

# Access at http://localhost:5173
```

#### Backend Setup (To Be Implemented)
```bash
# Navigate to backend
cd sample-backend

# Create virtual environment
python3 -m venv venv

# Activate virtual environment
source venv/bin/activate  # Linux/Mac
# or
venv\Scripts\activate     # Windows

# Install dependencies
pip install -r requirements.txt

# Set up environment variables
cp .env.example .env

# Initialize database
flask db init
flask db migrate
flask db upgrade

# Run development server
flask run

# Access at http://localhost:5000
```

### Environment Variables

#### Frontend (`.env`)
```env
VITE_API_BASE_URL=http://localhost:5000/api/v1
VITE_APP_NAME=Sample Project
VITE_APP_VERSION=1.0.0
```

#### Backend (`.env`)
```env
FLASK_APP=run.py
FLASK_ENV=development
SECRET_KEY=your-secret-key-here
DATABASE_URL=postgresql://user:password@localhost:5432/dbname
JWT_SECRET_KEY=your-jwt-secret-key-here
CORS_ORIGINS=http://localhost:5173
```

---

## 🧪 Testing Strategy

### Frontend Testing
```bash
# Recommended testing libraries
npm install --save-dev @testing-library/react @testing-library/jest-dom vitest
```

Test structure:
```
src/
├── components/
│   └── Button/
│       ├── Button.tsx
│       ├── Button.test.tsx
│       └── Button.module.css
```

### Backend Testing
```bash
# Run tests
pytest

# With coverage
pytest --cov=app tests/
```

---

## 📦 Deployment

### Frontend Deployment

#### Build for Production
```bash
cd sample-client
npm run build
# Output: dist/ directory
```

Recommended platforms:
- **Vercel** - Zero-config deployment
- **Netlify** - Continuous deployment
- **AWS S3 + CloudFront** - Full control
- **GitHub Pages** - Free hosting

### Backend Deployment

Recommended platforms:
- **Heroku** - Easy deployment
- **AWS EC2/ECS** - Full control
- **Digital Ocean App Platform** - Simple setup
- **Railway** - Modern deployment
- **Google Cloud Run** - Serverless containers

---

## 🔒 Security Best Practices

### Frontend
- [ ] Sanitize user inputs
- [ ] Implement Content Security Policy (CSP)
- [ ] Use HTTPS in production
- [ ] Store sensitive data securely (not in localStorage)
- [ ] Implement proper CORS configuration
- [ ] Keep dependencies updated

### Backend
- [ ] Use environment variables for secrets
- [ ] Implement rate limiting
- [ ] Validate and sanitize all inputs
- [ ] Use parameterized queries (prevent SQL injection)
- [ ] Implement proper authentication/authorization
- [ ] Enable HTTPS/SSL
- [ ] Set secure HTTP headers
- [ ] Hash passwords with bcrypt
- [ ] Implement CSRF protection

---

## 🚀 Recommended Enhancements

### Frontend
1. **Routing** - Add React Router for navigation
2. **State Management** - Implement Redux Toolkit or Zustand
3. **API Layer** - Add Axios or React Query
4. **UI Framework** - Integrate Material-UI, Chakra UI, or Tailwind CSS
5. **Forms** - Add React Hook Form with Zod validation
6. **Authentication** - Implement JWT-based auth flow
7. **Error Boundary** - Add global error handling
8. **Loading States** - Implement skeleton screens and loaders
9. **PWA** - Add Progressive Web App capabilities
10. **Internationalization** - Add i18n support

### Backend
1. **Database** - Set up PostgreSQL or MongoDB
2. **ORM** - Implement SQLAlchemy models
3. **Migrations** - Add Alembic/Flask-Migrate
4. **Authentication** - JWT-based authentication
5. **Authorization** - Role-based access control (RBAC)
6. **API Documentation** - Swagger/OpenAPI
7. **Logging** - Structured logging with rotation
8. **Caching** - Redis for session and data caching
9. **Task Queue** - Celery for background jobs
10. **Monitoring** - Add Sentry for error tracking

---

## 📚 Code Style & Conventions

### Frontend (TypeScript/React)

#### Naming Conventions
- **Components**: PascalCase (`UserProfile.tsx`)
- **Hooks**: camelCase with 'use' prefix (`useAuth.ts`)
- **Utils**: camelCase (`formatDate.ts`)
- **Constants**: UPPER_SNAKE_CASE (`API_BASE_URL`)
- **Types/Interfaces**: PascalCase with 'I' prefix for interfaces (`IUser`)

#### Component Structure
```typescript
// 1. Imports (external, then internal)
import { useState, useEffect } from 'react';
import { Button } from '@/components/common';

// 2. Types/Interfaces
interface UserProfileProps {
  userId: string;
  onUpdate?: () => void;
}

// 3. Component definition
export const UserProfile: React.FC<UserProfileProps> = ({ userId, onUpdate }) => {
  // 4. Hooks
  const [user, setUser] = useState<User | null>(null);
  
  // 5. Effects
  useEffect(() => {
    // fetch user
  }, [userId]);
  
  // 6. Handlers
  const handleUpdate = () => {
    // handle update
  };
  
  // 7. Render
  return (
    <div>
      {/* JSX */}
    </div>
  );
};
```

### Backend (Python/Flask)

#### Naming Conventions
- **Classes**: PascalCase (`UserService`)
- **Functions/Methods**: snake_case (`get_user_by_id`)
- **Constants**: UPPER_SNAKE_CASE (`MAX_LOGIN_ATTEMPTS`)
- **Private methods**: Leading underscore (`_validate_token`)

#### Code Organization
```python
# 1. Standard library imports
import os
from datetime import datetime

# 2. Third-party imports
from flask import Blueprint, request, jsonify
from marshmallow import ValidationError

# 3. Local imports
from app.models import User
from app.services.user_service import UserService
from app.schemas.user_schema import UserSchema

# 4. Blueprint/Router definition
api_bp = Blueprint('api', __name__)

# 5. Route handlers
@api_bp.route('/users', methods=['GET'])
def get_users():
    """
    Get all users
    ---
    responses:
      200:
        description: List of users
    """
    users = UserService.get_all()
    return jsonify({'success': True, 'data': users}), 200
```

---

## 🔧 Troubleshooting

### Frontend Common Issues

#### Port Already in Use
```bash
# Kill process on port 5173
lsof -ti:5173 | xargs kill -9
```

#### Module Not Found
```bash
# Clear cache and reinstall
rm -rf node_modules package-lock.json
npm install
```

#### TypeScript Errors
```bash
# Restart TypeScript server in VS Code
Cmd/Ctrl + Shift + P → "TypeScript: Restart TS Server"
```

### Backend Common Issues

#### Virtual Environment Issues
```bash
# Recreate virtual environment
rm -rf venv
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

#### Database Connection Errors
- Verify DATABASE_URL in `.env`
- Ensure database service is running
- Check database permissions

---

## 📖 Additional Resources

### Frontend Resources
- [React Documentation](https://react.dev)
- [TypeScript Handbook](https://www.typescriptlang.org/docs/)
- [Vite Guide](https://vitejs.dev/guide/)
- [React TypeScript Cheatsheet](https://react-typescript-cheatsheet.netlify.app/)

### Backend Resources
- [Flask Documentation](https://flask.palletsprojects.com/)
- [SQLAlchemy Documentation](https://docs.sqlalchemy.org/)
- [Flask Best Practices](https://flask.palletsprojects.com/en/latest/patterns/)
- [Python PEP 8 Style Guide](https://pep8.org/)

### Full-Stack Resources
- [RESTful API Design](https://restfulapi.net/)
- [JWT Authentication](https://jwt.io/introduction)
- [CORS Explained](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)

---

## 👥 Contributing Guidelines

### Branch Strategy
```
main           # Production-ready code
develop        # Integration branch
feature/*      # New features
bugfix/*       # Bug fixes
hotfix/*       # Emergency fixes
```

### Commit Convention
```
feat: Add user authentication
fix: Resolve database connection issue
docs: Update API documentation
style: Format code according to style guide
refactor: Restructure user service
test: Add unit tests for auth module
chore: Update dependencies
```

### Pull Request Process
1. Create feature branch from `develop`
2. Make changes with clear commits
3. Write/update tests
4. Update documentation
5. Submit PR with description
6. Address review comments
7. Merge after approval

---

## 📝 License

This project is open source and available under the [MIT License](LICENSE).

---

## 📞 Support & Contact

For questions or support:
- Create an issue in the repository
- Contact the development team
- Check documentation

---

**Last Updated**: November 11, 2025  
**Maintained By**: Development Team  
**Version**: 1.0.0

