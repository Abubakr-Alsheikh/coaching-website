# Hassan Zaki - Life Coaching Website

This project is a fully-featured personal website for life coach Hassan Zaki. It serves as a professional online presence, allowing potential clients to learn about his services, view his certifications, and book coaching sessions. The website features a dynamic frontend built with Django and Tailwind CSS, and includes a secure admin dashboard for easy management of content, bookings, and pricing plans.

## Table of Contents

- [Key Features](#key-features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Setup and Installation](#setup-and-installation)
- [Environment Variables](#environment-variables)
- [Running the Application](#running-the-application)
- [Admin Dashboard](#admin-dashboard)
- [Deployment](#deployment)

## Key Features

-   **Dynamic Homepage**: A visually appealing homepage featuring a hero section, an "About/My Journey" section, a display of certifications, and pricing plans. All content is manageable through the admin dashboard.
-   **Coaching Plans**: C.R.U.D. functionality for creating, displaying, and managing multiple coaching plans, including support for featured plans and discounts.
-   **Smart Booking System**: An intuitive booking form that:
    -   Automatically detects the user's timezone.
    -   Calculates and displays available time slots in real-time based on the coach's schedule and existing appointments.
    -   Prevents double-booking.
-   **Admin Dashboard**: A secure, login-protected dashboard for the coach to:
    -   View, manage, hide, and delete incoming coaching requests.
    -   Create, update, and delete pricing plans.
    -   Manage certifications (add, edit, delete).
    -   Update all major content on the public-facing website.
-   **Automated Email Notifications**:
    -   Sends a confirmation email to the client upon successful booking.
    -   Sends a notification email with booking details to the coach.
-   **Responsive Design**: Built with Tailwind CSS and Flowbite for a seamless experience on all devices, from desktops to mobile phones.

## Tech Stack

-   **Backend**: Python, Django
-   **Frontend**: HTML, Tailwind CSS, Flowbite, JavaScript
-   **Database**: SQLite3 (for development)
-   **Core Libraries**:
    -   `django-compressor`: To compress and bundle CSS/JS files.
    -   `python-dotenv`: To manage environment variables.

## Project Structure

```
abubakr-alsheikh-hassanzaki-coaching-website/
├── coaching_website/ # Django project configuration (settings, urls)
│   └── settings/     # Environment-specific settings (dev/prod)
├── core/             # Main application logic (models, views, forms, urls)
├── static/           # Static assets (CSS source, images)
├── templates/        # HTML templates for the application
├── manage.py         # Django's command-line utility
├── requirements.txt  # Python dependencies
├── package.json      # Node.js dependencies (Tailwind, Flowbite)
└── README.md
```

## Setup and Installation

Follow these steps to get the project up and running on your local machine.

#### Prerequisites

-   Python 3.x
-   Node.js and npm

#### 1. Clone the Repository

```bash
git clone https://github.com/your-username/abubakr-alsheikh-hassanzaki-coaching-website.git
cd abubakr-alsheikh-hassanzaki-coaching-website
```

#### 2. Setup Python Virtual Environment & Install Dependencies

```bash
# Create and activate a virtual environment
python -m venv venv
source venv/bin/activate  # On Windows, use `venv\Scripts\activate`

# Install Python packages
pip install -r requirements.txt
```

#### 3. Setup Frontend & Install Dependencies

```bash
# Install Node.js packages
npm install
```

#### 4. Configure Environment Variables

Create a `.env` file in the project root directory. You can copy the example below and fill in your details.

```bash
# See the "Environment Variables" section below for details.
cp .env.example .env
# Now edit the .env file with your credentials
```

#### 5. Build Tailwind CSS

Run the following command to compile the Tailwind CSS file. For development, you can keep this running in a separate terminal to automatically rebuild the CSS when you make changes.

```bash
# This command watches for changes and rebuilds the CSS automatically
npx tailwindcss -i ./static/src/input.css -o ./static/src/output.css --watch
```

#### 6. Database Migrations

Apply the database migrations to create the database schema.

```bash
python manage.py migrate
```

#### 7. Create Superuser

Create an admin user to access the dashboard.

```bash
python manage.py createsuperuser
```

Follow the prompts to set a username, email, and password.

## Environment Variables

The project uses a `.env` file to manage sensitive information and environment-specific settings. Create a file named `.env` in the root directory and add the following variables.

```plaintext
# .env.example

# Set to 'development' for local development or 'production' for deployment
DJANGO_ENV=development

# Generate a new secret key for your project.
# You can generate one using: python -c 'from django.core.management.utils import get_random_secret_key; print(get_random_secret_key())'
SECRET_KEY='your-strong-django-secret-key'

# Email Settings (example for Gmail)
# For Gmail, you will need to create an "App Password".
EMAIL_HOST_USER='your-email@gmail.com'
EMAIL_HOST_PASSWORD='your-gmail-app-password'
DEFAULT_FROM_EMAIL='your-email@gmail.com'

# The email address that will receive new coaching request notifications.
ADMIN_EMAIL='admin-email-to-receive-notifications@example.com'
```

## Running the Application

1.  **Start the Tailwind CSS compiler** (in a dedicated terminal, if not already running):
    ```bash
    npx tailwindcss -i ./static/src/input.css -o ./static/src/output.css --watch
    ```

2.  **Start the Django Development Server** (in a new terminal):
    ```bash
    python manage.py runserver
    ```

The application will now be available at `http://127.0.0.1:8000/`.

## Admin Dashboard

-   Access the login page at `http://127.0.0.1:8000/accounts/login/`.
-   Use the superuser credentials created during setup to log in.
-   Once logged in, you can navigate the dashboard to manage coaching requests, pricing plans, certifications, and homepage content.

## Deployment

The project is structured for both development and production environments. For deployment:

-   Set the `DJANGO_ENV` environment variable to `production`.
-   The `coaching_website/settings/production.py` file will be used, which sets `DEBUG = False`.
-   Update `ALLOWED_HOSTS` in `coaching_website/settings/production.py` with your domain(s).
-   Run `python manage.py collectstatic` to gather all static files into the `staticfiles` directory.
-   Use a production-grade web server like Gunicorn or uWSGI and a reverse proxy like Nginx to serve the application.
