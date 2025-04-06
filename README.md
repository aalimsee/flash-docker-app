


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


# Testing
To test your GitHub Actions workflow for building and pushing the Docker image to DockerHub, follow these steps:

1. Verify Your Repository and Files
Make sure the following files are correctly committed and pushed to your GitHub repository:

app.py (Flask application)

requirements.txt (Python dependencies)

Dockerfile (for creating the Docker image)

.github/workflows/docker-build.yml (GitHub Actions workflow)

2. Push Code to Trigger the Workflow
Make a change in any of your files (like updating the app.py or adding comments), or you can simply commit an empty change (e.g., a minor tweak in the README.md).

After making the change, run the following commands to commit and push to the main branch:

```git add .
git commit -m "Trigger build and push workflow"
git push origin main
```
3. Check GitHub Actions
Go to your GitHub repository.

Click on the "Actions" tab at the top.

You should see your workflow run under the "Docker Build and Push" name.

Click on the latest workflow run to see the progress and details of the build and push process.

If everything is set up correctly, the GitHub Actions log will show steps like:

Checking out the code.

Logging into DockerHub.

Setting up Docker Buildx.

Building and pushing the Docker image to your DockerHub account.

4. Verify on DockerHub
After the workflow completes successfully, go to your DockerHub account:

Log in to DockerHub at https://hub.docker.com/.

Check the Repositories section.

You should see the flask-docker-app repository with the latest tag (e.g., latest).

You can also pull the image and run it locally to verify that the Docker image works correctly:

```
docker pull yourdockerhubusername/flask-docker-app:latest
docker run -p 5000:5000 yourdockerhubusername/flask-docker-app:latest
```
This should start your Flask app on port 5000 locally.

5. Troubleshooting
If the workflow fails:

Go to the Actions tab and click on the failed workflow to see the logs.

The logs will show which step failed (e.g., docker/login-action or docker/build-push-action).

Ensure your DockerHub credentials are correctly set in GitHub Secrets (DOCKER_USERNAME and DOCKER_PASSWORD).

Ensure the Dockerfile, app.py, and requirements.txt are valid.

# Docker pull for Mac
```- name: Build and push Docker image
  uses: docker/build-push-action@v6
  with:
    context: .
    push: true
    platforms: linux/amd64,linux/arm64 # <<< include for MacOS>>>
    tags: ${{ secrets.DOCKER_USERNAME }}/flask-docker-app:latest```
