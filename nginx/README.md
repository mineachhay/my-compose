# Nginx Docker Compose Setup

This project runs a production-ready Nginx container using Docker Compose, serving static files from a custom directory.

## Project Structure

your-project/ 
├── docker-compose.yml 
├── nginx.conf 
    └── data/ 
    └── index.html

- `docker-compose.yml`: Docker Compose configuration. - `nginx.conf`: Custom Nginx configuration file, sets the root directory to `/data`. - `data/`: Directory containing your static website files. ## Usage 1. Place your static files (e.g., `index.html`) inside the `data` directory. 2. Customize `nginx.conf` if needed. 3. Run the container: ```sh docker compose up -d
Access your site at http://localhost⁠.
Notes
The data directory is mounted as /data inside the container.
The custom nginx.conf configures Nginx to serve files from /data.
The container restarts automatically on failure or host reboot (restart: always).
Customization
To change the served directory or Nginx settings, edit nginx.conf and update the volume mounts in docker-compose.yml accordingly.