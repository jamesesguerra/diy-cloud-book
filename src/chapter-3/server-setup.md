# Setting up your Server
Before we start deploying apps, we need to prepare the server itself. This involves updating the system, applying basic security measures, setting up SSH for remote access, and installing Docker as the platform for running applications. Taking care of these essentials first will make everything else more stable and easier to manage.

## Housekeeping
Once you have a Linux server, it's a good idea to do some housekeeping before we start anything else.

Keep repositories and system packages updated
```sh
sudo apt-get update && apt upgrade -y
```

Install some packages you might need for debugging / editing later on
```sh
sudo apt-get install -y curl && \
sudo apt-get install -y vim && \
sudo apt-get install -y nano
```
