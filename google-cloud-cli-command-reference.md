# Google Cloud CLI (`gcloud`) — Practical Command Reference

> **Updated:** 17 August 2026  
> **Scope:** A practical, high-coverage reference for the Google Cloud CLI, with commands grouped by the Google Cloud services you are most likely to administer.
>
> Google Cloud's CLI contains thousands of commands, so this guide focuses on the commands and workflows that are most useful for day-to-day cloud administration, DevOps, networking, Compute Engine, IAM, storage, databases, containers, serverless, logging, monitoring, and troubleshooting. Google documents the complete command tree separately. 

## Official references

- Google Cloud CLI reference: https://docs.cloud.google.com/sdk/gcloud/reference/
- Google Cloud CLI cheat sheet: https://docs.cloud.google.com/sdk/docs/cheatsheet
- Google Cloud CLI overview: https://cloud.google.com/cli
- Google Cloud SDK documentation: https://docs.cloud.google.com/sdk/docs

---

# 1. Command structure

Most `gcloud` commands follow this pattern:

```bash
gcloud <component> <resource> <operation> [RESOURCE_NAME] [FLAGS]
```

Examples:

```bash
gcloud compute instances list
gcloud compute instances describe VM_NAME --zone=ZONE
gcloud compute instances create VM_NAME --zone=ZONE --machine-type=e2-medium
```

Common operations:

```text
list
describe
create
update
delete
get
set
add
remove
start
stop
restart
reset
attach
detach
resize
deploy
run
logs
export
import
```

Google also supports release levels such as `alpha`, `beta`, and `preview` for commands that are not generally available.

---

# 2. Installation and first-time setup

## Check installation

```bash
gcloud version
```

```bash
gcloud info
```

## Initialize gcloud

```bash
gcloud init
```

This normally lets you:

- Sign in.
- Select a Google Cloud project.
- Select a default region/zone where appropriate.
- Create or activate a configuration.

## Update gcloud

```bash
gcloud components update
```

## Install an additional component

```bash
gcloud components install COMPONENT_NAME
```

## List installed components

```bash
gcloud components list
```

## Get help

```bash
gcloud help
gcloud COMMAND --help
```

Examples:

```bash
gcloud compute instances create --help
gcloud compute networks --help
gcloud auth --help
```

## Search help

```bash
gcloud help TOPIC
```

## Built-in cheat sheet

```bash
gcloud cheat-sheet
```

---

# 3. Authentication

## Login with your Google account

```bash
gcloud auth login
```

## List authenticated accounts

```bash
gcloud auth list
```

## Change active account

```bash
gcloud config set account USER_EMAIL
```

Example:

```bash
gcloud config set account user@example.com
```

## Revoke an account

```bash
gcloud auth revoke USER_EMAIL
```

## Login using a service account key

```bash
gcloud auth activate-service-account SERVICE_ACCOUNT_EMAIL \
    --key-file=KEY_FILE.json
```

Example:

```bash
gcloud auth activate-service-account \
    deployer@PROJECT_ID.iam.gserviceaccount.com \
    --key-file=service-account.json
```

> Prefer short-lived credentials, workload identity, or service-account impersonation over long-lived JSON keys when possible.

## Application Default Credentials

```bash
gcloud auth application-default login
```

## Print an access token

```bash
gcloud auth print-access-token
```

## Print an identity token

```bash
gcloud auth print-identity-token
```

## Revoke Application Default Credentials

```bash
gcloud auth application-default revoke
```

---

# 4. Configurations

Configurations are useful when you work with multiple projects or accounts.

## List configurations

```bash
gcloud config configurations list
```

## Create a configuration

```bash
gcloud config configurations create CONFIG_NAME
```

Example:

```bash
gcloud config configurations create production
```

## Activate a configuration

```bash
gcloud config configurations activate production
```

## Delete a configuration

```bash
gcloud config configurations delete CONFIG_NAME
```

## Show current configuration

```bash
gcloud config list
```

## Set project

```bash
gcloud config set project PROJECT_ID
```

Example:

```bash
gcloud config set project resonant-forge-505414-n2
```

## Set default region

```bash
gcloud config set compute/region REGION
```

Example:

```bash
gcloud config set compute/region asia-south1
```

## Set default zone

```bash
gcloud config set compute/zone ZONE
```

Example:

```bash
gcloud config set compute/zone asia-south1-a
```

## Get a configuration property

```bash
gcloud config get-value project
gcloud config get-value compute/region
gcloud config get-value compute/zone
```

## Show all properties

```bash
gcloud config list
```

## Set a property

```bash
gcloud config set PROPERTY VALUE
```

---

# 5. Projects

## List projects

```bash
gcloud projects list
```

## Describe a project

```bash
gcloud projects describe PROJECT_ID
```

## Create a project

```bash
gcloud projects create PROJECT_ID \
    --name="PROJECT_NAME"
```

## Set active project

```bash
gcloud config set project PROJECT_ID
```

## Get current project

```bash
gcloud config get-value project
```

## Delete a project

```bash
gcloud projects delete PROJECT_ID
```

> Project deletion is destructive. Verify the project ID before executing.

---

# 6. Billing

## List billing accounts

```bash
gcloud billing accounts list
```

## Describe billing account

```bash
gcloud billing accounts describe BILLING_ACCOUNT_ID
```

## List projects associated with a billing account

```bash
gcloud billing projects list \
    --billing-account=BILLING_ACCOUNT_ID
```

## Link project to billing account

```bash
gcloud billing projects link PROJECT_ID \
    --billing-account=BILLING_ACCOUNT_ID
```

## Check project billing information

```bash
gcloud billing projects describe PROJECT_ID
```

---

# 7. Enable and disable APIs

## List enabled services

```bash
gcloud services list --enabled
```

## List all available services

```bash
gcloud services list --available
```

## Enable an API

```bash
gcloud services enable SERVICE_NAME
```

Examples:

```bash
gcloud services enable compute.googleapis.com
gcloud services enable container.googleapis.com
gcloud services enable run.googleapis.com
gcloud services enable sqladmin.googleapis.com
gcloud services enable cloudbuild.googleapis.com
```

## Disable an API

```bash
gcloud services disable SERVICE_NAME
```

## Check a service

```bash
gcloud services list --enabled \
    --filter="name:compute.googleapis.com"
```

---

# 8. IAM — users, roles, and permissions

## View project IAM policy

```bash
gcloud projects get-iam-policy PROJECT_ID
```

## Add a project IAM role

```bash
gcloud projects add-iam-policy-binding PROJECT_ID \
    --member="MEMBER" \
    --role="ROLE"
```

Example:

```bash
gcloud projects add-iam-policy-binding PROJECT_ID \
    --member="user:user@example.com" \
    --role="roles/viewer"
```

Common member formats:

```text
user:USER_EMAIL
serviceAccount:SERVICE_ACCOUNT_EMAIL
group:GROUP_EMAIL
domain:DOMAIN
```

## Remove a project IAM role

```bash
gcloud projects remove-iam-policy-binding PROJECT_ID \
    --member="MEMBER" \
    --role="ROLE"
```

## List IAM roles

```bash
gcloud iam roles list
```

## List predefined roles

```bash
gcloud iam roles list --project=PROJECT_ID
```

## Describe a role

```bash
gcloud iam roles describe roles/ROLE_NAME
```

Example:

```bash
gcloud iam roles describe roles/compute.admin
```

---

# 9. Service accounts

## List service accounts

```bash
gcloud iam service-accounts list
```

## Create a service account

```bash
gcloud iam service-accounts create SERVICE_ACCOUNT_NAME \
    --display-name="DISPLAY_NAME"
```

Example:

```bash
gcloud iam service-accounts create deployer \
    --display-name="Deployment Service Account"
```

## Describe service account

```bash
gcloud iam service-accounts describe SERVICE_ACCOUNT_EMAIL
```

## Delete service account

```bash
gcloud iam service-accounts delete SERVICE_ACCOUNT_EMAIL
```

## Grant service-account IAM permission

```bash
gcloud iam service-accounts add-iam-policy-binding \
    SERVICE_ACCOUNT_EMAIL \
    --member="MEMBER" \
    --role="ROLE"
```

## List service-account keys

```bash
gcloud iam service-accounts keys list \
    --iam-account=SERVICE_ACCOUNT_EMAIL
```

## Create a key

```bash
gcloud iam service-accounts keys create KEY_FILE.json \
    --iam-account=SERVICE_ACCOUNT_EMAIL
```

## Delete a key

```bash
gcloud iam service-accounts keys delete KEY_ID \
    --iam-account=SERVICE_ACCOUNT_EMAIL
```

---

# 10. Service-account impersonation

Instead of downloading service-account keys, you can often impersonate a service account.

```bash
gcloud COMMAND \
    --impersonate-service-account=SERVICE_ACCOUNT_EMAIL
```

Example:

```bash
gcloud compute instances list \
    --impersonate-service-account=deployer@PROJECT_ID.iam.gserviceaccount.com
```

Set a default impersonated service account:

```bash
gcloud config set auth/impersonate_service_account \
    SERVICE_ACCOUNT_EMAIL
```

Remove it:

```bash
gcloud config unset auth/impersonate_service_account
```

---

# 11. Compute Engine — VM basics

## List VMs

```bash
gcloud compute instances list
```

## List VMs in a zone

```bash
gcloud compute instances list \
    --zones=asia-south1-a
```

## Describe a VM

```bash
gcloud compute instances describe VM_NAME \
    --zone=ZONE
```

## Create a VM

```bash
gcloud compute instances create VM_NAME \
    --zone=ZONE \
    --machine-type=MACHINE_TYPE
```

Example:

```bash
gcloud compute instances create web-01 \
    --zone=asia-south1-a \
    --machine-type=e2-medium
```

## Create a VM with an image

```bash
gcloud compute instances create VM_NAME \
    --zone=ZONE \
    --machine-type=e2-medium \
    --image-family=debian-12 \
    --image-project=debian-cloud
```

## Start a VM

```bash
gcloud compute instances start VM_NAME \
    --zone=ZONE
```

## Stop a VM

```bash
gcloud compute instances stop VM_NAME \
    --zone=ZONE
```

## Restart a VM

```bash
gcloud compute instances restart VM_NAME \
    --zone=ZONE
```

## Reset a VM

```bash
gcloud compute instances reset VM_NAME \
    --zone=ZONE
```

> `reset` is similar to a hard reset. Prefer `restart` for normal operation.

## Delete a VM

```bash
gcloud compute instances delete VM_NAME \
    --zone=ZONE
```

---

# 12. SSH and VM access

## SSH into a VM

```bash
gcloud compute ssh VM_NAME \
    --zone=ZONE
```

## SSH using IAP tunneling

Useful when the VM does not have a public external IP:

```bash
gcloud compute ssh VM_NAME \
    --zone=ZONE \
    --tunnel-through-iap
```

## Execute a remote command

```bash
gcloud compute ssh VM_NAME \
    --zone=ZONE \
    --command="COMMAND"
```

Example:

```bash
gcloud compute ssh web-01 \
    --zone=asia-south1-a \
    --command="uname -a"
```

## Copy local file to VM

```bash
gcloud compute scp LOCAL_FILE \
    VM_NAME:REMOTE_PATH \
    --zone=ZONE
```

## Copy VM file to local machine

```bash
gcloud compute scp \
    VM_NAME:REMOTE_FILE \
    LOCAL_PATH \
    --zone=ZONE
```

## Copy a directory

```bash
gcloud compute scp \
    --recurse \
    ./my-directory \
    VM_NAME:~/ \
    --zone=ZONE
```

---

# 13. Compute Engine zones and regions

## List regions

```bash
gcloud compute regions list
```

## Describe a region

```bash
gcloud compute regions describe REGION
```

## List zones

```bash
gcloud compute zones list
```

## Describe a zone

```bash
gcloud compute zones describe ZONE
```

## List available machine types

```bash
gcloud compute machine-types list
```

## List machine types in a zone

```bash
gcloud compute machine-types list \
    --zones=asia-south1-a
```

---

# 14. VM machine types

## Describe machine type

```bash
gcloud compute machine-types describe MACHINE_TYPE \
    --zone=ZONE
```

## Change VM machine type

The VM normally needs to be stopped first:

```bash
gcloud compute instances stop VM_NAME \
    --zone=ZONE

gcloud compute instances set-machine-type VM_NAME \
    --machine-type=MACHINE_TYPE \
    --zone=ZONE

gcloud compute instances start VM_NAME \
    --zone=ZONE
```

---

# 15. Persistent disks

## List disks

```bash
gcloud compute disks list
```

## Describe disk

```bash
gcloud compute disks describe DISK_NAME \
    --zone=ZONE
```

## Create disk

```bash
gcloud compute disks create DISK_NAME \
    --size=100GB \
    --type=pd-balanced \
    --zone=ZONE
```

## Resize disk

```bash
gcloud compute disks resize DISK_NAME \
    --size=200GB \
    --zone=ZONE
```

## Attach disk

```bash
gcloud compute instances attach-disk VM_NAME \
    --disk=DISK_NAME \
    --zone=ZONE
```

## Detach disk

```bash
gcloud compute instances detach-disk VM_NAME \
    --disk=DISK_NAME \
    --zone=ZONE
```

## Delete disk

```bash
gcloud compute disks delete DISK_NAME \
    --zone=ZONE
```

---

# 16. Disk snapshots

## List snapshots

```bash
gcloud compute snapshots list
```

## Create snapshot

```bash
gcloud compute disks snapshot DISK_NAME \
    --snapshot-names=SNAPSHOT_NAME \
    --zone=ZONE
```

## Describe snapshot

```bash
gcloud compute snapshots describe SNAPSHOT_NAME
```

## Create disk from snapshot

```bash
gcloud compute disks create NEW_DISK_NAME \
    --source-snapshot=SNAPSHOT_NAME \
    --zone=ZONE
```

## Delete snapshot

```bash
gcloud compute snapshots delete SNAPSHOT_NAME
```

---

# 17. VM images

## List images

```bash
gcloud compute images list
```

## Describe image

```bash
gcloud compute images describe IMAGE_NAME
```

## Create image from disk

```bash
gcloud compute images create IMAGE_NAME \
    --source-disk=DISK_NAME \
    --source-disk-zone=ZONE
```

## Delete image

```bash
gcloud compute images delete IMAGE_NAME
```

---

# 18. Instance templates

## List templates

```bash
gcloud compute instance-templates list
```

## Describe template

```bash
gcloud compute instance-templates describe TEMPLATE_NAME
```

## Create template

```bash
gcloud compute instance-templates create TEMPLATE_NAME \
    --machine-type=e2-medium \
    --image-family=debian-12 \
    --image-project=debian-cloud
```

## Delete template

```bash
gcloud compute instance-templates delete TEMPLATE_NAME
```

---

# 19. Managed instance groups

## List managed instance groups

```bash
gcloud compute instance-groups managed list
```

## Describe MIG

```bash
gcloud compute instance-groups managed describe MIG_NAME \
    --zone=ZONE
```

## Create a zonal MIG

```bash
gcloud compute instance-groups managed create MIG_NAME \
    --base-instance-name=INSTANCE_PREFIX \
    --size=2 \
    --template=TEMPLATE_NAME \
    --zone=ZONE
```

## Resize MIG

```bash
gcloud compute instance-groups managed resize MIG_NAME \
    --size=5 \
    --zone=ZONE
```

## List instances in MIG

```bash
gcloud compute instance-groups managed list-instances MIG_NAME \
    --zone=ZONE
```

## Delete MIG

```bash
gcloud compute instance-groups managed delete MIG_NAME \
    --zone=ZONE
```

---

# 20. Autoscaling

## Create autoscaler

```bash
gcloud compute instance-groups managed set-autoscaling MIG_NAME \
    --zone=ZONE \
    --min-num-replicas=2 \
    --max-num-replicas=8 \
    --target-cpu-utilization=0.60
```

## Describe autoscaler

```bash
gcloud compute instance-groups managed describe MIG_NAME \
    --zone=ZONE
```

## Disable autoscaling

```bash
gcloud compute instance-groups managed stop-autoscaling MIG_NAME \
    --zone=ZONE
```

---

# 21. VPC networks

## List VPC networks

```bash
gcloud compute networks list
```

## Describe VPC

```bash
gcloud compute networks describe NETWORK_NAME
```

## Create custom VPC

```bash
gcloud compute networks create NETWORK_NAME \
    --subnet-mode=custom
```

## Create auto-mode VPC

```bash
gcloud compute networks create NETWORK_NAME \
    --subnet-mode=auto
```

## Delete VPC

```bash
gcloud compute networks delete NETWORK_NAME
```

> A VPC cannot be deleted while dependent resources such as subnets, routes, routers, VPN resources, or other network resources still reference it.

---

# 22. Subnets

## List subnets

```bash
gcloud compute networks subnets list
```

## Describe subnet

```bash
gcloud compute networks subnets describe SUBNET_NAME \
    --region=REGION
```

## Create subnet

```bash
gcloud compute networks subnets create SUBNET_NAME \
    --network=NETWORK_NAME \
    --region=REGION \
    --range=10.0.0.0/24
```

## Expand subnet range

```bash
gcloud compute networks subnets expand-ip-range SUBNET_NAME \
    --region=REGION \
    --prefix-length=23
```

## Delete subnet

```bash
gcloud compute networks subnets delete SUBNET_NAME \
    --region=REGION
```

---

# 23. Routes

## List routes

```bash
gcloud compute routes list
```

## Describe route

```bash
gcloud compute routes describe ROUTE_NAME
```

## Create route

```bash
gcloud compute routes create ROUTE_NAME \
    --network=NETWORK_NAME \
    --destination-range=10.10.0.0/16 \
    --next-hop-instance=VM_NAME \
    --next-hop-instance-zone=ZONE
```

## Delete route

```bash
gcloud compute routes delete ROUTE_NAME
```

---

# 24. Firewall rules

## List firewall rules

```bash
gcloud compute firewall-rules list
```

## Describe firewall rule

```bash
gcloud compute firewall-rules describe RULE_NAME
```

## Create firewall rule

```bash
gcloud compute firewall-rules create RULE_NAME \
    --network=NETWORK_NAME \
    --allow=tcp:80,tcp:443
```

## Allow SSH

```bash
gcloud compute firewall-rules create allow-ssh \
    --network=NETWORK_NAME \
    --allow=tcp:22 \
    --source-ranges=SOURCE_CIDR
```

## Allow HTTP

```bash
gcloud compute firewall-rules create allow-http \
    --network=NETWORK_NAME \
    --allow=tcp:80 \
    --source-ranges=0.0.0.0/0
```

## Allow HTTPS

```bash
gcloud compute firewall-rules create allow-https \
    --network=NETWORK_NAME \
    --allow=tcp:443 \
    --source-ranges=0.0.0.0/0
```

## Delete firewall rule

```bash
gcloud compute firewall-rules delete RULE_NAME
```

> Avoid opening SSH/RDP to `0.0.0.0/0` unless you have a specific security reason. Prefer IAP, VPN, or restricted source ranges.

---

# 25. Cloud Routers

## List routers

```bash
gcloud compute routers list
```

## Describe router

```bash
gcloud compute routers describe ROUTER_NAME \
    --region=REGION
```

## Create router

```bash
gcloud compute routers create ROUTER_NAME \
    --network=NETWORK_NAME \
    --region=REGION
```

## Delete router

```bash
gcloud compute routers delete ROUTER_NAME \
    --region=REGION
```

### Important: VPC deletion dependency

If you see:

```text
The network resource ... is already being used by .../regions/REGION/routers/ROUTER
```

find the router:

```bash
gcloud compute routers list
```

Then inspect it:

```bash
gcloud compute routers describe ROUTER_NAME \
    --region=REGION
```

If it is no longer needed:

```bash
gcloud compute routers delete ROUTER_NAME \
    --region=REGION
```

Then retry:

```bash
gcloud compute networks delete NETWORK_NAME
```

---

# 26. Cloud NAT

## List NAT configurations

```bash
gcloud compute routers nats list \
    --router=ROUTER_NAME \
    --region=REGION
```

## Describe NAT

```bash
gcloud compute routers nats describe NAT_NAME \
    --router=ROUTER_NAME \
    --region=REGION
```

## Create NAT

```bash
gcloud compute routers nats create NAT_NAME \
    --router=ROUTER_NAME \
    --region=REGION \
    --auto-allocate-nat-external-ips \
    --nat-all-subnet-ip-ranges
```

## Delete NAT

```bash
gcloud compute routers nats delete NAT_NAME \
    --router=ROUTER_NAME \
    --region=REGION
```

---

# 27. External/static IP addresses

## List addresses

```bash
gcloud compute addresses list
```

## List regional addresses

```bash
gcloud compute addresses list \
    --regions=REGION
```

## Describe address

```bash
gcloud compute addresses describe ADDRESS_NAME \
    --region=REGION
```

## Reserve regional static IP

```bash
gcloud compute addresses create ADDRESS_NAME \
    --region=REGION
```

## Reserve global static IP

```bash
gcloud compute addresses create ADDRESS_NAME \
    --global
```

## Delete regional IP

```bash
gcloud compute addresses delete ADDRESS_NAME \
    --region=REGION
```

## Delete global IP

```bash
gcloud compute addresses delete ADDRESS_NAME \
    --global
```

---

# 28. Load balancing

Common command groups:

```bash
gcloud compute forwarding-rules list
gcloud compute forwarding-rules describe FORWARDING_RULE
gcloud compute forwarding-rules delete FORWARDING_RULE
```

## Backend services

```bash
gcloud compute backend-services list
gcloud compute backend-services describe BACKEND_SERVICE
```

## Health checks

```bash
gcloud compute health-checks list
gcloud compute health-checks describe HEALTH_CHECK
```

## Target pools

```bash
gcloud compute target-pools list
gcloud compute target-pools describe TARGET_POOL
```

## URL maps

```bash
gcloud compute url-maps list
gcloud compute url-maps describe URL_MAP
```

---

# 29. Cloud Storage (`gcloud storage`)

Google recommends the modern `gcloud storage` commands for Cloud Storage workflows.

## List buckets

```bash
gcloud storage ls
```

## Create bucket

```bash
gcloud storage buckets create gs://BUCKET_NAME \
    --location=REGION
```

## Describe bucket

```bash
gcloud storage buckets describe gs://BUCKET_NAME
```

## List objects

```bash
gcloud storage ls gs://BUCKET_NAME
```

## Upload file

```bash
gcloud storage cp LOCAL_FILE \
    gs://BUCKET_NAME/
```

## Upload directory

```bash
gcloud storage cp \
    --recursive \
    ./DIRECTORY \
    gs://BUCKET_NAME/
```

## Download file

```bash
gcloud storage cp \
    gs://BUCKET_NAME/FILE \
    LOCAL_PATH
```

## Synchronize directory

```bash
gcloud storage rsync \
    --recursive \
    LOCAL_DIRECTORY \
    gs://BUCKET_NAME/
```

## Delete object

```bash
gcloud storage rm gs://BUCKET_NAME/OBJECT
```

## Delete bucket

```bash
gcloud storage rm --recursive gs://BUCKET_NAME
```

> Bucket deletion is destructive and requires the bucket to be empty unless recursive deletion is used.

---

# 30. Cloud SQL

## List SQL instances

```bash
gcloud sql instances list
```

## Describe instance

```bash
gcloud sql instances describe INSTANCE_NAME
```

## Create PostgreSQL instance

```bash
gcloud sql instances create INSTANCE_NAME \
    --database-version=POSTGRES_17 \
    --tier=db-custom-2-7680 \
    --region=REGION
```

## Start instance

```bash
gcloud sql instances patch INSTANCE_NAME \
    --activation-policy=ALWAYS
```

## Stop instance

```bash
gcloud sql instances patch INSTANCE_NAME \
    --activation-policy=NEVER
```

## Restart instance

```bash
gcloud sql instances restart INSTANCE_NAME
```

## Delete instance

```bash
gcloud sql instances delete INSTANCE_NAME
```

## List databases

```bash
gcloud sql databases list \
    --instance=INSTANCE_NAME
```

## Create database

```bash
gcloud sql databases create DATABASE_NAME \
    --instance=INSTANCE_NAME
```

## List users

```bash
gcloud sql users list \
    --instance=INSTANCE_NAME
```

## Create user

```bash
gcloud sql users create USERNAME \
    --instance=INSTANCE_NAME \
    --password=PASSWORD
```

---

# 31. Cloud SQL backups

## List backups

```bash
gcloud sql backups list \
    --instance=INSTANCE_NAME
```

## Describe backup

```bash
gcloud sql backups describe BACKUP_ID \
    --instance=INSTANCE_NAME
```

## Create backup

```bash
gcloud sql backups create \
    --instance=INSTANCE_NAME
```

## Restore backup

```bash
gcloud sql backups restore BACKUP_ID \
    --restore-instance=INSTANCE_NAME
```

---

# 32. BigQuery (`bq`)

BigQuery has its own `bq` CLI in addition to `gcloud`.

## Check bq

```bash
bq version
```

## List datasets

```bash
bq ls --project_id=PROJECT_ID
```

## List tables

```bash
bq ls PROJECT_ID:DATASET_ID
```

## Show table

```bash
bq show PROJECT_ID:DATASET_ID.TABLE_ID
```

## Run a query

```bash
bq query \
    --use_legacy_sql=false \
    'SELECT * FROM `PROJECT_ID.DATASET_ID.TABLE_ID` LIMIT 10'
```

## Create dataset

```bash
bq mk \
    --dataset \
    PROJECT_ID:DATASET_ID
```

## Delete dataset

```bash
bq rm \
    -r \
    PROJECT_ID:DATASET_ID
```

---

# 33. Google Kubernetes Engine — GKE

## List clusters

```bash
gcloud container clusters list
```

## Describe cluster

```bash
gcloud container clusters describe CLUSTER_NAME \
    --location=LOCATION
```

## Create cluster

```bash
gcloud container clusters create CLUSTER_NAME \
    --location=LOCATION \
    --num-nodes=3
```

## Get Kubernetes credentials

```bash
gcloud container clusters get-credentials CLUSTER_NAME \
    --location=LOCATION
```

Then use:

```bash
kubectl get nodes
```

## Resize cluster

```bash
gcloud container clusters resize CLUSTER_NAME \
    --location=LOCATION \
    --num-nodes=5
```

## Upgrade cluster

```bash
gcloud container clusters upgrade CLUSTER_NAME \
    --location=LOCATION \
    --master
```

## Delete cluster

```bash
gcloud container clusters delete CLUSTER_NAME \
    --location=LOCATION
```

---

# 34. `kubectl` essentials after GKE login

## Cluster information

```bash
kubectl cluster-info
```

## Nodes

```bash
kubectl get nodes
```

## Pods

```bash
kubectl get pods
kubectl get pods -A
```

## Deployments

```bash
kubectl get deployments
```

## Services

```bash
kubectl get services
```

## Describe a pod

```bash
kubectl describe pod POD_NAME
```

## Logs

```bash
kubectl logs POD_NAME
```

## Follow logs

```bash
kubectl logs -f POD_NAME
```

## Execute command in pod

```bash
kubectl exec -it POD_NAME -- /bin/sh
```

## Apply YAML

```bash
kubectl apply -f deployment.yaml
```

## Delete YAML resources

```bash
kubectl delete -f deployment.yaml
```

---

# 35. Cloud Run

## List services

```bash
gcloud run services list
```

## Describe service

```bash
gcloud run services describe SERVICE_NAME \
    --region=REGION
```

## Deploy container

```bash
gcloud run deploy SERVICE_NAME \
    --image=IMAGE_URL \
    --region=REGION
```

## Deploy from source

```bash
gcloud run deploy SERVICE_NAME \
    --source=. \
    --region=REGION
```

## Update environment variable

```bash
gcloud run services update SERVICE_NAME \
    --region=REGION \
    --set-env-vars=KEY=VALUE
```

## Delete service

```bash
gcloud run services delete SERVICE_NAME \
    --region=REGION
```

---

# 36. Artifact Registry

## List repositories

```bash
gcloud artifacts repositories list
```

## Describe repository

```bash
gcloud artifacts repositories describe REPOSITORY \
    --location=LOCATION
```

## Create Docker repository

```bash
gcloud artifacts repositories create REPOSITORY \
    --repository-format=docker \
    --location=LOCATION
```

## Configure Docker authentication

```bash
gcloud auth configure-docker LOCATION-docker.pkg.dev
```

## List Docker images

```bash
gcloud artifacts docker images list \
    LOCATION-docker.pkg.dev/PROJECT_ID/REPOSITORY
```

## Delete image

```bash
gcloud artifacts docker images delete \
    IMAGE_URL
```

---

# 37. Cloud Build

## Submit a build

```bash
gcloud builds submit .
```

## Submit with a Dockerfile

```bash
gcloud builds submit \
    --tag=LOCATION-docker.pkg.dev/PROJECT_ID/REPOSITORY/IMAGE:TAG \
    .
```

## List builds

```bash
gcloud builds list
```

## Describe build

```bash
gcloud builds describe BUILD_ID
```

## Cancel build

```bash
gcloud builds cancel BUILD_ID
```

## View build logs

```bash
gcloud builds log BUILD_ID
```

---

# 38. Cloud Functions / Cloud Run functions

## List functions

```bash
gcloud functions list
```

## Describe function

```bash
gcloud functions describe FUNCTION_NAME \
    --gen2 \
    --region=REGION
```

## Deploy function

```bash
gcloud functions deploy FUNCTION_NAME \
    --gen2 \
    --runtime=RUNTIME \
    --region=REGION \
    --source=. \
    --entry-point=ENTRY_POINT
```

## Delete function

```bash
gcloud functions delete FUNCTION_NAME \
    --gen2 \
    --region=REGION
```

---

# 39. Pub/Sub

## List topics

```bash
gcloud pubsub topics list
```

## Create topic

```bash
gcloud pubsub topics create TOPIC_NAME
```

## Describe topic

```bash
gcloud pubsub topics describe TOPIC_NAME
```

## Delete topic

```bash
gcloud pubsub topics delete TOPIC_NAME
```

## List subscriptions

```bash
gcloud pubsub subscriptions list
```

## Create subscription

```bash
gcloud pubsub subscriptions create SUBSCRIPTION_NAME \
    --topic=TOPIC_NAME
```

## Delete subscription

```bash
gcloud pubsub subscriptions delete SUBSCRIPTION_NAME
```

## Publish message

```bash
gcloud pubsub topics publish TOPIC_NAME \
    --message="Hello Google Cloud"
```

## Pull messages

```bash
gcloud pubsub subscriptions pull SUBSCRIPTION_NAME \
    --auto-ack
```

---

# 40. Secret Manager

## List secrets

```bash
gcloud secrets list
```

## Create secret

```bash
gcloud secrets create SECRET_NAME \
    --replication-policy=automatic
```

## Add secret version

```bash
printf 'SECRET_VALUE' | \
gcloud secrets versions add SECRET_NAME \
    --data-file=-
```

## Access latest secret version

```bash
gcloud secrets versions access latest \
    --secret=SECRET_NAME
```

## List versions

```bash
gcloud secrets versions list SECRET_NAME
```

## Disable version

```bash
gcloud secrets versions disable VERSION_ID \
    --secret=SECRET_NAME
```

## Delete secret

```bash
gcloud secrets delete SECRET_NAME
```

> Do not put passwords, API keys, or private keys directly into shell history when avoidable.

---

# 41. Cloud Logging

## List logs

```bash
gcloud logging logs list
```

## Read recent logs

```bash
gcloud logging read \
    'severity>=ERROR' \
    --limit=50
```

## Read VM-related logs

```bash
gcloud logging read \
    'resource.type="gce_instance"' \
    --limit=50
```

## Read logs from a specific VM

```bash
gcloud logging read \
    'resource.type="gce_instance" AND resource.labels.instance_id="INSTANCE_ID"' \
    --limit=50
```

## Read logs with timestamps

```bash
gcloud logging read \
    'severity>=WARNING' \
    --limit=100 \
    --format="table(timestamp,severity,textPayload)"
```

## Delete a log

```bash
gcloud logging logs delete LOG_NAME
```

---

# 42. Monitoring

## List monitored resources

```bash
gcloud monitoring
```

For detailed monitoring administration, use the Cloud Monitoring APIs, console, or service-specific commands where available.

---

# 43. VPC connectivity troubleshooting

## List routes

```bash
gcloud compute routes list
```

## List firewall rules

```bash
gcloud compute firewall-rules list
```

## Describe VM networking

```bash
gcloud compute instances describe VM_NAME \
    --zone=ZONE
```

## List network interfaces

```bash
gcloud compute instances describe VM_NAME \
    --zone=ZONE \
    --format="yaml(networkInterfaces)"
```

## List subnetworks

```bash
gcloud compute networks subnets list
```

## List Cloud Routers

```bash
gcloud compute routers list
```

## List NAT configurations

```bash
gcloud compute routers nats list \
    --router=ROUTER_NAME \
    --region=REGION
```

---

# 44. Quota troubleshooting

When a VM/MIG operation fails with an error such as:

```text
Exceeded limit 'QUOTA_FOR_INSTANCES'
```

start with:

```bash
gcloud compute regions describe REGION
```

Look for quota information in the returned data.

You can also inspect project/service quotas through the Google Cloud console and Service Usage APIs.

Useful commands:

```bash
gcloud compute regions list
gcloud compute zones list
gcloud compute instances list
```

Check how many instances currently exist:

```bash
gcloud compute instances list \
    --format="table(name,zone,status)"
```

Check MIGs:

```bash
gcloud compute instance-groups managed list
```

Check autoscaling:

```bash
gcloud compute instance-groups managed list
```

If an autoscaler is trying to create more VMs than the regional quota permits, reduce the MIG maximum or request a quota increase.

---

# 45. Common quota workflow

```bash
# 1. Identify current project
gcloud config get-value project

# 2. Identify region
gcloud config get-value compute/region

# 3. List VMs
gcloud compute instances list

# 4. List managed instance groups
gcloud compute instance-groups managed list

# 5. Inspect the MIG
gcloud compute instance-groups managed describe MIG_NAME \
    --zone=ZONE

# 6. Check region information
gcloud compute regions describe REGION
```

---

# 46. Labels

Labels are extremely useful for administration and automation.

## List instances with labels

```bash
gcloud compute instances list \
    --format="table(name,labels)"
```

## Add a label

```bash
gcloud compute instances add-labels VM_NAME \
    --zone=ZONE \
    --labels=environment=prod
```

## Replace labels

```bash
gcloud compute instances update VM_NAME \
    --zone=ZONE \
    --update-labels=environment=prod,team=platform
```

---

# 47. Filtering

Filtering is one of the most important gcloud skills.

## Filter by name

```bash
gcloud compute instances list \
    --filter="name:web"
```

## Filter by status

```bash
gcloud compute instances list \
    --filter="status=RUNNING"
```

## Filter by zone

```bash
gcloud compute instances list \
    --filter="zone:asia-south1-a"
```

## Filter by label

```bash
gcloud compute instances list \
    --filter="labels.environment=prod"
```

## Multiple conditions

```bash
gcloud compute instances list \
    --filter="status=RUNNING AND labels.environment=prod"
```

## Exclude a condition

```bash
gcloud compute instances list \
    --filter="-status=TERMINATED"
```

---

# 48. Output formatting

## Default output

```bash
gcloud compute instances list
```

## JSON

```bash
gcloud compute instances describe VM_NAME \
    --zone=ZONE \
    --format=json
```

## YAML

```bash
gcloud compute instances describe VM_NAME \
    --zone=ZONE \
    --format=yaml
```

## Table

```bash
gcloud compute instances list \
    --format="table(name,zone,status)"
```

## CSV

```bash
gcloud compute instances list \
    --format="csv(name,zone,status)"
```

## Get one value

```bash
gcloud compute instances describe VM_NAME \
    --zone=ZONE \
    --format="value(networkInterfaces[0].networkIP)"
```

## Sort

```bash
gcloud compute instances list \
    --sort-by=name
```

## Limit

```bash
gcloud compute instances list \
    --limit=10
```

---

# 49. Useful global flags

These flags work across many `gcloud` commands.

## Project

```bash
--project=PROJECT_ID
```

## Account

```bash
--account=USER_EMAIL
```

## Region

```bash
--region=REGION
```

## Zone

```bash
--zone=ZONE
```

## No interactive prompts

```bash
--quiet
```

Example:

```bash
gcloud compute instances delete VM_NAME \
    --zone=ZONE \
    --quiet
```

## Verbosity

```bash
--verbosity=debug
```

Other levels include:

```text
debug
info
warning
error
critical
none
```

## Output format

```bash
--format=json
--format=yaml
--format=table(...)
--format=value(...)
```

## Help

```bash
--help
```

---

# 50. `gcloud topic`

`gcloud topic` provides documentation for concepts that apply across commands.

```bash
gcloud topic --help
```

Useful topics:

```bash
gcloud topic filters
gcloud topic formats
gcloud topic projections
gcloud topic configurations
gcloud topic escaping
gcloud topic startup
```

---

# 51. Alpha and beta commands

Some commands are released at different maturity levels.

## Alpha

```bash
gcloud alpha COMMAND
```

## Beta

```bash
gcloud beta COMMAND
```

Example:

```bash
gcloud beta compute ...
```

> Prefer GA commands for production unless you specifically need an alpha/beta feature.

---

# 52. Cloud Scheduler

## List jobs

```bash
gcloud scheduler jobs list
```

## Describe job

```bash
gcloud scheduler jobs describe JOB_NAME \
    --location=REGION
```

## Pause job

```bash
gcloud scheduler jobs pause JOB_NAME \
    --location=REGION
```

## Resume job

```bash
gcloud scheduler jobs resume JOB_NAME \
    --location=REGION
```

## Delete job

```bash
gcloud scheduler jobs delete JOB_NAME \
    --location=REGION
```

---

# 53. VPC VPN

## List VPN gateways

```bash
gcloud compute vpn-gateways list
```

## List VPN tunnels

```bash
gcloud compute vpn-tunnels list
```

## Describe tunnel

```bash
gcloud compute vpn-tunnels describe TUNNEL_NAME \
    --region=REGION
```

## Delete tunnel

```bash
gcloud compute vpn-tunnels delete TUNNEL_NAME \
    --region=REGION
```

---

# 54. DNS

## List managed zones

```bash
gcloud dns managed-zones list
```

## Describe zone

```bash
gcloud dns managed-zones describe ZONE_NAME
```

## Create managed zone

```bash
gcloud dns managed-zones create ZONE_NAME \
    --dns-name=example.com. \
    --description="Example DNS zone"
```

## List record sets

```bash
gcloud dns record-sets list \
    --zone=ZONE_NAME
```

## Delete managed zone

```bash
gcloud dns managed-zones delete ZONE_NAME
```

---

# 55. Load balancer troubleshooting checklist

```bash
# Forwarding rules
gcloud compute forwarding-rules list

# Backend services
gcloud compute backend-services list

# Health checks
gcloud compute health-checks list

# URL maps
gcloud compute url-maps list

# Target proxies
gcloud compute target-http-proxies list
gcloud compute target-https-proxies list

# Firewall rules
gcloud compute firewall-rules list
```

---

# 56. VM troubleshooting checklist

When a VM cannot be reached:

```bash
# Check the VM
gcloud compute instances describe VM_NAME \
    --zone=ZONE

# Check status
gcloud compute instances list \
    --filter="name=VM_NAME"

# Check network interfaces
gcloud compute instances describe VM_NAME \
    --zone=ZONE \
    --format="yaml(networkInterfaces)"

# Check firewall
gcloud compute firewall-rules list

# Check routes
gcloud compute routes list

# Check logs
gcloud logging read \
    'resource.type="gce_instance"' \
    --limit=50

# Try IAP SSH
gcloud compute ssh VM_NAME \
    --zone=ZONE \
    --tunnel-through-iap
```

---

# 57. "Failed to lookup instance" troubleshooting

If SSH/IAP returns:

```text
Failed to lookup instance
```

check:

```bash
gcloud config get-value project
gcloud config get-value compute/zone
gcloud compute instances list
```

Then explicitly specify the project and zone:

```bash
gcloud compute ssh VM_NAME \
    --project=PROJECT_ID \
    --zone=ZONE \
    --tunnel-through-iap
```

If the VM is in another zone:

```bash
gcloud compute instances list \
    --format="table(name,zone,status)"
```

Then use the exact zone shown.

---

# 58. IAP troubleshooting

## Check VM

```bash
gcloud compute instances describe VM_NAME \
    --zone=ZONE
```

## Use IAP SSH

```bash
gcloud compute ssh VM_NAME \
    --zone=ZONE \
    --tunnel-through-iap
```

## Test IAP TCP forwarding

```bash
gcloud compute start-iap-tunnel VM_NAME 22 \
    --local-host-port=localhost:2222 \
    --zone=ZONE
```

---

# 59. Common `gcloud` mistakes

## Wrong project

Check:

```bash
gcloud config get-value project
```

Fix:

```bash
gcloud config set project PROJECT_ID
```

Or override for one command:

```bash
gcloud compute instances list \
    --project=PROJECT_ID
```

## Wrong zone

Find the VM:

```bash
gcloud compute instances list \
    --format="table(name,zone,status)"
```

## Wrong region

```bash
gcloud compute regions list
```

## Resource already exists

Check:

```bash
gcloud RESOURCE COMMAND list
```

Then inspect:

```bash
gcloud RESOURCE COMMAND describe NAME
```

## Resource is being used

Find dependencies before deleting the parent resource.

For a VPC:

```bash
gcloud compute networks subnets list
gcloud compute routes list
gcloud compute routers list
gcloud compute vpn-tunnels list
gcloud compute firewall-rules list
```

---

# 60. Safe deletion workflow

Before deleting an important resource:

```bash
# Identify project
gcloud config get-value project

# Inspect resource
gcloud RESOURCE describe RESOURCE_NAME

# List related resources
gcloud RESOURCE list

# Delete dependencies first

# Delete parent resource last
```

For a VPC:

```bash
gcloud compute networks describe NETWORK_NAME
gcloud compute networks subnets list
gcloud compute routes list
gcloud compute routers list
gcloud compute vpn-tunnels list
gcloud compute firewall-rules list
```

Then delete dependencies and finally:

```bash
gcloud compute networks delete NETWORK_NAME
```

---

# 61. Useful shell aliases

For Bash/Linux/Cloud Shell:

```bash
alias g='gcloud'
alias gi='gcloud compute instances'
alias gn='gcloud compute networks'
alias gs='gcloud storage'
```

Then:

```bash
g gi list
g gn list
g gs ls
```

---

# 62. Useful environment variables

```bash
export PROJECT_ID="my-project-id"
export REGION="asia-south1"
export ZONE="asia-south1-a"
```

Use them:

```bash
gcloud config set project "$PROJECT_ID"
gcloud config set compute/region "$REGION"
gcloud config set compute/zone "$ZONE"
```

---

# 63. Useful one-liners

## Current project

```bash
gcloud config get-value project
```

## Current account

```bash
gcloud config get-value account
```

## Current zone

```bash
gcloud config get-value compute/zone
```

## All VMs

```bash
gcloud compute instances list
```

## Running VMs

```bash
gcloud compute instances list \
    --filter="status=RUNNING"
```

## VM names only

```bash
gcloud compute instances list \
    --format="value(name)"
```

## VM names and IPs

```bash
gcloud compute instances list \
    --format="table(name,networkInterfaces[0].networkIP,networkInterfaces[0].accessConfigs[0].natIP)"
```

## List VPCs

```bash
gcloud compute networks list
```

## List subnets

```bash
gcloud compute networks subnets list
```

## List firewall rules

```bash
gcloud compute firewall-rules list
```

## List static IPs

```bash
gcloud compute addresses list
```

## List routers

```bash
gcloud compute routers list
```

## List NATs

```bash
gcloud compute routers nats list \
    --router=ROUTER_NAME \
    --region=REGION
```

---

# 64. Automation pattern

For scripts, use:

```bash
gcloud COMMAND \
    --project="$PROJECT_ID" \
    --quiet
```

Use structured output:

```bash
gcloud compute instances list \
    --format=json
```

Or extract a value:

```bash
VM_IP=$(gcloud compute instances describe VM_NAME \
    --zone="$ZONE" \
    --format="value(networkInterfaces[0].networkIP)")
```

Then:

```bash
echo "$VM_IP"
```

---

# 65. Useful command discovery

When you know the service but not the command:

```bash
gcloud SERVICE --help
```

Example:

```bash
gcloud compute --help
gcloud compute instances --help
gcloud compute networks --help
gcloud storage --help
gcloud container --help
gcloud run --help
```

Find the command hierarchy:

```bash
gcloud help
```

Check a specific command:

```bash
gcloud compute instances create --help
```

---

# 66. Essential command patterns to memorize

If you are learning Google Cloud CLI, memorize these patterns first:

```bash
# List
gcloud RESOURCE list

# Describe
gcloud RESOURCE describe NAME

# Create
gcloud RESOURCE create NAME [FLAGS]

# Update
gcloud RESOURCE update NAME [FLAGS]

# Delete
gcloud RESOURCE delete NAME

# Filter
gcloud RESOURCE list --filter="EXPRESSION"

# Format
gcloud RESOURCE list --format="table(...)"

# Project
gcloud ... --project=PROJECT_ID

# Region
gcloud ... --region=REGION

# Zone
gcloud ... --zone=ZONE

# Non-interactive
gcloud ... --quiet

# Help
gcloud ... --help
```

---

# 67. Daily Google Cloud administration cheat sheet

```bash
# AUTH
gcloud auth list
gcloud auth login

# CONFIG
gcloud config list
gcloud config set project PROJECT_ID
gcloud config set compute/region REGION
gcloud config set compute/zone ZONE

# PROJECT
gcloud projects list
gcloud projects describe PROJECT_ID

# APIS
gcloud services list --enabled
gcloud services enable SERVICE.googleapis.com

# IAM
gcloud projects get-iam-policy PROJECT_ID
gcloud iam service-accounts list

# VM
gcloud compute instances list
gcloud compute instances describe VM --zone=ZONE
gcloud compute ssh VM --zone=ZONE
gcloud compute instances start VM --zone=ZONE
gcloud compute instances stop VM --zone=ZONE

# NETWORK
gcloud compute networks list
gcloud compute networks subnets list
gcloud compute firewall-rules list
gcloud compute routes list
gcloud compute routers list

# STORAGE
gcloud storage ls
gcloud storage ls gs://BUCKET

# GKE
gcloud container clusters list
gcloud container clusters get-credentials CLUSTER --location=LOCATION

# CLOUD RUN
gcloud run services list

# SQL
gcloud sql instances list

# LOGGING
gcloud logging logs list
gcloud logging read 'severity>=ERROR' --limit=50

# SECRETS
gcloud secrets list
gcloud secrets versions access latest --secret=SECRET_NAME
```

---

# 68. Recommended learning order

Learn these in order:

1. `gcloud init`
2. `gcloud auth`
3. `gcloud config`
4. `gcloud projects`
5. `gcloud services`
6. `gcloud compute instances`
7. `gcloud compute networks`
8. `gcloud compute networks subnets`
9. `gcloud compute firewall-rules`
10. `gcloud compute routes`
11. `gcloud compute routers`
12. `gcloud compute disks`
13. `gcloud compute snapshots`
14. `gcloud compute instance-templates`
15. `gcloud compute instance-groups managed`
16. IAM and service accounts
17. Cloud Storage
18. Cloud SQL
19. GKE + `kubectl`
20. Cloud Run
21. Artifact Registry
22. Cloud Build
23. Secret Manager
24. Logging and Monitoring
25. Pub/Sub
26. DNS
27. Load balancing
28. VPN and Cloud NAT
29. Automation and scripting

---

# 69. Important safety rules

Before running destructive commands, always check:

```bash
gcloud config get-value project
```

For zonal resources:

```bash
gcloud compute instances describe VM_NAME --zone=ZONE
```

For regional resources:

```bash
gcloud compute routers describe ROUTER_NAME --region=REGION
```

Use `--quiet` only when you intentionally want to bypass confirmation.

Be particularly careful with:

```bash
gcloud projects delete
gcloud compute instances delete
gcloud compute disks delete
gcloud compute snapshots delete
gcloud compute networks delete
gcloud compute firewall-rules delete
gcloud sql instances delete
gcloud container clusters delete
gcloud storage rm --recursive
gcloud secrets delete
```

---

# 70. Official documentation and complete command reference

Google Cloud CLI is much larger than this practical guide. Google states that the CLI provides thousands of commands covering Google Cloud services.

Use the official command reference whenever you need an exact command or flag:

- Google Cloud CLI reference: https://docs.cloud.google.com/sdk/gcloud/reference/
- Google Cloud CLI cheat sheet: https://docs.cloud.google.com/sdk/docs/cheatsheet
- Google Cloud CLI overview: https://cloud.google.com/cli
- Google Cloud SDK documentation: https://docs.cloud.google.com/sdk/docs

For any unfamiliar command, the safest first step is:

```bash
gcloud COMMAND --help
```

For example:

```bash
gcloud compute instances create --help
```

---

# Quick mental model

Think of Google Cloud CLI like this:

```text
gcloud
 ├── auth
 ├── config
 ├── projects
 ├── services
 ├── iam
 │   └── service-accounts
 ├── compute
 │   ├── instances
 │   ├── disks
 │   ├── snapshots
 │   ├── images
 │   ├── networks
 │   ├── networks subnets
 │   ├── firewall-rules
 │   ├── routes
 │   ├── routers
 │   ├── addresses
 │   ├── forwarding-rules
 │   ├── backend-services
 │   └── instance-groups managed
 ├── storage
 ├── sql
 ├── container
 ├── run
 ├── artifacts
 ├── builds
 ├── pubsub
 ├── secrets
 ├── logging
 └── dns
```

The key skill is not memorizing every command. Learn how to discover commands with `--help`, inspect resources with `describe`, enumerate resources with `list`, and control output with `--filter` and `--format`.
