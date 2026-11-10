# CloudCart – Containerized E-Commerce Website & Jenkins CI/CD

Responsive sample storefront packaged with Docker and served by Nginx. Jenkins checks out the GitHub source, builds an image, pushes it to Docker Hub, and deploys the container on the Jenkins EC2 host.

## Architecture
GitHub `main` → Jenkins → Docker build → Docker Hub → EC2 Docker container → Nginx storefront on port 8081.

## Run locally
```bash
docker build -t cloudcart:local .
docker run --rm -p 8081:80 cloudcart:local
```
Open http://localhost:8081. Or run `docker compose up --build`.

## Jenkins setup
1. Install Java, Git, Docker and Jenkins on Amazon Linux EC2.
2. Give the Jenkins service account Docker access and verify Docker commands work from a build.
3. Create a Pipeline job connected to this repo and `main`.
4. Add a Jenkins username/password credential with ID `dockerhub-creds`; use a Docker Hub access token as the password.
5. Replace `YOUR_DOCKERHUB_USERNAME` in `Jenkinsfile`.
6. Restrict EC2 ingress: SSH/Jenkins only from trusted IPs; port 8081 only for intended clients.

## Files
- `index.html`, `css/`, `js/`: storefront UI
- `Dockerfile`: Nginx container
- `Jenkinsfile`: checkout, build, push and deploy stages
- `docker-compose.yml`: local runtime

## Scope and security
This is a frontend demo. Cart interaction is client-side; payment, inventory, authentication and order processing are not implemented. Never commit credentials, tokens, private keys or `.env` files. Prefer an EC2 IAM role over stored AWS keys. Add HTTPS, image scanning, rollback and production monitoring before real use.
