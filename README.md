# django-react-notes

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg?style=flat)](backend/requirements.txt)
[![Node](https://img.shields.io/badge/Node-18%2B-green.svg?style=flat)](frontend/package.json)

A notes application with a Django REST API backend and a React (Vite) frontend. Users register, log in, and manage their own notes. Authentication is handled with JWT.

## Tech stack

**Backend**
- Django 4.2
- Django REST Framework
- Simple JWT for authentication
- PostgreSQL

**Frontend**
- React 19
- Vite 7
- React Router
- Axios

## Project structure

```
app/
├── backend/     Django project and REST API
└── frontend/    React single page application
```

## Prerequisites

- Python 3.10 or newer
- Node.js 18 or newer
- A running PostgreSQL instance

## Backend setup

1. Move into the backend folder and create a virtual environment.

   ```
   cd backend
   python -m venv venv
   source venv/bin/activate   # on Windows use: venv\Scripts\activate
   ```

2. Install the dependencies.

   ```
   pip install -r requirements.txt
   ```

3. Create a `.env` file inside `backend/` with your database credentials.

   ```
   DB_NAME=your_database_name
   DB_USER=your_database_user
   DB_PWD=your_database_password
   DB_HOST=localhost
   DB_PORT=5432
   ```

4. Run the migrations.

   ```
   python manage.py migrate
   ```

5. Optionally, create an admin user so you can access the Django admin panel.

   ```
   python manage.py createsuperuser
   ```

6. Start the development server.

   ```
   python manage.py runserver
   ```

The API is now available at `http://localhost:8000`.

## Frontend setup

1. Move into the frontend folder and install the dependencies.

   ```
   cd frontend
   npm install
   ```

2. By default the frontend expects the API at a preconfigured path. To point it at your local backend instead, create a `.env` file inside `frontend/`.

   ```
   VITE_API_URL=http://localhost:8000
   ```

3. Start the development server.

   ```
   npm run dev
   ```

The app is now available at `http://localhost:5173`.

## API endpoints

| Method | Endpoint                     | Description                    | Auth required |
|--------|-------------------------------|---------------------------------|----------------|
| POST   | `/api/user/register/`         | Create a new user               | No             |
| POST   | `/api/token/`                 | Obtain access and refresh tokens| No             |
| POST   | `/api/token/refresh/`         | Refresh an access token         | No             |
| GET    | `/api/notes/`                 | List the logged in user's notes | Yes            |
| POST   | `/api/notes/`                 | Create a note                   | Yes            |
| DELETE | `/api/notes/delete/<id>/`     | Delete a note                   | Yes            |

Authenticated requests need an `Authorization: Bearer <access_token>` header.

## Notes for local development

- `DEBUG` is enabled and CORS is fully open in the current backend settings, which is fine for local development but should be tightened before any real deployment.
- The Django secret key in `settings.py` is a placeholder and should be replaced with a proper secret outside of local development.
