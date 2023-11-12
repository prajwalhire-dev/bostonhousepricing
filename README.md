# Boston House Pricing Prediction.
### Software and tools required

1. [Github Account](https://github.com)
2. [VS Code IDE](https://code.visualstudio.com/)
3. [HerokuAccount](https://heroku.com)
4. [Git CLI](https://git-scm.com/book/en/v2/Getting-Started-The-Command-Line)


## Setting Up the Environment

To recreate the project's environment, follow these steps:

```
# Create a new environment
conda create -p venv python==3.10 -y

# Activate the environment on Windows
conda activate venv/

# Activate the environment on macOS and Linux
source activate venv/
```
## Preparing the Machine Learning Model
The model and the scaler are serialized into pickle files using the following commands within the Jupyter Notebook:

```
import pickle

# Save the scaler
pickle.dump(scaler, open('scaling.pkl', 'wb'))

# Save the regression model
pickle.dump(regression, open('regmodel.pkl', 'wb'))

# Load the regression model
pickled_model = pickle.load(open('regmodel.pkl', 'rb'))

```

## The Flask Web Application
A Flask web application is developed to serve the machine learning model's predictions over the web. The application has the following routes:
```
@app.route('/'): #Serves the home page of the web application.
@app.route('/predict_api', methods=['POST']): #API endpoint to receive JSON data and return the prediction as JSON.
@app.route('/predict', methods=['POST']): #Endpoint for form submissions, which returns the prediction on the home page.
```

## Deployment on Heroku
Two methods are used for deploying the web application on Heroku:

1. GitHub Integration: The web application is deployed by connecting the GitHub repository to Heroku, which enables automatic deployment on every push to the repository.
2. Docker Containerization: A Dockerfile is created for the project, and GitHub Actions is used to set up CI/CD pipelines for deployment.


## Dockerfile Contents
The Dockerfile is designed to:

* Use Python 3.10.0 as the base image.
* Copy the application files into the /app directory in the Docker container.
* Set the /app directory as the working directory.
* Install the required dependencies from requirements.txt.
* Expose the port specified by the $PORT environment variable.
* Start the application using gunicorn.


## Requirements File
The Python dependencies required for this project are listed in the requirements.txt file, which you can install using:

`pip install -r requirements.txt`

## Running the Application Locally
To run the Flask application locally, navigate to the application's directory and use:

```python app.py ```

Alternatively, you can use *gunicorn* as follows:

`gunicorn --workers=4 --bind 0.0.0.0:$PORT app:app`

Remember to replace **$PORT** with the port number you want to use.


