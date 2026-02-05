# Legal Tabular Review System

A full-stack application for legal document review that ingests multiple legal documents, extracts key fields into a structured table, and supports side-by-side comparison with review workflows and customizable field templates.

## 🚀 Features

- **Multi-Format Document Ingestion**: Support for PDF, DOCX, HTML, and TXT formats
- **Field Extraction**: Automated extraction of key fields from legal documents with:
  - Source citations (document + location)
  - Confidence scores
  - Normalization output and raw text
- **Customizable Field Templates**: Create and manage custom field schemas with validation rules
- **Review Workflows**: Comprehensive review states (CONFIRMED, REJECTED, MANUAL_UPDATED, MISSING_DATA, PENDING)
- **Tabular Comparison**: Side-by-side comparison of extracted fields across multiple documents
- **Project Management**: Organize documents into projects with status tracking (DRAFT, ACTIVE, COMPLETED, ARCHIVED)
- **API Documentation**: Interactive Swagger/OpenAPI documentation

## 🛠️ Tech Stack

### Backend
- **Framework**: NestJS (Node.js/TypeScript)
- **Database**: PostgreSQL with Prisma ORM
- **API Documentation**: Swagger/OpenAPI
- **Document Parsing**: 
  - PDF: pdf-parse
  - DOCX: mammoth
  - HTML: cheerio
- **Validation**: class-validator, class-transformer

### Frontend
- **Framework**: React 18 with TypeScript
- **Build Tool**: Vite
- **Routing**: React Router v6
- **State Management**: TanStack Query (React Query)
- **HTTP Client**: Axios
- **UI**: Lucide React icons, custom components
- **Styling**: CSS with clsx for conditional classes

## 📋 Prerequisites

Before you begin, ensure you have the following installed:
- **Node.js**: v18.x or higher (v20.18.1+ recommended for optimal compatibility)
- **npm**: v10.x or higher
- **PostgreSQL**: v12 or higher
- **Git**: For cloning the repository

## 🔧 Installation

### 1. Clone the Repository

```bash
git clone <repository-url>
cd legal-tabular-review
```

### 2. Backend Setup

```bash
cd backend

# Install dependencies
npm install

# Create .env file from example
cp .env.example .env

# Edit .env with your database credentials
# DATABASE_URL="postgresql://user:password@localhost:5432/dbname"
# PORT=3000
# NODE_ENV=development

# Generate Prisma Client
npx prisma generate

# Run database migrations
npx prisma migrate dev

# (Optional) Seed the database with sample data
npm run seed
```

### 3. Frontend Setup

```bash
cd ../frontend

# Install dependencies
npm install

# (Optional) Create .env file for custom API URL
# VITE_API_URL=http://localhost:3000
```

## 🚀 Running the Application

### Development Mode

Both applications are currently running and accessible!

**Backend Server:**
```bash
cd backend
npm run start:dev
```
- **URL**: http://localhost:3000
- **Swagger API Docs**: http://localhost:3000/api/docs
- **Status**: ✅ Running with hot-reload

**Frontend Application:**
```bash
cd frontend  
npm run dev
```
- **URL**: http://localhost:5174
- **Status**: ✅ Running with Tailwind CSS
- **Features**: Modern UI with loading states, error handling, and responsive design

### Production Mode

**Backend**:
```bash
cd backend
npm run build
npm run start:prod
```

**Frontend**:
```bash
cd frontend
npm run build
npm run preview
```

## 📚 API Documentation

Once the backend is running, access the interactive Swagger documentation at:
**http://localhost:3000/api/docs**

### Available API Endpoints

#### Projects
- `POST /projects` - Create a new project
- `GET /projects` - List all projects
- `GET /projects/:id` - Get project details
- `GET /projects/:id/statistics` - Get project statistics
- `PATCH /projects/:id` - Update project
- `DELETE /projects/:id` - Delete project

#### Documents
- `POST /documents/upload` - Upload a document file
- `POST /documents` - Create document metadata
- `GET /documents` - List all documents
- `GET /documents/:id` - Get document details
- `DELETE /documents/:id` - Delete document

#### Field Templates
- `POST /field-templates` - Create field template
- `GET /field-templates` - List all templates
- `GET /field-templates/:id` - Get template details
- `PATCH /field-templates/:id` - Update template
- `DELETE /field-templates/:id` - Delete template

#### Extractions
- `POST /extractions/start` - Start extraction process
- `POST /extractions/:id/complete` - Mark extraction complete
- `PATCH /extractions/:id/fail` - Mark extraction failed
- `GET /extractions` - List extractions
- `GET /extractions/:id` - Get extraction details

#### Reviews
- `GET /reviews` - List all reviews
- `GET /reviews/statistics/:projectId` - Get review statistics
- `GET /reviews/progress/:projectId` - Get review progress
- `GET /reviews/extracted-field/:extractedFieldId` - Get reviews by field
- `GET /reviews/:id` - Get review details
- `PATCH /reviews/:id` - Update review

#### Health
- `GET /health` - Health check endpoint

## 📁 Project Structure

```
legal-tabular-review/
├── backend/                    # NestJS Backend Application
│   ├── prisma/
│   │   ├── schema.prisma      # Database schema
│   │   └── migrations/        # Database migrations
│   ├── src/
│   │   ├── app.module.ts      # Main application module
│   │   ├── main.ts            # Application entry point
│   │   ├── document/          # Document management module
│   │   ├── extraction/        # Field extraction module
│   │   ├── field-template/    # Field template module
│   │   ├── health/            # Health check module
│   │   ├── prisma/            # Prisma service
│   │   ├── project/           # Project management module
│   │   └── review/            # Review workflow module
│   ├── package.json
│   └── .env                   # Environment variables
│
├── frontend/                  # React Frontend Application
│   ├── src/
│   │   ├── api/               # API client functions
│   │   ├── components/        # Reusable components
│   │   ├── pages/             # Page components
│   │   ├── App.jsx            # Main app component
│   │   └── main.jsx           # Application entry point
│   ├── package.json
│   └── vite.config.ts         # Vite configuration
│
├── data/                      # Sample legal documents for testing
├── docs/                      # Additional documentation
│   ├── REQUIREMENTS.md        # Detailed requirements
│   └── README.md              # Design documentation
└── README.md                  # This file
```

## 🗄️ Database Schema

The application uses PostgreSQL with Prisma ORM. Key entities include:

- **Project**: Container for documents and field templates
- **Document**: Legal documents with metadata and parsed content
- **FieldTemplate**: Customizable field definitions with types and validation
- **Extraction**: Extraction process tracking with status
- **ExtractedField**: Individual field values with citations and confidence
- **Review**: Review workflow with manual overrides and audit trail

### Database Migrations

```bash
# Create a new migration
npx prisma migrate dev --name migration_name

# Apply migrations
npx prisma migrate deploy

# Open Prisma Studio (database GUI)
npx prisma studio
```

## 🧪 Testing

### Frontend Testing

The frontend includes Vitest for testing with React Testing Library.

```bash
cd frontend

# Run tests once
npm test

# Run tests in watch mode
npm run test

# Run tests with UI
npm run test:ui

# Run tests with coverage
npm run test:coverage
```

**Test Files:**
- `src/test/HomePage.test.tsx` - HomePage component tests
- `src/test/Layout.test.tsx` - Layout component tests  
- `src/test/api.test.ts` - API client tests

**Note:** Testing requires Node.js v20+ due to jsdom dependencies. If using Node v18, some tests may fail with ESM compatibility errors. Consider upgrading to Node v20 or higher for full testing support.

### Sample Dataset

Sample legal documents are available in the `data/` directory:
- `EX-10.2.html` - Sample contract document
- `Tesla, Inc. (Form_ PRE 14A, Received_ 09_05_2025 06_21_37).html` - Proxy filing

Use these documents to test:
- Document ingestion and parsing
- Field extraction with citations
- Review workflow states
- Template updates and re-extraction

### Validation Checklist

- [ ] Multi-format document upload (PDF, DOCX, HTML, TXT)
- [ ] Field extraction includes: value, citations, confidence, normalization
- [ ] Custom field templates can be created and updated
- [ ] Template updates trigger re-extraction
- [ ] Review states properly tracked (CONFIRMED, REJECTED, MANUAL_UPDATED, etc.)
- [ ] Tabular comparison displays fields across documents
- [ ] Project statistics and progress tracking
- [ ] API endpoints return proper error codes and messages

## 🔨 Development

### Code Formatting

**Backend**:
```bash
npm run format  # Format code with Prettier
npm run lint    # Lint and fix code
```

**Frontend**:
```bash
npm run lint    # ESLint validation
```

### Adding a New Module (Backend)

```bash
cd backend
nest generate module module-name
nest generate controller module-name
nest generate service module-name
```

## 🐛 Troubleshooting

### Backend won't start
- Ensure PostgreSQL is running
- Verify `.env` file has correct `DATABASE_URL`
- Run `npx prisma generate` to regenerate Prisma Client
- Check if port 3000 is available

### Frontend build errors
- Clear node_modules and reinstall: `rm -rf node_modules && npm install`
- Ensure Node version is v18+ (check with `node -v`)
- Check if backend is running on expected port

### Database connection issues
- Verify PostgreSQL service is running
- Check database credentials in `.env`
- Ensure database exists (create with `createdb dbname`)
- Check firewall and network settings

### CORS errors
- Verify backend CORS configuration in `main.ts`
- Check frontend API URL in `.env` or `api/index.js`
- Ensure both services are running on expected ports

## 📄 Documentation

- **Requirements**: See [docs/REQUIREMENTS.md](docs/REQUIREMENTS.md) for detailed task descriptions
- **API Docs**: http://localhost:3000/api/docs (when backend is running)
- **Design Docs**: See [docs/README.md](docs/README.md) for architecture and design decisions

## 🤝 Contributing

1. Create a feature branch: `git checkout -b feature/your-feature`
2. Commit your changes: `git commit -am 'Add new feature'`
3. Push to the branch: `git push origin feature/your-feature`
4. Submit a pull request

## 📝 License

MIT

## 👥 Authors

MHS676

---

**Note**: This is a demonstration project for the Legal Tabular Review system. For production deployment, ensure proper security measures, environment variable management, and database backup strategies are in place.
