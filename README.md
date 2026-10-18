# Django REST App

A Django project that demonstrates REST APIs for students, employees, blogs, and comments. It uses Django REST Framework serializers and views, with examples of function-based views, generic views, and a model viewset.

## Tech stack

- Python
- Django
- Django REST Framework
- django-filter
- SQLite (the default database)

There is no dependency lockfile or requirements file in this repository yet. Install the packages listed above in your Python environment before starting the project.

## Getting started

### Prerequisites (macOS)

- Python 3.12 or newer
- `pip`
- macOS Terminal (the commands below use the default `zsh` shell)

If Python 3 is not installed, install it with [Homebrew](https://brew.sh/):

```bash
brew install python
```

From the project root, create and activate a virtual environment, then install the dependencies:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install Django djangorestframework django-filter
```

Apply the database migrations and start the development server:

```bash
python manage.py migrate
python manage.py runserver
```

Open <http://127.0.0.1:8000/api/v1/students/> to browse the API. The Django admin is at <http://127.0.0.1:8000/admin/>.

To create an admin account for the admin site, run:

```bash
python manage.py createsuperuser
```

## API routes

All REST API routes are prefixed with `/api/v1/`.

| Resource | Routes | Methods |
| --- | --- | --- |
| Students | `/api/v1/students/`, `/api/v1/students/<id>/` | Collection: `GET`, `POST`; detail: `GET`, `PUT`, `DELETE` |
| Employees | `/api/v1/employees/`, `/api/v1/employees/<id>/` | Collection: `GET`, `POST`; detail: `GET`, `PUT`, `PATCH`, `DELETE` |
| Blogs | `/api/v1/blogs/`, `/api/v1/blogs/<id>/` | Collection: `GET`, `POST`; detail: `GET`, `PUT`, `PATCH`, `DELETE` |
| Comments | `/api/v1/comments/`, `/api/v1/comments/<id>/` | Collection: `GET`, `POST`; detail: `GET`, `PUT`, `PATCH`, `DELETE` |

For example, retrieve the students collection with:

```bash
curl http://127.0.0.1:8000/api/v1/students/
```

Employees support filtering by `designation`, `emp_name`, `id_min`, and `id_max`. Blog collection results support search with `?q=<term>` and ordering with `?order-by=<field>` (for example, `id` or `blog_title`). Blog and comment collections use limit/offset pagination (two results per page by default). The employee endpoint uses its own pagination parameters, `page-num` and `page_size`.

The separate `/students/` route serves a simple sample response and is not part of the versioned REST API.

## Project layout

```text
django_rest_main/   Django project settings and top-level URL configuration
api/                Versioned REST API views, serializers, and pagination
students/           Student model and sample web route
employees/          Employee model and filtering
blogs/              Blog and comment models and serializers
manage.py           Django management command entry point
```

## Development

Run the Django test suite with:

```bash
python manage.py test
```

The project uses SQLite by default. The local database file is created in the project root after running migrations.

When you are done, leave the virtual environment with:

```bash
deactivate
```
