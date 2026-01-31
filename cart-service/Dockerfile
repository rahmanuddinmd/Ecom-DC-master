FROM ubuntu
RUN apt update -y
RUN apt install apache2 -y  #Installs Apache2 web server in the container
COPY index.html /var/www/html
CMD ["/usr/sbin/apachectl", "-D", "FOREGROUND"]  #This line ensures Apache is the main process of the container.

# apachectl is a control script for Apache (start/stop/reload).

# -D FOREGROUND tells Apache not to daemonize (i.e., not run in the background), but instead stay in the foreground.

# Why? Because in Docker, if the main process exits, the container stops. Running in the foreground keeps the container alive.
