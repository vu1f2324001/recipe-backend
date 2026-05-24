# Recipe App (Frontend + Backend)

A full-stack **Recipe** web application with:
- **Node.js + Express** backend
- **MongoDB (Mongoose)** for storing users and recipes
- **JWT authentication** (Register/Login/Profile)
- **Firebase Storage** for recipe image uploads
- Simple frontend pages (HTML/CSS/JS)

---

## Project Structure

- `recipe-backend/` — Express API (auth, recipes, upload)
- `recipe-frontend/` — Static frontend (HTML/CSS/JS)

---

## Backend (recipe-backend)

### Requirements
- Node.js 18+
- MongoDB running (local or Atlas)
- Firebase project with Storage enabled

### Setup
1. Go to backend directory:
   ```bash
   cd recipe-backend
   ```
2. Create `.env` (if not already) with at least:
   - `MONGO_URI`
   - `JWT_SECRET`
   - `FIREBASE_STORAGE_BUCKET`
   - `GOOGLE_API_KEY` (optional; depends on how you use firebase client side)

3. Install dependencies:
   ```bash
   npm install
   ```

### Run
- Development:
  ```bash
  npm run dev
  ```
- Production:
  ```bash
  npm start
  ```

Backend default port: **5012**

---

## API Endpoints

### Auth
- `POST /api/auth/register`
  - Body: `{ name, email, password }`
- `POST /api/auth/login`
  - Body: `{ email, password }`
  - Returns: `{ token }`
- `GET /api/auth/profile`
  - Requires `Authorization: Bearer <token>`

### Recipes
- `POST /api/recipe/add`
  - Body: `{ recipeName, recipeDescription, imageUrl }`

### Upload (Firebase Storage)
- `POST /upload`
  - FormData: `file` (image)
  - Returns: `{ url }`

> Note: The current frontend recipe flow uploads directly to Firebase Storage from the browser (using `recipe-frontend/js/script.js`) and then calls `POST /api/recipe/add` with the `imageUrl`.

---

## Frontend (recipe-frontend)

### How it works
- Login/Register pages call backend endpoints:
  - `http://localhost:5012/api/auth/login`
  - `http://localhost:5012/api/auth/register`
- After login, user is redirected to `dashboard.html`.
- Recipe upload:
  - Browser uploads the selected image to Firebase Storage.
  - Then it calls `POST http://127.0.0.1:5012/api/recipe/add`.

### Run
Open `recipe-frontend/*.html` in a browser (no build step required).

---

## Environment Variables Summary (Backend)

Create `recipe-backend/.env` with:
- `MONGO_URI=...`
- `JWT_SECRET=...`
- `FIREBASE_STORAGE_BUCKET=...`

---

## Troubleshooting
- **MongoDB connection fails**: check `MONGO_URI`.
- **JWT failures**: verify `JWT_SECRET` matches between login and auth middleware.
- **Firebase upload fails**:
  - ensure Firebase Storage bucket is correct
  - ensure service account JSON in `recipe-backend/config/firebase-adminsdk.json` matches your Firebase project

---

## License
ISC

