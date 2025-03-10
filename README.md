# Deploying Google Cloud Function with Load Balancer, Monitoring, and Grafana on GCP

Prerequisites

Before you begin, ensure you have the following:

A Google Cloud Platform (GCP) account with billing enabled

A GCP Project (Take note of the Project ID)

The following tools installed:

Terraform (>= 1.3.0)

Google Cloud SDK (gcloud)

kubectl

Deployment Steps

1️⃣ Clone the Repository
  
  git clone <repo-url>
  cd <repo-directory>

2️⃣ Authenticate with Google Cloud

Login and set the active project:

  gcloud auth login
  gcloud config set project <PROJECT_ID>

  Enable necessary APIs:

  gcloud services enable compute.googleapis.com cloudfunctions.googleapis.com monitoring.googleapis.com

3️⃣ Initialize and Apply Terraform

Ensure Terraform is initialized and apply the configuration:

  terraform init
  terraform apply -auto-approve

4️⃣ Verify Deployment

✅ Cloud Function Deployment

Check deployed functions:

  gcloud functions list --region=<REGION>

Invoke the Cloud Function manually:

  gcloud functions call hello-world-function --region=<REGION>

✅ Load Balancer Setup

Fetch the Load Balancer IP:

  gcloud compute forwarding-rules list --format='value(IPAddress)'

Test it in the browser:

  curl -X GET https://<LOAD_BALANCER_IP>

✅ Grafana Access

Get the external IP of the Grafana instance:

  gcloud compute instances list --format='value(EXTERNAL_IP)' --filter="name:grafana-server"

Access Grafana:

  http://<GRAFANA_IP>:3000
  (Default credentials: admin/admin)

✅ Monitoring and Alerts

Check dashboards:

  gcloud monitoring dashboards list

Verify alert policy:

  gcloud monitoring alert-policies list

5️⃣ Cleanup

To destroy all resources:

  terraform destroy -auto-approve

Troubleshooting

If Terraform errors occur, try terraform plan to review expected changes.

Ensure your IAM permissions allow deployment of GCP resources.

Check Cloud Function logs:

 gcloud functions logs read hello-world-function --region=<REGION>


 Next Steps

Add CI/CD for automatic deployment

Secure Grafana access with firewall rules

Use Cloud Storage Versioning for function updates
 
  
