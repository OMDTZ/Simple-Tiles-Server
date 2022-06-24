# Introduction

This is a straightforward technique for setting up a tile server that uses GDAL for processing imagery and a Nginx server to serve imagery tiles. It can be accessed locally through a local area network or remotely, from a distant server. When the server is deployed, it may serve imagery that may be viewed using QGIS, JOSM, and other relevant tools.
add The setup is fairly straightforward; all that is required is some patience to learn, a basic understanding of remote server management, and some knowledge of coding. Please share with us any better suggestions you may have for making this more useful.

## REQUIREMENTS…
- Linux operating system, If your using Window you should install putty (https://www.putty.org/)
- GDAL  library
- python 3 
- QGIS
- git 
- Nginx web serving
- josm 


## PROCESSES
install the following if not installed in your computer, open command terminal and inter the following commands

- Deploy the instance, or VM
  - For Digital Ocean
  - For AWS
- Set- up your VM, users, permission. Example below for AWS
  - Launch a new EC2 instance (Launch Instance)
    - Select Ubuntu Server 16.04 LTS 64-bit
    - Select a t2.small instance (1 vCPU, 2GB RAM)
    - Give it at least 20GB of storage (50 is better)
    - Once the Amazon instance is running, you need to set up a security group before you can SSH into it. Add a rule for SSH, from any IP address. If this is the first time, create a new security group:
    - Add the following rules:
    - SSH | TCP | port 22 | Anywhere HTTP | TCP | port 80 | Anywhere HTTPS | TCP | port 442 | Anywhere

    - Create a key pair (we used the downloaded .pem file provided by Amazon)

    - Amazon instance require a public key .pem file (the normal id_rsa that you may already have doesn't appear in the list of selectable keys). Maybe there's a way to upload your normal id_rsa_pub...
    - Set up domain name service  
    - Now go the Amazon Route 53 console and create a Hosted Zone 
    - Copy the Amazon nameservers from NS row to your domain registrar (we use Namecheap, and in NAMESERVERS area enter Custom DNS and the four Amazon names (without the period at the end, i.e. ns-1333.awsdns-38.org and so on)
    - Set two A records (example.com and www.example.com), both pointing to the IP address of your EC2 instance 
    - Set one CNAME (*.example.com, value = example.com)
    - Connect to the server  
    - ssh -i /path/to/mykey.pem ubuntu@example.com
- Inatall GDAL library (sudo apt-get install gdal)
- python (sudo apt-get install python3 or use $ sudo apt-get install python3-gdal)
- git (sudo apt-get install git)
- Nginx web serving (sudo apt-get install nginx)
- josm (sudo apt-get install qgis)

- Spin up a server.
- Get an Amazon AWS account, Digital ocean or any other server providers
- for AWS, Go to the AWS console (console.aws.amazon.com), go to the Compute -> EC2 page
- 

## Prep the server and create a user (we're using the name hot-admin as an example).

- sudo adduser hot-admin    # Enter password, name, etc 
- sudo usermod -aG sudo hot-admin 
- sudo mkdir /home/hot-admin/.ssh 
- sudo cp .ssh/authorized_keys /home/hot-admin/.ssh/ 
- sudo chown hot-admin /home/hot-admin/.ssh/authorized_keys 
- Now you can exit from your ssh session and ssh back in using your username 
- ssh -i .ssh/mykey.pem hot-admin@example.com 
- You have to set up Git with your username 
- git config --global.user.name username 

git clone https://github.com/ivangayton/setup-scripts/various

