# OpenAI + Google Vector Similarity

## Prerequisites

1. Setup a service account with Editor permissions
1. Create a VPC and use private service connect
    ```bash
    gcloud compute networks create {VPC} --bgp-routing-mode=regional --subnet-mode=auto --project={PROJECT}
    gcloud compute firewall-rules create {VPC}-allow-icmp --network {VPC} --priority 65534 --project {PROJECT} --allow icmp
    gcloud compute firewall-rules create {VPC}-allow-internal --network {VPC} --priority 65534 --project {PROJECT} --allow all --source-ranges 10.128.0.0/9
    gcloud compute firewall-rules create {VPC}-allow-rdp --network {VPC} --priority 65534 --project {PROJECT} --allow tcp:3389
    gcloud compute firewall-rules create {VPC}-allow-ssh --network {VPC} --priority 65534 --project {PROJECT} --allow tcp:22
    gcloud compute addresses create {RANGE} --global --prefix-length=16 --network={VPC} --purpose=VPC_PEERING --project={PROJECT}
    gcloud services vpc-peerings connect --service=servicenetworking.googleapis.com --network={VPC} --ranges={RANGE} --project={PROJECT}
    ```
1. Create a notebook (e.g., Vertex AI Workbench) that uses the service account and VPC - record the notebook region (needs to match the Matching Engine deployment)

## Running

See [demo.ipynb](demo.ipynb)