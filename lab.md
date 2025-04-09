## Quickstart (GKE)

1. Ensure you have the following requirements:
   - [Google Cloud project](https://cloud.google.com/resource-manager/docs/creating-managing-projects#creating_a_project).
   - Shell environment with `gcloud`, `git`, and `kubectl`.

2. Clone the latest major version.

   ```sh
   git clone https://github.com/fullstackenabler/fse-ngx.git
   cd microservices-demo/
   ```
3. Set the Google Cloud project and region and ensure the Google Kubernetes Engine API is enabled.

   ```sh
   export PROJECT_ID=<PROJECT_ID>
   export REGION=us-central1
   gcloud services enable container.googleapis.com \
     --project=${PROJECT_ID}
   ```

   Substitute `<PROJECT_ID>` with the ID of your Google Cloud project.

4. Create a GKE cluster and get the credentials for it.

   ```sh
   gcloud container clusters create-auto fse-environment \
     --project=${PROJECT_ID} --region=${REGION}
   ```

   Creating the cluster may take a few minutes.

5. Create new namespace

   ```sh
   kubectl create namespace fullstackenabler
   ```

Confirm the creation of the namespace with the following command

   ```sh
   kubectl get namespace
   ```

6. Deploy FSE environment to the cluster.

   ```sh
   kubectl apply -f ./fse-ngx/fse-ngnix.yaml
   ```
