# Django Todo List

A Todo List web application built with **Python and Django**, with a production-oriented serving setup using **Gunicorn** and **Nginx**.

This project was also used as a hands-on exercise to understand how Django applications are served through an application server and a reverse proxy.

## Tech Stack

- Python
- Django
- SQLite
- Gunicorn
- Nginx
- Linux (Ubuntu / WSL2)

## Architecture

The application uses Gunicorn to run the Django application, while Nginx acts as a reverse proxy and forwards incoming HTTP requests to Gunicorn.

```text
Client / Browser
       |
       v
 Nginx (:8080)
       |
       v
Gunicorn (:8000)
       |
       v
Django Application
```

## Project Structure

```text
django-todo-list/
│
├── todo_app/
├── todo_project/
├── deploy/
│   └── nginx/
│       └── todo_list.conf
├── static/
├── manage.py
├── requirements.txt
└── README.md
```

## Running Locally

### 1. Clone the repository

```bash
git clone https://github.com/anasyaghi9/django-todo-list.git
cd django-todo-list
```

### 2. Create and activate a virtual environment

```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Apply migrations

```bash
python manage.py migrate
```

### 5. Run the development server

```bash
python manage.py runserver
```

Open `http://127.0.0.1:8000` in your browser.

## Gunicorn Configuration

Gunicorn is used as the WSGI application server to run the Django application.

```bash
gunicorn --workers 3 --bind 127.0.0.1:8000 todo_project.wsgi:application
```

## Nginx Configuration

The Nginx configuration is available at:

`deploy/nginx/todo_list.conf`

Nginx listens on port `8080` and forwards incoming requests to Gunicorn running on port `8000`.

To test the Nginx configuration:

```bash
sudo nginx -t
```

To reload Nginx after configuration changes:

```bash
sudo systemctl reload nginx
```

Access the application through:

`http://localhost:8080`

## What I Learned

- Understanding the role of Gunicorn as a WSGI application server.
- Configuring Nginx as a reverse proxy for a Django application.
- Understanding the request flow between the client, Nginx, Gunicorn, and Django.
- Working with Linux and Ubuntu through WSL2.
- Managing application processes and server configurations.

## Author

**Anas Atallah Yaghi**

- GitHub: [@anasyaghi9](https://github.com/anasyaghi9)
- LinkedIn: [Anas Yaghi](https://linkedin.com/in/anas-yaghi-a431aa287)
