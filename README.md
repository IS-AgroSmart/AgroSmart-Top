# AgroSmart-Top
The top-level repository for the AgroSmart/DroneApp web application.

This repository aims to simplify the deployment of the application, by including some top-level files which must be included one level above the source code which is on [IS-AgroSmart](https://github.com/IS-AgroSmart)/[AgroSmart-Web](https://github.com/IS-AgroSmart/AgroSmart-Web).

## First-time usage

1. Clone this repo with `git clone --recurse-submodules https://github.com/IS-AgroSmart/AgroSmart-Top ~/AgroSmart`.

2. Create the file `AgroSmart/app/IngSoft1/settings.ini` file and fill it with the required secrets. Only The Chosen Ones ~~should~~ will have access to the file.

3. To run the app, `cd` into the directory, and run `PREFIX=$(pwd) docker-compose up`. Repeat any time the app must be started.

4. Create a starting admin user: run `docker exec -it container-django /bin/sh`. On the container console:

   * Run  `python3 manage.py migrate`

   * Run `python3 manage.py createsuperuser` and provide the required credentials (username `admin`, email and password shall be determined by use of rational thought)

5. (TODO) Any additional, one-time-only steps. To check:

   * Set up the gradient style on Geoserver
   * Somehow send the gradient image to the Geoserver volume???

## Not-first-time usage

1. `cd ~/AgroSmart`
2. `PREFIX=$(pwd) docker-compose up`

## // TODO

* Verify setup steps.
* Maybe add a Bash script that can be run from a clean install of Ubuntu Server. It should automatically install any required programs and get the app ready for launch. Bonus: use https://www.digitalocean.com/community/tutorials/automating-initial-server-setup-with-ubuntu-18-04 and OVH Horizon's "Script Data" (https://docs.ovh.com/gb/en/public-cloud/create-an-instance-in-horizon/) to execute the Bash script when creating the image.
* Do something about automatically running the app on boot, and separating its stdin/stdout from any specific shell.

