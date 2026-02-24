# FinSync

FinSync is a comprehensive financial synchronization and tax compliance platform designed to streamline invoice management, data extraction, and GST (Goods and Services Tax) return filing. It provides an end-to-end solution for businesses to upload financial documents, automatically extract relevant data, and seamlessly communicate with government tax portals.

## 🌟 Key Features

- **User Authentication & Management**: Secure login and registration system with role-based access and data isolation.
- **Invoice Data Extraction**: Automated processing of uploaded files (PDF, Excel, CSV) to extract invoice details, amounts, and tax information using a dedicated Python backend.
- **GST Return Management**: Track and manage GST returns (GSTR-1, GSTR-3B) with status tracking.
- **Government Portal Integration**: Built-in integration with government tax portals (currently featuring a robust mock implementation with file validation, error handling, and realistic reference number generation, ready for real API integration).
- **Report Generation**: Export processed data and tax summaries to various formats (Excel, PDF, CSV).
- **Interactive Dashboard**: Modern, responsive UI with informative charts and data tables.

## 🏗️ Architecture & Tech Stack

FinSync is built using a modern, full-stack architecture separated into a fast frontend, a robust Node.js backend, and a specialized Python service for data processing.

### Frontend
- **Framework**: React 18 with Vite
- **Routing**: Wouter
- **Styling**: Tailwind CSS & Framer Motion
- **UI Components**: Shadcn UI (Radix UI primitives)
- **State Management & Data Fetching**: TanStack React Query
- **Forms & Validation**: React Hook Form with Zod

### Backend (Node.js)
- **Framework**: Express.js
- **Authentication**: Passport.js (Local Strategy, bcrypt for password hashing)
- **ORM**: Drizzle ORM
- **Database**: MySQL 8.0 (with SQLite fallback support)
- **File Handling**: Multer for document uploads

### Backend (Python)
- Dedicated service for advanced invoice data extraction, AI/OCR processing, and data parsing.

## 🗄️ Database Schema Overview

The database ensures strict 100% data isolation between users. Major entities include:
- `users`: Core account management and authentication.
- `invoices`: Extracted invoice data (invoice number, GSTIN, amount, tax, HSN code).
- `gst_returns`: Tracking of tax filings and compliance status.
- `uploaded_files`: Tracking of source documents and processing status.
- `download_history`: Logging of generated report downloads.

_For a comprehensive breakdown, refer to `FinSync-main/DATABASE_STRUCTURE_OVERVIEW.md`._

## 🚀 Setup & Installation

### Prerequisites
- Node.js (v18 or higher recommended)
- Python (v3.10 or higher) for the data processing backend
- MySQL 8.0 server

### 1. Clone the repository
\`\`\`bash
git clone https://github.com/AbidAli-hub/Finsync_Main.git
cd Finsync_Main/FinSync-main
\`\`\`

### 2. Environment Configuration
Copy the sample environment file and configure your local settings:
\`\`\`bash
cp .env.example .env
\`\`\`
Ensure you set the appropriate database credentials (`DATABASE_URL`) and government API configuration if switching to production mode (`USE_REAL_GOVERNMENT_API`).

### 3. Install Dependencies
\`\`\`bash
# Install Node.js dependencies
npm install

# Install Python dependencies
cd python_backend
pip install -r requirements.txt # (or refer to pyproject.toml / uv.lock if using uv/poetry)
cd ..
\`\`\`

### 4. Database Setup
Push the Drizzle ORM schema to your configured database:
\`\`\`bash
npm run db:push
\`\`\`

### 5. Running the Application
You can start the development servers using the provided batch scripts (on Windows):
\`\`\`cmd
# Start all servers (Frontend, Node Backend, Python Backend)
start-all-servers.bat

# Or start the Node dev server manually
npm run dev
\`\`\`

## 🔒 Security
- Passwords are encrypted using `bcrypt`.
- 100% database-level user isolation guarantees that users can only access their own invoices and financial data.
- Built-in validation checks for all uploaded files (size, format, existence) prior to processing or government portal submission.

## 📄 License
This project is licensed under the MIT License.
