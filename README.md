# GADS 2020 Project 1


<details>
  
  <summary>Google Cloud Platform Big Data and Machine Learning Fundamentals Course: Lab 1</summary>
  
  ![Google Cloud Platform Big Data and Machine Learning Fundamentals Course: Lab 1](./img/BigDataMLFund01.png)

</details>


<details>
  
  <summary>Google Cloud Platform Big Data and Machine Learning Fundamentals Course: Lab 2</summary>
  
  ![Google Cloud Platform Big Data and Machine Learning Fundamentals Course: Lab 2](./img/BigDataMLFund02.png)

</details>


<details>
  
  <summary>Google Cloud Platform Big Data and Machine Learning Fundamentals Course: Lab 3</summary>
  
  ![Google Cloud Platform Big Data and Machine Learning Fundamentals Course: Lab 3](./img/BigDataMLFund03.png)

</details>


<details>
  
  <summary>Google Cloud Platform Big Data and Machine Learning Fundamentals Course: Lab 4</summary>
  
  ![Google Cloud Platform Big Data and Machine Learning Fundamentals Course: Lab 4](./img/BigDataMLFund04.png)

</details>


<details>
  
  <summary>Google Cloud Platform Big Data and Machine Learning Fundamentals Course: Lab 5</summary>
  
  ![Google Cloud Platform Big Data and Machine Learning Fundamentals Course: Lab 5](./img/BigDataMLFund05.png)

</details>


------


<details>
  
  <summary>Modernizing Data Lakes and Data Warehouses with GCP: Lab 1</summary>
  
  ![Modernizing Data Lakes and Data Warehouses with GCP: Lab 1](./img/ModernizingDataLakes_and_DataWarehous_withGCP01.png)

</details>


<details>
  
  <summary>Modernizing Data Lakes and Data Warehouses with GCP: Lab 2</summary>
  
  ![Modernizing Data Lakes and Data Warehouses with GCP: Lab 2](./img/ModernizingDataLakes_and_DataWarehous_withGCP02.png)

</details>



<details>
  
  <summary>Modernizing Data Lakes and Data Warehouses with GCP: Lab 3</summary>
  
  ![Modernizing Data Lakes and Data Warehouses with GCP: Lab 3](./img/ModernizingDataLakes_and_DataWarehous_withGCP03.png)

</details>



<details>
  
  <summary>Modernizing Data Lakes and Data Warehouses with GCP: Lab 4</summary>
  
  ![Modernizing Data Lakes and Data Warehouses with GCP: Lab 4](./img/ModernizingDataLakes_and_DataWarehous_withGCP04.png)

</details>


------


<details>
  
  <summary>Building Batch Data Pipelines on GCP: Lab 1</summary>
  
  ![Building Batch Data Pipelines on GCP: Lab 1](./img/BuildingBatchDataPipelines_onGCP01.png)

</details>


------


<details>
  
  <summary>Google Cloud Platform Fundamentals - Core Infrastructure: Lab 1</summary>
  
  ![Google Cloud Platform Fundamentals - Core Infrastructure: Lab 1](./img/GCP_Fund-CoreInfra01.png)

</details>


------
  
  
## Translation labs

<details>
  
  <summary>Lab Translation - GCP Fundamentals: Getting Started with Compute Engine</summary>
  
  ```
gcloud config set project <WRITE_HERE_YOUR_PROJECT_ID>

gcloud compute instances create my-vm-1 \
	--zone us-central1-a \
	--image-project debian-cloud \
	--image debian-9-stretch-v20200902 \
	--tags http-server 

gcloud compute firewall-rules create default-allow-http \
	--allow tcp:80 \
	--target-tags http-server

gcloud compute instances create my-vm-2 \
	--zone us-central1-b \
	--image-project debian-cloud \
	--image debian-9-stretch-v20200902 

gcloud compute ssh my-vm-2 --zone us-central1-b 	
	ping -c 2 my-vm-1
	exit
	
gcloud compute ssh my-vm-1 --zone us-central1-a
	sudo apt install -y nginx-light 
	curl http://localhost/
	sudo sed -i '/^<h1>.*/a Hello from Fady!' /var/www/html/index.nginx-debian.html
	curl http://localhost/
	exit
	
gcloud compute ssh my-vm-2 --zone us-central1-b 	
	curl http://my-vm-1/
	exit
	
VM_IP=`gcloud compute instances describe my-vm-1 --zone us-central1-a --format 'get(networkInterfaces[0].accessConfigs[0].natIP)'`
curl http://$VM_IP
  ```

</details>


<details>
  
  <summary>Lab Translation - Google Cloud Fundamentals: Getting Started with Cloud Storage and Cloud SQL</summary>
  
  ```

gcloud config set project <WRITE_HERE_YOUR_PROJECT_ID>

gcloud compute instances create bloghost \
	--zone us-central1-a \
	--image-project debian-cloud \
	--image debian-9-stretch-v20200902 \
	--tags http-server \
	--metadata startup-script=apt\ update$'\n'apt\ install\ -y\ apache2\ php\ php-mysql$'\n'service\ apache2\ restart 

gcloud compute firewall-rules create default-allow-http \
	--allow tcp:80 \
	--target-tags http-server

gsutil mb gs://$DEVSHELL_PROJECT_ID
gsutil cp gs://cloud-training/gcpfci/my-excellent-blog.png gs://$DEVSHELL_PROJECT_ID/my-excellent-blog.png
gsutil acl ch -u allUsers:R gs://$DEVSHELL_PROJECT_ID/my-excellent-blog.png

export VM_IP=`gcloud compute instances describe bloghost --zone us-central1-a --format 'get(networkInterfaces[0].accessConfigs[0].natIP)'`

gcloud sql instances create blog-db --region us-central1

gcloud sql users set-password root \
	--instance blog-db \
	--host % \
	--prompt-for-password

gcloud sql users create blogdbuser \
	--instance blog-db \
	--host $VM_IP \
	--password blogdbuser

gcloud sql instances patch blog-db --authorized-networks $VM_IP/32

export DB_IP=`gcloud sql instances describe blog-db --format 'get(ipAddresses[0].ipAddress)'`

cat << EOF > index.php
<html>
<head><title>Welcome to my excellent blog</title></head>
<body>
<h1>Welcome to my excellent blog</h1>
<?php
\$dbserver = $DB_IP;
\$dbuser = "blogdbuser";
\$dbpassword = "blogdbuser";
\$conn = new mysqli(\$dbserver, \$dbuser, \$dbpassword);
if (mysqli_connect_error()) {
echo ("Database connection failed: " . mysqli_connect_error());
} else {
echo ("Database connection succeeded.");
}
?>
</body>
</html>
EOF

sed -i '/^<h1>.*/i <img src="https://storage.googleapis.com/'"$DEVSHELL_PROJECT_ID"'/my-excellent-blog.png">' index.php

cat index.php 

gcloud compute scp index.php bloghost:~/index.php --zone us-central1-a

gcloud compute ssh bloghost --zone us-central1-a 
	sudo cp index.php /var/www/html/index.php
	service apache2 restart

  ```

</details>
