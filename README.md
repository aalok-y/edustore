
# EduStore

EduStore is a secure document management and sharing platform for students and organizations. Students upload AES-encrypted documents, set access validity periods, and share them with authorized organizations. After a document's validity expires, organizations lose access.

---

## Features

### Student-side

* **User Authentication and Authorization** via Clerk (OAuth 2.0 / OpenID Connect).
* **Encrypted Uploads**: AES-256–encrypted files handled by Multer.
* **Validity Period**: Per-document expiry dates; post-expiry access is denied.
* **Access Control**: Share and revoke documents with specific organizations.
* **Extension Requests**: Request and track validity-period extensions.
* **Dashboard**: Manage and view document metadata (upload date, expiry, status).

### Organization-side

* **Shared Documents Listing** with filtering by expiry status.
* **Validity Enforcement**: Automatic blocking of expired files.
* **Extension Management**: Approve or deny extension requests.
* **Access Revocation**: Manually revoke student access.
* **Audit Logs**: Track access events and request histories.

### Common

* **AES Encryption** (client- and server-side) for document confidentiality.
* **REST API**: CRUD endpoints for documents, users, and requests.
* **RBAC**: Student and Organization roles enforced in middleware and database.

---

## Tech Stack

### Backend

* **Express (Node.js)**: REST API framework
* **Clerk (Express middleware)**: Authentication and user management
* **Prisma ORM**: Database schema, migrations, and type-safe queries
* **AES Encryption**: AES-256-GCM for secure document handling
* **TypeScript**: Static typing and developer tooling

### Frontend

* **React with TypeScript**: Component-based UI
* **ShadCN/ui**: Tailwind CSS–powered component library
* **Clerk React**: Auth UI and hooks
* **TanStack Query**: Data fetching and caching
* **AES Encryption**: Web Crypto API for client-side encryption

---

## Installation

This repository uses **Git submodules** for `backend` and `frontend`. Clone with:

```bash
git clone --recurse-submodules <monorepo-url>
cd edustore
```

If you already cloned without submodules:

```bash
git submodule update --init --recursive
```

### Backend

1. Enter the submodule folder:

   ```bash
   cd backend
   ```
2. Copy and edit environment variables:

   ```bash
   cp .env.example .env
   # then set values in backend/.env:
   # DATABASE_URL=
   # PORT=8000
   # JWT_SECRET=
   # CLERK_PUBLISHABLE_KEY=
   # CLERK_SECRET_KEY=
   # CLERK_SIGN_IN_URL=
   # ENCRYPTION_KEY=
   # ENCRYPTION_SALT=
   ```
3. Install and start:

   ```bash
   npm install
   npx prisma migrate deploy
   npm start
   ```

### Frontend

1. Switch to the folder:

   ```bash
   cd ../frontend
   ```
2. Copy and configure env:

   ```bash
   cp .env.example .env
   # then set values in frontend/.env:
   # VITE_CLERK_PUBLISHABLE_KEY=
   # VITE_API_URL=
   # VITE_CLERK_SIGN_IN_URL=/sign-in
   # VITE_CLERK_SIGN_UP_URL=/sign-up
   ```
3. Install and run:

   ```bash
   npm install
   npm run dev
   ```

---

## Environment Variables

### Backend (`backend/.env`)

```text
# PostgreSQL Database URL
DATABASE_URL=

# Port your backend server runs on
PORT=8000

# JWT secret used for signing tokens (keep it secure)
JWT_SECRET=

# Clerk public API key (from Clerk dashboard)
CLERK_PUBLISHABLE_KEY=

# Clerk secret API key (do NOT share this)
CLERK_SECRET_KEY=

# URL to redirect for Clerk sign-in
CLERK_SIGN_IN_URL=

# Encryption key used for securing file data
ENCRYPTION_KEY=

# Salt used along with the encryption key
ENCRYPTION_SALT=
```

### Frontend (`frontend/.env`)

```text
# Clerk Publishable Key (from your Clerk dashboard)
VITE_CLERK_PUBLISHABLE_KEY=

# API Base URL
VITE_API_URL=

# Clerk Sign-In Page URL
VITE_CLERK_SIGN_IN_URL=/sign-in

# Clerk Sign-Up Page URL
VITE_CLERK_SIGN_UP_URL=/sign-up
```

