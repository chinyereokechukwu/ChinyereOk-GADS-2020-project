# Lab:Getting Started with Compute Engine

## Objectives

In this lab, you will learn how to perform the following tasks:

  •Create a Compute Engine virtual machine using the Google Cloud Platform (GCP) Console.

  •Create a Compute Engine virtual machine using the gcloud command-line interface.

  •Connect between the two instances.

## Steps:

### Create a virtual machine using the GCP Console

        gcloud compute instances create my-vm-1  --machine-type "n1-standard-1"  --image-project "debian-cloud"  --image "debian-9-stretch-v20190213" 
        --subnet "default" --tags http

        gcloud compute firewall -rules create allow-http --action=ALOW --destination=INGRESS --rules=http


### Create a virtual machine using the gcloud command line

        gcloud config set compute/zone us-central1-b

        gcloud compute instances create my-vm-2 --machine-type "n1-standard-1"  --image-project "debian-cloud" --image "debian-9-stretch-v20190213" --subnet "default"

 
### Connect between VM instances

  1.Use the ping command to confirm that my-vm-2 can reach my-vm-1 over the network:
  
         connect to my vm-2:

         gcloud compute ssh my-vm-2

   ping my-vm-1 from my-vm-2:
 
         ping -c 4 my-vm-1
    
   
  2.Use the ssh command to open a command prompt on my-vm-1:

         ssh my-vm-1
     

  3.At the command prompt on my-vm-1, install the Nginx web server:

        sudo apt-get install nginx-light -y

  4.Use the nano text editor to add a custom message to the home page of the web server:

        sudo nano /var/www/html/index.nginx-debian.html


  5.Use the arrow keys to move the cursor to the line just below the h1 header.Add text like this, and replace YOUR_NAME with your name:

         Hi from CHINYERE


  6.Press Ctrl+O and then press Enter to save your edited file, and then press Ctrl+X to exit the nano text editor.


  7.Confirm that the web server is serving your new page. At the command prompt on my-vm-1, execute this command:

         curl http://localhost/

   Result:The response will be the HTML source of the web server's home page, including your line of custom text.

  The response will be the HTML source of the web server's home page, including your line of custom text.


  8.To exit the command prompt on my-vm-1, execute this command:

         exit

  9.You will return to the command prompt on my-vm-2


  10.To confirm that my-vm-2 can reach the web server on my-vm-1, at the command prompt on my-vm-2, execute this command:

         curl http://my-vm-1/

   Result:The response will again be the HTML source of the web server's home page, including your line of custom text.


  11.Now get the external IP of the my-vm-1 instances from this command:

        gcloud compute instances list --zone us-central1-a

   Copy the External IP address for my-vm-1 and paste it into the address bar of a new browser tab. You will see your web server's home page, including your custom text.


