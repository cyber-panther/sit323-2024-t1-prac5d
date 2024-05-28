
---

# Deployment to Google Cloud Container Registry
## SIT323 Task 5.3D

### 1. Create a Private Container Registry

1. **Enable Container Registry API:**

   ```sh
   gcloud services enable containerregistry.googleapis.com
   ```

### 2. Authenticate with the Registry

1. **Configure Docker to use Google Cloud credentials:**

   ```sh
   gcloud auth configure-docker
   ```

### 3. Build and Tag Your Docker Image

1. **Build the Docker image:**

   ```sh
   docker build -t sit323-5d-app:v1 .
   ```

2. **Tag the Docker image for your registry:**

   ```sh
   docker tag sit323-5d-app:v1 gcr.io/my-project-id/sit323-5d-app:v1
   ```

### 4. Publish the Docker Image

1. **Push the Docker image to your registry:**

   ```sh
   docker push gcr.io/my-project-id/sit323-5d-app:v1
   ```

### 5. Verify the Published Image

1. **Run the image locally to verify:**

   ```sh
   docker run -d -p 3000:3000 gcr.io/my-project-id/sit323-5d-app:v1
   ```

### Screenshot Suggestions

1. **Enabling Container Registry API:**
   - Google Cloud Console page showing the API being enabled.
   
2. **Configuring Docker Authentication:**
   - Terminal output confirming Docker configuration with Google Cloud credentials.

3. **Building the Docker Image:**
   - Terminal showing the Docker build process with no errors.

4. **Tagging the Docker Image:**
   - Terminal output showing the command and result of tagging the Docker image.

5. **Pushing the Docker Image:**
   - Terminal output showing the image being pushed to Google Container Registry.

6. **Running the Docker Container:**
   - Terminal showing the running container.
   - Browser screenshot accessing the application at `http://localhost:8080`.

By following this guide and including the suggested screenshots, you'll have a comprehensive README file to assist others in publishing their microservice to Google Cloud.

Here's an enhanced README file with detailed explanations of each step and the reasons behind them:

### Explanation of Each Step

1. **Enable Container Registry API:**
   - This step activates the Container Registry service in your Google Cloud project, allowing you to store and manage Docker images.

2. **Authenticate with the Registry:**
   - Configuring Docker to use Google Cloud credentials ensures secure communication between your local Docker client and GCR.

3. **Build and Tag Your Docker Image:**
   - Building the image packages your application into a container. Tagging it with the registry URL prepares it for upload.

4. **Publish the Docker Image:**
   - Pushing the image uploads it to GCR, making it available for deployments and other uses.

5. **Verify the Published Image:**
   - Running the image locally ensures it functions correctly, confirming a successful upload to GCR.