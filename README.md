# AgroSmart-Top
The top-level repository for the AgroSmart/DroneApp web application.

This repository aims to simplify the deployment of the application, by including some top-level files which must be included one level above the source code which is on [IS-AgroSmart](https://github.com/IS-AgroSmart)/[AgroSmart-Web](https://github.com/IS-AgroSmart/AgroSmart-Web).

## Pre-install steps
1. Update the OS.
2. Install Git, Docker, Docker Compose and NPM.

## First-time usage

1. Clone this repo with `git clone --recurse-submodules https://github.com/IS-AgroSmart/AgroSmart-Top ~/AgroSmart`.
2. Change to the `deploy` branch: `cd ~/AgroSmart; git checkout deploy`.
3. Install all NPM dependencies on the `app/frontend` directory by running `cd ~/AgroSmart/app/frontend; npm install`.
4. Create the file `~/AgroSmart/.env` and fill it with the required secrets. Only The Chosen Ones ~~should~~ will have access to the file.
5. To run the app, `cd` into the `~/AgroSmart` directory, and run `docker-compose up`. Repeat any time the app must be started.
6. Create a starting admin user: run `docker exec -it container-django /bin/sh`. On the container console:

   * Run  `python3 manage.py migrate`

   * Run  `python3 manage.py collectstatic`

   * Run `python3 manage.py createsuperuser` and provide the required credentials (username `admin`, email and password shall be determined by use of rational thought)

5. Set up the gradient style on Geoserver, to be used by the indices. To do so:

   1. Visit `<ip>/geoserver/geoserver/web`, log in to Geoserver, click on "Styles" on the left bar.
   2. Create a new style, which must be called exactly `gradient`. Leave the workspace blank and the format as SLD, as default.
   3. Enter the contents of [gradient.xml](gradient.xml) in the text box.
   4. Click the Save button at the bottom of the form.
6. Upload the gradient legend to the Geoserver container: run `docker cp gradient.png container-geoserver:/opt/geoserver/data_dir/styles/gradient.png`

## Not-first-time usage

1. `cd ~/AgroSmart`
2. `docker-compose up`

## Updating the source code

1. Stop the containers by attaching to their terminal session and pressing Ctrl+C.
2. Make sure that you are in the `~/AgroSmart` directory (which you should be, if you are in the same terminal that was running the app).
3. Run `git pull --recurse-submodules`.
4. Run the server again with `PREFIX=$(pwd) docker-compose up`.

## // TODO

* Verify setup steps.
* Maybe add a Bash script that can be run from a clean install of Ubuntu Server. It should automatically install any required programs and get the app ready for launch. Bonus: use https://www.digitalocean.com/community/tutorials/automating-initial-server-setup-with-ubuntu-18-04 and OVH Horizon's "Script Data" (https://docs.ovh.com/gb/en/public-cloud/create-an-instance-in-horizon/) to execute the Bash script when creating the image.
* Do something about automatically running the app on boot, and separating its stdin/stdout from any specific shell.

