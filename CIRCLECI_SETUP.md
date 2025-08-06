# CircleCI Setup Guide

## Environment Variables Required

To use this CircleCI configuration, you need to set up the following environment variables in your CircleCI project settings:

### 1. Go to CircleCI Project Settings

- Navigate to your project in CircleCI
- Go to **Project Settings** → **Environment Variables**

### 2. Add the following environment variables:

| Variable Name        | Description                              | Example                  |
| -------------------- | ---------------------------------------- | ------------------------ |
| `DOCKERHUB_USERNAME` | Your Docker Hub username                 | `fernandobdaf`           |
| `DOCKERHUB_PASSWORD` | Your Docker Hub password or access token | `your-password-or-token` |

### 3. Docker Hub Access Token (Recommended)

Instead of using your Docker Hub password, create an access token:

1. Go to [Docker Hub](https://hub.docker.com/)
2. Navigate to **Account Settings** → **Security**
3. Click **New Access Token**
4. Give it a name like "CircleCI Integration"
5. Copy the token and use it as `DOCKERHUB_PASSWORD`

## What the Pipeline Does

### 1. Build and Test Job

- Installs all dependencies for all services
- Runs tests for all services
- Only runs on the `main` branch

### 2. Build and Push Job

- Logs in to Docker Hub
- Builds Docker images for all 4 services:
  - `udagram-api-feed`
  - `udagram-api-user`
  - `udagram-frontend`
  - `udagram-reverseproxy`
- Tags images with both:
  - Git commit SHA (`$CIRCLE_SHA1`)
  - `latest` tag
- Pushes all images to Docker Hub
- Only runs after successful tests
- Only runs on the `main` branch

## Image Names

Your images will be pushed to Docker Hub as:

- `your-username/udagram-api-feed:latest`
- `your-username/udagram-api-feed:commit-sha`
- `your-username/udagram-api-user:latest`
- `your-username/udagram-api-user:commit-sha`
- `your-username/udagram-frontend:latest`
- `your-username/udagram-frontend:commit-sha`
- `your-username/udagram-reverseproxy:latest`
- `your-username/udagram-reverseproxy:commit-sha`

## Usage

Once set up, every push to the `main` branch will:

1. ✅ Install dependencies
2. ✅ Run all tests
3. ✅ Build all Docker images
4. ✅ Push to Docker Hub

## Troubleshooting

- Make sure your Docker Hub credentials are correct
- Ensure you have write access to your Docker Hub account
- Check that all Dockerfiles are properly configured
- Verify that the `main` branch is your default branch
