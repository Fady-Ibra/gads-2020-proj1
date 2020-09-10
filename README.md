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
  
  <summary>Translation labs Google Cloud Platform Fundamentals - Core Infrastructure: Lab 1</summary>
  
  ```
gcloud config set project <WRITE_HERE_YOUR_PROJECT_ID>

gcloud compute instances create my-vm-1 \
	--zone=us-central1-a \
	--image-project=debian-cloud \
	--image=debian-9-stretch-v20200902 \
	--tags=http-server 

gcloud compute firewall-rules create default-allow-http \
	--allow tcp:80 \
	--target-tags http-server

gcloud compute instances create my-vm-2 \
	--zone=us-central1-b \
	--image-project=debian-cloud \
	--image=debian-9-stretch-v20200902 \

gcloud compute ssh --zone us-central1-b my-vm-2
	
	ping -c 2 my-vm-1
	sudo su -
	ssh my-vm-1
		sudo su -
		apt -y install nginx-light 
		curl http://localhost/
		sed -i '/^<h1>.*/a Hello from Fady!' /var/www/html/index.nginx-debian.html
		curl http://localhost/
		exit
		exit
	curl http://my-vm-1/
	exit
	exit
VM_IP=`gcloud compute instances describe my-vm-1 --zone us-central1-a --format 'get(networkInterfaces[0].accessConfigs[0].natIP)'`
curl http://$VM_IP
  ```

</details>
