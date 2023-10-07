# hw-3-Microservice-Orchestration

## Steps to Run it on Locally

1. Begin by installing Docker Desktop and launching it on your MacBook.
 - Ensure that no containers are currently active, as this will prevent any ports from being in use by existing containers.
2. Clone the git repository: `https://github.com/rinormaloku/k8s-mastery`
3. Launch a terminal and proceed to clone the repository:
 - Execute the following command: `git clone https://github.com/rinormaloku/k8s-mastery`
4. Open additional terminals on your MacBook (each one for the sa-webapp, sa-logic and sa-frontend):
5. Access the recently cloned repository by entering: `cd k8-mastery`
6. Goto Terminal-1, sa-webapp:
   - Verify that JDK8 is installed on your system.
   - Navigate to the "sa-webapp" directory using the command: `cd sa-webapp`
   - Install Maven to generate the "target" folder: `mvn install`
   - Go into the newly created "target" folder: `cd target`
   - Start the java application: `java -jar sentiment-analysis-web-0.0.1-SNAPSHOT.jar --sa.logic.api.url=http://localhost:5000`
7. Goto Terminal-2, sa-logic:
   - Ensure that Python3 is installed on your computer.
   - Next, navigate to the "sa-logic/sa" directory: `cd sa-logic/sa`
   - Execute the following commands in this directory:
       - `python3 -m pip install -r requirements.txt`
       - `python3 -m textblob.download_corpora`
   - If you encounter Flask and Jinja2 errors, you may need to run the following commands to resolve them:
       - `python3 -m pip uninstall Flask jinja2`
       - `python3 -m pip install Flask jinja2`
   - Repeat the above commands until all the errors are gone.
   - Before running the sentiment_analysis.py file to avoid CORS-related errors, make the following changes:
       - `from flask_cors import CORS, cross_origin`
       - `cors = CORS(app , resources={r"/analyse/sentiment": {"origins": "*"}})`
       - Add a decorator to the method. `@cross_origin(origin='*')`
       - After making the necessary changes, you can execute the sentiment_analysis.py file using the following command:
       - `python3 sentiment_analysis.py`
8. Goto Terminal-3, sa-frontend:
   - Ensure that you have Node>18 installed on your machine.
   - Navigate to the "sa-frontend" folder: `cd sa-frontend`
   - Install the required npm packages: `npm i`
   - Build the application. This will create a "build" folder: `npm run build`
   - Start the application: `npm start`

## Build and Push to DockerHub

1. Open Terminal-1, sa-webapp:
   - Make sure you are in the sa-webapp folder, or else do: `cd ..`
   - Run the following command for build: `docker build -t hnikhar/sentiment-analysis-webapp:latest .`
   - Run the following command for push: `docker push hnikhar/sentiment-analysis-webapp:latest`
2. Repeat the same commands. Open Terminal-2, sa-logic:
   - Make sure you are in the sa-logic folder, or else do: `cd ..`
   - Run the following command for build: `docker build -t hnikhar/sentiment-analysis-logic:latest .`
   - Run the following command for push: `docker push hnikhar/sentiment-analysis-logic:latest`
3. Repeat the same commands. Open Terminal-3, sa-frontend:
   - Run the following command for build: `docker build -t hnikhar/sentiment-analysis-frontend:latest .`
   - Run the following command for push: `docker push hnikhar/sentiment-analysis-frontend:latest`

## Kubernetes on Cloud

# Google Cloud Setup:
1. Log in to console.cloud.google.com.
2. Turn on Billing Account.
3. Navigate to Google Kubernetes Engine.
4. Create a cluster (switch to Standard).
5. Give it an appropriate name.
6. Select a Region and click "Create." Wait for about 5 minutes.
7. Once the cluster is created, click on the three dots and select "Connect."
8. Copy the command mentioned in the window to connect to the cluster.

# Cloud Terminal Setup:
1. Open Cloud Terminal.
2. Paste the cluster connect command copied earlier.
3. Pull the web app and logic Docker images:
  - `docker pull hnikhar/sentiment-analysis-webapp:latest`
  - `docker pull hnikhar/sentiment-analysis-logic:latest`
4. Tag these images:
  - `docker tag hnikhar/sentiment-analysis-webapp:latest gcr.io/vertical-shore-398902/hnikhar/sentiment-analysis-webapp:latest`
  - `docker tag hnikhar/sentiment-analysis-logic:latest gcr.io/vertical-shore-398902/hnikhar/sentiment-analysis-logic:latest`
5. Push these tagged images to Google Cloud Registry:
  - `docker push gcr.io/vertical-shore-398902/hnikhar/sentiment-analysis-webapp:latest`
  - `docker push gcr.io/vertical-shore-398902/hnikhar/sentiment-analysis-logic:latest`

