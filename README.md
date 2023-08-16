# mlops-training-data-analyst
Labs and demos for courses for GCP Training (http://cloud.google.com/training).

gcloud auth list
gcloud config list project

Task 1. Enable Google Cloud services
In Cloud Shell, use gcloud to enable the services used in the lab:

gcloud services enable \
  compute.googleapis.com \
  iam.googleapis.com \
  iamcredentials.googleapis.com \
  monitoring.googleapis.com \
  logging.googleapis.com \
  notebooks.googleapis.com \
  aiplatform.googleapis.com \
  bigquery.googleapis.com \
  artifactregistry.googleapis.com \
  cloudbuild.googleapis.com \
  container.googleapis.com
Copied!
Task 2. Create Vertex AI custom service account for Vertex Tensorboard integration
Create custom service account:
SERVICE_ACCOUNT_ID=vertex-custom-training-sa
gcloud iam service-accounts create $SERVICE_ACCOUNT_ID  \
    --description="A custom service account for Vertex custom training with Tensorboard" \
    --display-name="Vertex AI Custom Training"
Copied!
Grant it access to Cloud Storage for writing and retrieving Tensorboard logs:
PROJECT_ID=$(gcloud config get-value core/project)
gcloud projects add-iam-policy-binding $PROJECT_ID \
    --member=serviceAccount:$SERVICE_ACCOUNT_ID@$PROJECT_ID.iam.gserviceaccount.com \
    --role="roles/storage.admin"
Copied!
Grant it access to your BigQuery data source to read data into your TensorFlow model:
gcloud projects add-iam-policy-binding $PROJECT_ID \
    --member=serviceAccount:$SERVICE_ACCOUNT_ID@$PROJECT_ID.iam.gserviceaccount.com \
    --role="roles/bigquery.admin"
Copied!
Grant it access to Vertex AI for running model training, deployment, and explanation jobs:
gcloud projects add-iam-policy-binding $PROJECT_ID \
    --member=serviceAccount:$SERVICE_ACCOUNT_ID@$PROJECT_ID.iam.gserviceaccount.com \
    --role="roles/aiplatform.user"
Copied!
Task 3. Launch Vertex AI Workbench notebook
In the Google Cloud Console, on the Navigation Menu, click Vertex AI > Workbench.

On the Notebook instances page, click New Notebook > TensorFlow Enterprise > TensorFlow Enterprise 2.11 > Without GPUs.

In the New notebook instance dialog, confirm the name of the deep learning VM.

If you don’t want to change the region and zone, leave all settings as they are and then click Create.
The new VM will take 2-3 minutes to start.

Click Open JupyterLab.
A JupyterLab window will open in a new tab.

Click Check my progress to verify the objective.
Create a Vertex AI Notebook

Task 4. Clone the lab repository
Next you'll clone the training-data-analyst repo to your JupyterLab instance.

To clone the training-data-analyst notebook in your JupyterLab instance:

In JupyterLab, to open a new terminal, click the Terminal icon.

At the command-line prompt, run the following command:

git clone https://github.com/GoogleCloudPlatform/training-data-analyst
Copied!
To confirm that you have cloned the repository, double-click on the training-data-analyst directory and ensure that you can see its contents.
The files for all the Jupyter notebook-based labs throughout this course are available in this directory.

It will take several minutes for the repo to clone.

Click Check my progress to verify the objective.
Clone the lab repository

Task 5. Install lab dependencies and Run the Notebook
Run the following to go to the training-data-analyst/self-paced-labs/vertex-ai/vertex-ai-qwikstart folder, then pip3 install requirements.txt to install lab dependencies:

cd training-data-analyst/self-paced-labs/vertex-ai/vertex-ai-qwikstart
Copied!
pip3 install --user -r requirements.txt
Copied!
Note: Ignore the incompatibility warnings and errors.
Navigate to lab notebook
In your notebook, navigate to training-data-analyst > self-paced-labs > vertex-ai > vertex-ai-qwikstart, and open lab_exercise_long.ipynb.

Continue the lab in the notebook, and run each cell by clicking the Run icon at the top of the screen.

Alternatively, you can execute the code in a cell with SHIFT + ENTER.

Read the narrative and make sure you understand what's happening in each cell.


