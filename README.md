


# flash-docker-app
3.3 Introduction to Containerisation

# Steps
1. Create a Public Repository in GitHub
2. Commit Your Flask App
    - app.py
    - requirements.txt
    - Dockerfile
3. Push your code to GitHub
4. Set Up GitHub Actions Workflow
    - .github/workflows
        - docker-build.yaml

# Key Points
- This workflow triggers on any push to the main branch.
- It uses GitHub Secrets for DockerHub credentials. You need to add your DockerHub username and password to GitHub Secrets (explained below).
- It builds and pushes your Docker image to your DockerHub registry.

Add GitHub Secrets for DockerHub Credentials:
- Go to your GitHub repository.
- Navigate to Settings > Secrets and Variables > Actions.
- Click New repository secret.
- Add the following secrets:
    - DOCKER_USERNAME: Your DockerHub username.
    - DOCKER_PASSWORD: Your DockerHub password or personal access token.

# use the GitHub CLI (gh) to add secrets to your repository
gh secret set DOCKER_USERNAME --repo <your-username>/<your-repo> --body "<your-dockerhub-username>"
gh secret set DOCKER_PASSWORD --repo <your-username>/<your-repo> --body "<your-dockerhub-password-or-access-token>"


