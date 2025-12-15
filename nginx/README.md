Instructions:

Create a directory called html in the same location as your docker-compose.yml and put your static files (e.g., index.html) there.
Run:
docker compose up -d
Access your site at http://localhost⁠.
Notes:

For custom Nginx configs, add another volume: - ./nginx.conf:/etc/nginx/nginx.conf:ro
The restart: always ensures Nginx restarts if the container or host reboots.
Sources:

https://docs.docker.com/get-started/docker-concepts/running-containers/multi-container-applications/⁠

