Here is the updated README.md content including HTTPS setup instructions:

# Nginx Docker Compose Setup (HTTP + HTTPS)

This project runs a production-ready Nginx container using Docker Compose, serving static files from a custom directory with optional HTTPS support.

## Project Structure

your-project/ ├── docker-compose.yml ├── nginx.conf ├── certs/ │ ├── nginx.crt │ └── nginx.key └── data/ └── index.html

- `docker-compose.yml`: Docker Compose configuration. - `nginx.conf`: Custom Nginx configuration file, sets the root directory and HTTPS. - `certs/`: Directory containing SSL certificate and key files. - `data/`: Directory containing your static website files. ## Usage ### HTTP only 1. Place your static files (e.g., `index.html`) inside the `data` directory. 2. Customize `nginx.conf` if needed (for HTTP only, remove HTTPS server block). 3. Run the container: ```sh docker compose up -d
Access your site at http://localhost⁠.
Enable HTTPS (Self-signed certificates)
Generate self-signed certificates:
mkdir -p certs
openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
  -keyout certs/nginx.key -out certs/nginx.crt \
  -subj "/CN=localhost"
Use the provided nginx.conf with HTTPS server block.
Run the container:
docker compose up -d
Access your site at https://localhost⁠ (browser will warn about self-signed cert).
Notes
The data directory is mounted as /data inside the container.
The custom nginx.conf configures Nginx to serve files from /data and handle HTTPS.
The container restarts automatically on failure or host reboot (restart: always).
For production, use valid SSL certificates (e.g., from Let's Encrypt).
Customization
To change the served directory or Nginx settings, edit nginx.conf and update the volume mounts in docker-compose.yml accordingly.