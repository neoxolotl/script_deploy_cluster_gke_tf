README
======
./start                                                                 User Commands                                                                 start
       ./start - Install Terraform and modules for Google Provider and deploy Cluster.

SYNOPSIS
       ./start [OPTION]... [COMMANDS]...
       ./start [OPTION] []...

OPTIONS
       Install Terraform and modules for Google Provider and deploy Cluster 
       Mandatory arguments to long options are mandatory for short options too.

       -p, --provision

       -tf, --Terraform choice install 

        	L, --Linux - Install and Initialize Terraform on Linux
        	M, --MacOs - Install and Initialize Terraform on MacOS - beta
		  
COMMANDS
	CREATE, --Create Install Terraform + Google Modules. 
	
	DESTROY, --Destroy from Terraform Cluster. 

	OUTPUT, --Output

	--help, --Help you 
		
Examples
=========
	
	./start -p CREATE -tf L	
				(Install Terraform on Linux and deploy Cluster)
					
	./start -p CREATE -tf M
				(Install Terraform on MacOs and deploy Cluster "have Bugs") 

	./start -p DESTROY -tf L
				(destroy the cluster)









Requeriments
==============

Unzip 

apt install unzip 


cd terraform

Init modules 

terraform init 





This documentations 

1.- Install Terraform
=========================


Linux
======

wget https://releases.hashicorp.com/terraform/0.12.6/terraform_0.12.6_linux_amd64.zip
unzip terraform_0.12.6_linux_amd64.zip
sudo mv terraform /opt/terraform
sudo ln -s /opt/terraform /usr/local/bin/terraform

	Initialize
	----------

echo "deb https://packages.cloud.google.com/apt cloud-sdk main" | sudo tee -a /etc/apt/sources.list.d/google-cloud-sdk.list
curl https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
sudo apt-get update && sudo apt-get install google-cloud-sdk kubectl
gcloud init 




MacOS
==========

brew install terraform

	Initialize
	----------

curl https://sdk.cloud.google.com | bash
exec -l $SHELL
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/darwin/amd64/kubectl
chmod +x ./kubectl && sudo mv ./kubectl /usr/local/bin/kubectl
gcloud init


RESULT: 
=======
...
Apply complete! Resources: 2 added, 0 changed, 0 destroyed.

Outputs:

endpoint = 35.202.190.41
master_version = 1.15.12-gke.2
-----------------gcloud --------------------------------------------------
NAME          LOCATION     MASTER_VERSION  MASTER_IP      MACHINE_TYPE   NODE_VERSION   NUM_NODES  STATUS
demo-cluster  us-central1  1.15.12-gke.2   35.202.190.41  n1-standard-1  1.15.12-gke.2  1          RUNNING
Fetching cluster endpoint and auth data.
kubeconfig entry generated for demo-cluster.
-----------------Verify kubectl-------------------------------------------
/home/fsosa/script_deploy_cluster_gke_tf/terraform-gke
deployment.extensions/demo created
service/demo created
ingress.networking.k8s.io/ingress-nginx created
-----------------Wait...... building ingress-----------------------------
NAME            HOSTS   ADDRESS         PORTS   AGE
ingress-nginx   *       34.107.233.96   80      7m2s

After do you browser
--------------------
 
fsosa@fsosa-Latitude-5480:/$ curl 34.107.233.96:80 
{
    "hello": "world"
}
fsosa@fsosa-Latitude-5480:/$ curl 34.107.233.96/greetings 
{
    "hello world from": "Hostname_7demo-7c4578c9f-cr6rl"
}
fsosa@fsosa-Latitude-5480:/$ curl 34.107.233.96/square/4
{
    "square": 16
}







