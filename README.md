# Tracker-Backend

A FastAPI backend for personal finance tracking, supporting user authentication, expense/income management, dashboard summaries, and image uploads to Google Cloud Storage.

---

## Features

- User registration, login, JWT authentication, profile update, and deletion
- Expense and income CRUD operations
- Dashboard summary endpoint
- Image upload to Google Cloud Storage
- Email notification support
- Interactive API documentation (Swagger UI)

---

## Project Structure

```
Tracker-Backend-develop/
│
├── main.py
├── requirement.txt
├── .env
├── README.md
├── src/
│   ├── configs/
│   ├── dashboard/
│   ├── expense/
│   ├── income/
│   ├── security/
│   ├── user/
│   └── utility/
├── tests/
└── uploads/
```

---

## Environment Variables (`.env`)

Create a `.env` file in your project root with the following content:

```env
DATABASE_URL=mysql+pymysql://root:root@127.0.0.1:3306/tracker
SECRET_KET=YOUR_SECRET_KEY
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=300
MAIL_USERNAME=YOUR_EMAIL
MAIL_PASSWORD=YOUR_EMAIL_PASSWORD
MAIL_FROM=YOUR_EMAIL
GOOGLE_APPLICATION_CREDENTIALS=PATH_TO_GCP_JSON
GCP_BUCKET_NAME=YOUR_GCP_BUCKET_NAME
```

**Descriptions:**
- `DATABASE_URL`: MySQL connection string.
- `SECRET_KET`: Secret key for JWT tokens.
- `ALGORITHM`: JWT signing algorithm.
- `ACCESS_TOKEN_EXPIRE_MINUTES`: Token expiry time (minutes).
- `MAIL_USERNAME`, `MAIL_PASSWORD`, `MAIL_FROM`: Email credentials for notifications.
- `GOOGLE_APPLICATION_CREDENTIALS`: Path to your Google Cloud service account JSON.
- `GCP_BUCKET_NAME`: Google Cloud Storage bucket for images.

---

## Installation & Setup

1. **Clone the repository**
   ```sh
   git clone <repo-url>
   cd Tracker-Backend-develop
   ```

2. **Install dependencies**
   ```sh
   pip install -r requirement.txt
   ```

3. **Configure `.env`**
   - Copy the example above and fill in your credentials.

4. **Prepare MySQL**
   - Ensure MySQL is running and the `tracker` database exists.

5. **Run the server**
   ```sh
   uvicorn main:app --reload
   ```

6. **Access API documentation**
   - Open [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs) in your browser.

   ![Swagger UI Screenshot](docs/swagger_ui.png)

---

## Running Tests

To run the unit tests:
```sh
pytest
```

---

## API Endpoints Overview

### User

- `POST /user/register` – Register a new user
- `POST /user/login` – User login
- `POST /user/verify` – Verify OTP
- `GET /user/user_data` – Get user details
- `PUT /user/user_update` – Update user details
- `DELETE /user/user_delete` – Delete user
- `POST /user/upload_image` – Upload user image

### Expense

- `POST /expense/expense_create` – Create expense
- `GET /expense/expense_details` – List expenses
- `DELETE /expense/expense_delete/{id}` – Delete expense
- `GET /expense/expense_download` – Download expenses

### Income

- `POST /income/income_create` – Create income
- `GET /income/income_details` – List incomes
- `DELETE /income/income_delete/{id}` – Delete income
- `GET /income/income_download` – Download incomes

### Dashboard

- `GET /user/dashboard` – Get dashboard summary

---

## Usage

- Use the Swagger UI for interactive API testing.
- Endpoints requiring authentication need a JWT token (obtain via `/user/login`).

---

## References

- [FastAPI Documentation](https://fastapi.tiangolo.com/)
- [Swagger UI](https://swagger.io/tools/swagger-ui/)

---

**API Docs Screenshot Example:**

![Swagger UI Screenshot](docs/swagger_ui.png)

---

*This project is under active development. More features coming soon!*
