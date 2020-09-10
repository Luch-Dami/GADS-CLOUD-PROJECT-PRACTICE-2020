# Lab: Google Cloud Fundamentals: Getting Started with Compute Engine

## Objectives:
In this lab, you will learn how to perform the following tasks:
- Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.
- Create a Compute Engine virtual machine using the gcloud command-line interface.
- Connect between the two instances.

### Steps:
1. Create a Compute Engine virtual machine named `my-vm-1` using the Google Cloud Platform (GCP) Console.
 - To list all the zones in the region and filter the result associated with the us-central1 region that was assigned by qwiklabs, use the following command: 
```
    gcloud compute zones list | grep us-central1  
```
 - Set the config default compute zone with the following command:  
```    
gcloud config set compute/zone us-central1-b
```
 - Create the instance on the default network:
```
    gcloud compute instances create "my-vm-1" --machine-type "n1-standard-1" --image-project "debian-cloud" --image "debian-9-stretch-v20190213" --
	subnet "default" --tags http-server
```
2. Create a Compute Engine virtual machine named `my-vm-2` using the gcloud command-line interface:
 - To create a VM instance called `my-vm-2`:
```
    gcloud compute instances create "my-vm-2" --machine-type "n1-standard-1" --image-project "debian-cloud" --image "debian-9-stretch-v20190213" --
	subnet "default"
```
3.Connect between the two instances:
  - To SSH to my-vm-2, use the command:
```
    gcloud compute ssh my-vm-2
```
  - Use the ping command to confirm that my-vm-2 can reach my-vm-1 over the network:
```    
ping my-vm-1
```    
Use CTRL C to Stop
  - Use the ssh command to open a command prompt on my-vm-1:
 ```
  ssh my-vm-1
``` 
  - At the command prompt on my-vm-1, install the Nginx web server:
```
    sudo apt-get install nginx-light -y
```
  - Use the nano text editor to add a custom message to the home page of the web server
```
sudo nano /var/www/html/index.nginx-debian.html
```
  - Use the arrow keys to move the cursor to the line just below the h1 header. Add text like this, and replace YOUR_NAME with your name:
    ```
Hi from YOUR_NAME
```
  - Press Ctrl+O and then press Enter to save your edited file, and then press Ctrl+X to exit the nano text editor.

  - Confirm that the web server is serving your new page. At the command prompt on my-vm-1, execute this command:
```    
curl http://localhost/
```  
The response will be the HTML source of the web server's home page, including your line of custom text.
  - To exit the command prompt on my-vm-1:
    ```
    exit
    ``` 
  - To confirm that my-vm-2 can reach the web server on my-vm-1,at the command prompt on my-vm-2, execute this command:
    ```
    curl http://my-vm-1/
    ```
The response will again be the HTML source of the web server's home page, including your line of custom text.

  - To access the IP address of my-vm-1 instance, execute this command:
    ```
    gcloud compute instance list
    ```
  - Copy and paste the IP address of my-vm-1 to a new browser tab and press Enter.

   Result: You will see your web server's home page, including your custom text.