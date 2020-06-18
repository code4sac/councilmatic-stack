# councilmatic-stack

The goal of this project is to get the imago project, scraper-us-municipal project, and councilmatic-starter-template all working together.
![IMG_20190619_200810](https://user-images.githubusercontent.com/4978032/59816096-a5db2980-92cf-11e9-8f64-ee62fcf5f610.jpg)

## Requirements

1. Install docker an docker-compose if you do not have them installed
2. Clone this scrapers project into the the folder `scrapers` in this project: https://github.com/feydan/scrapers-us-municipal.
3. Clone this sacramento-councilmatic project into the folder `sacramento-councilmatic` into this project: https://github.com/code4sac/sacramento-councilmatic and switch to the `councilmatic-stack` branch
4. Run the initial cache table creation `docker-compose exec councilmatic python manage.py createcachetable`

## Initializing

1. Run `docker-compose up` to start the database and scrapers containers. Keep this terminal window running.
2. Run the initial migration for scrapers `docker-compose exec scrapers pupa dbinit us`
3. Run the initial migration for councilmatic `docker-compose exec councilmatic python manage.py migrate`
4. In the `sacramento-councilmatic/councilmatic` folder, copy `settings_deployment.py.example` to `settings_deployment.py`, and when developing locally change the `DEBUG = False` line to `DEBUG = True`

## Running the scrapers

1. Ensure the containers are running. If they are still running from the Initializing step above continue to step 2. Otherwise start the containers: `docker-compose up`.
2. `docker-compose exec scrapers /bin/bash` (ssh's into the scrapers project)
3. `pupa update sacramento` (runs the update script)
4. `exit` ssh into scrapers

## Accessing the web application

The web application is accessible at http://localhost:8001/ in your browser.

## Accessing the database

`docker-compose exec postgresql psql opencivicdata pupa`

## Todo

1. Fix bootstrapping so that you do not need to run the init scripts and have the update script automatically run on a cron job

## Resources

Docker stuff: https://docs.docker.com/compose/django/#create-a-django-project

Open civic data api: https://github.com/opencivicdata/imago

Scrapers US Municipal: https://github.com/opencivicdata/scrapers-us-municipal/pull/243

Councilmatic: https://github.com/datamade/councilmatic-starter-template,
