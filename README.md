# Step-by-Step Documentation

#### Step 1: Installed Docker
- Downloaded Docker from the official [Docker website](https://www.docker.com/get-started) and installed it on the local machine.

#### Step 2: Cloned the Sample Web Application
- Used Git to clone the sample web application repository from GitHub.
  ```sh
  git clone https://github.com/agrimgautam/sit323-2024-t1-prac5p.git
  cd sit323-2024-t1-prac5p
  ```

#### Step 3: Created a Dockerfile
- Created a `Dockerfile` in the root directory of the project. The Dockerfile included instructions to use the Node.js base image, set the working directory, copy necessary files, install dependencies, expose the application port, and define the command to run the application.
  ```dockerfile
    # Use the official Node.js image as the base image
    FROM node:18.20.2

    # Set the working directory in the container
    WORKDIR /

    # Copy package.json and package-lock.json to the working directory
    COPY package*.json ./

    # Install dependencies
    RUN npm install

    # Copy the rest of the application code to the working directory
    COPY . .

    # Expose port 3000
    EXPOSE 3000

    # Command to run the application
    CMD ["node", "index.js"]
  ```

#### Step 4: Built the Docker Image
- Used the `docker build` command to build the Docker image from the Dockerfile.
  ```sh
  docker build -t agrimgautam/sit323-2024-t1-prac5p .
  ```

#### Step 5: Created a Docker Compose File
- Created a `docker-compose.yml` file in the project directory to define the services for the application.
  ```yaml
    version: '3'
    services:
    web:
        build: .
        ports:
          - "3000:3000"
  ```

#### Step 6: Started the Docker Compose Environment
- Started the application using Docker Compose with the `docker-compose up` command.
  ```sh
  docker-compose up
  ```

#### Step 7: Tested the Application
- Opened a web browser and navigated to `http://localhost:3000` to verify that the application was running correctly.

#### Step 8: Pushed the Docker Image to a Registry
- Logged into Docker Hub, tagged the Docker image, and pushed it to the Docker repository.
  ```sh
  docker login
  docker tag agrimgautam/sit323-2024-t1-prac5p agrimgautam/sit323-2024-t1-prac5p:latest
  docker push agrimgautam/sit323-2024-t1-prac5p:latest
  ```

To publish your microservice to a private container registry on Google Cloud, follow these steps:

### 1. Create a Private Container Registry on Google Cloud

1. **Set up Google Cloud SDK:**
   - If you don't already have the Google Cloud SDK installed, download and install it from [here](https://cloud.google.com/sdk/docs/install).

2. **Initialize the Google Cloud SDK:**
   - Open a terminal and run:

     ```sh
     gcloud init
     ```

3. **Create a Google Container Registry (GCR) bucket:**
   - GCR uses Google Cloud Storage buckets to store images. The GCR registry name is based on the region. For example:
     - `gcr.io` (multi-region)
     - `us.gcr.io` (us region)
     - `eu.gcr.io` (eu region)
     - `asia.gcr.io` (asia region)

   - Create a bucket using the following command (assuming `gcr.io` for a multi-region setup):

     ```sh
     gcloud services enable containerregistry.googleapis.com
     ```

### 2. Authenticate with the Registry

1. **Authenticate Docker with your Google Cloud account:**

   ```sh
   gcloud auth configure-docker
   ```

   This command updates your Docker configuration to use the Google Cloud credentials for authentication.

### 3. Build and Tag Your Docker Image

1. **Build your Docker image:**
   - Make sure you are in the directory containing your `Dockerfile`.

   ```sh
   docker build -t sit323-5d-app:v1 .
   ```

2. **Tag the Docker image for your registry:**
   - Replace `meta-chassis-424710-r6` with your Google Cloud project ID. The project ID can be found in the Google Cloud Console.

   ```sh
   docker tag sit323-5d-app:v1 gcr.io/meta-chassis-424710-r6/sit323-5d-app:v1
   ```

### 4. Publish the Docker Image

1. **Push the Docker image to your Google Container Registry:**

   ```sh
   docker push gcr.io/meta-chassis-424710-r6/sit323-5d-app:v1
   ```

   This command uploads your Docker image to the specified Google Container Registry.

### 5. Verify the Published Image

1. **Run the Docker image from your Google Container Registry:**

   ```sh
   docker run -d -p 8080:8080 gcr.io/meta-chassis-424710-r6/sit323-5d-app:v1
   ```

2. **Check that your microservice is running:**
   - Open a web browser and navigate to `http://localhost:8080`.
   - You should see your application running and accessible via the specified port.

### Summary

Here is a summarized list of commands to follow:

```sh
# Step 1: Enable GCR (only needed once)
gcloud services enable containerregistry.googleapis.com

# Step 2: Authenticate Docker with GCR
gcloud auth configure-docker

# Step 3: Build and tag the Docker image
docker build -t sit323-5d-app:v1 .
docker tag sit323-5d-app:v1 gcr.io/meta-chassis-424710-r6/sit323-5d-app:v1

# Step 4: Push the Docker image to GCR
docker push gcr.io/meta-chassis-424710-r6/sit323-5d-app:v1

# Step 5: Run the image to verify it
docker run -d -p 8080:8080 gcr.io/meta-chassis-424710-r6/sit323-5d-app:v1
```

By following these steps, you'll have your microservice published to a private container registry on Google Cloud and verified that it can run from the published image.