# running-nginx-on-docker

Description:
Dockerizing a basic web application using Docker and Docker Compose. 
The web application consists of a single HTML file with associated CSS and JavaScript files.

1. Create directory
	mkdir web_application

2. Create Dockerfile
	vim Dockerfile

	##Dockerfile
	FROM nginx:latest	# Use nginx official image
	EXPOSE 80			# Expose port 80 to port 8080
	WORKDIR /app		# Set a working directory
	COPY . /app			# Copy file into the container

3. Create volume
	docker volume create --name web-volume

4. Create docker-compose.yml
	vim docker-compose.yml
	  
##docker-compose.yml
version: '3'
services:
  web:
    image: nginx:latest
    volumes:
      - web-volume:/var/lib/docker/volumes/web-volume/_data
    ports:
      - ${APP_PORT}:80	#env var
	deploy:
      resources:
        limits:
          cpus: 0.50
          memory: 512M
        reservations:
          cpus: 0.25
          memory: 128M

volumes:
  web-volume:
    external: true

5. Set up default port
	vim .env

	## .env file
	APP_PORT=80

6. Build docker image
	docker build -t webapp .

7. Run the container
	docker-compose up -d

8. Connect to container
	docker exec -it 60bf445a11a0 sh

9. Go to nginx directory
	cd /usr/share/nginx/html

10. Rename index.html
	 mv index.html index2.html
	 
11. Exit container
	 exit

12. Go to volume directory
	 cd /var/lib/docker/volumes/web-volume/_data

13. Clone github repository
	 git clone https://github.com/designmodo/html-website-templates.git

14. Change directory
	 cd html-website-templates/'Horizontal Scroll One Page Template Website'

15. Move files to nginx folder
	 mv -t /var/lib/docker/volumes/web-volume/_data _first-steps.url assets js scss _open-generator.url css manual ajax-email.php index.html 'readme first.txt'

16. Access on browser
