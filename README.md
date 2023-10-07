# hw-3-Microservice-Orchestration

## Steps to Run it on local

1. Begin by installing Docker Desktop and launching it on your MacBook.
 - Ensure that no containers are currently active, as this will prevent any ports from being in use by existing containers.
2. Clone the git repository: https://github.com/rinormaloku/k8s-mastery
3. Launch a terminal and proceed to clone the repository:
 - Execute the following command: git clone https://github.com/rinormaloku/k8s-mastery
4. Open additional terminals on your MacBook (each one for the sa-webapp, sa-logic and sa-frontend):
5. Access the recently cloned repository by entering: cd k8-mastery
6. Goto Terminal-1, sa-webapp:
   - Verify that JDK8 is installed on your system.
   - Navigate to the "sa-webapp" directory using the command: cd sa-webapp
   - Install Maven to generate the "target" folder: mvn install
   - Go into the newly created "target" folder: cd target
   - Start the java application: java -jar sentiment-analysis-web-0.0.1-SNAPSHOT.jar --sa.logic.api.url=http://localhost:5000
7. Goto Terminal-2, sa-logic:
   - Ensure that Python3 is installed on your computer.
   - Next, navigate to the "sa-logic/sa" directory: cd sa-logic/sa
   - Execute the following commands in this directory:
       - python3 -m pip install -r requirements.txt
       - python3 -m textblob.download_corpora
   - If you encounter Flask and Jinja2 errors, you may need to run the following commands to resolve them:
       - python3 -m pip uninstall Flask jinja2
       - python3 -m pip install Flask jinja2
   - Repeat the above commands until all the errors are gone.
   - Before running the sentiment_analysis.py file to avoid CORS-related errors, make the following changes:
       - Add a decorator to the method. After making the necessary changes, you can execute the sentiment_analysis.py file using the following command:
       - python3 sentiment_analysis.py
8. Goto Terminal-3, sa-frontend:
   - Ensure that you have Node>18 installed on your machine.
   - Navigate to the "sa-frontend" folder: cd sa-frontend
   - Install the required npm packages: npm i
   - Build the application. This will create a "build" folder: npm run build
   - Start the application: npm start

