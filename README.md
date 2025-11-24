# job-tracker-app-api (WIP)
Job tracker API project.
> The goal of this project is to build a job search application that fetches job listings that will intergrate with external job search APIs (e.g., Indeed, Adzuna). With email notifications as soon as the listing is live.

> This will allow users to browse, filter, and save job listings without visiting several job search sites.

## Features
- Provide a full list of jobs from an API call.
- Authorization & Authentication for exisiting users and the feature of new users registering.
- Basic user information is stored securely within a database.
- Search, filter by and save job listings.

## Tech Stack
**Frontend:**

**Backend:**
- Python 3.11.5
- Django>=3.2.4,<3.3

**Database:**
- PostgreSQL

**Other:**
- Docker version 28.5.1, build e180ab8
- flake8>=3.9.2,<3.10
- psycopg2>=2.8.6,<2.9

## Installation Instructions
- Step-by-step setup:

**Clone the repository**
```
git clone https://github.com/tom-williams26/job-tracker-app-api.git
cd project-directory


**Create the virtual environment**
```
python -m venv venv
venv\Scripts\activate   # Windows


**Build Docker image**

Reads dockerfile for the services outlined.
Installs dependencies, copies files and sets up layers.
Creates the images ahead of time, but doesn't start the containers.

*Both work for this application*
- Docker Compose v1: `docker-compose build`
- Docker Compose v2: `docker compose build`

**Docker Container setup**
Check for any existing images.
Builds the images if neccessary and starts the containers.
Starts the containers as per the compose file. Ensure the latest build is running.

*Both work for this application*
- Docker Compose v1: `docker-compose up --build`
- Docker Compose v2: `docker compose up --build`

**Database Setup**

- With PostgreSQL running in a docker container, the database still needs to be initialize the database.
*Within the docker container*
- Only needed if changes are made to the models locally `docker-compose run --rm app sh -c "python manage.py makemigrations"`
- Applies all migrations in the repo to the database but not before waiting for the database to be live `docker-compose run --rm app sh -c "python manage.py wait_for_db & python manage.py migrate""`

- For Admin access `docker-compose run --rm app sh -c "python manage.py createsuperuser"`

**Install Development Dependencies (only if running locally)**
*Docker will handle the following if running locally*
```
pip install -r requirements.txt
pip install -r requirements.dev.txt


**Run Tests (Optional)**
`docker-compose run --rm app sh -c "python manage.py test"`
or to check for tests and linting issues
`docker-compose run --rm app sh -c "python manage.py test & flake8"`

