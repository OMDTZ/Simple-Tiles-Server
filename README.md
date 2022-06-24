# Introduction

This is a straightforward technique for setting up a tile server that uses GDAL for processing imagery and a Nginx server to serve imagery tiles. It can be accessed locally through a local area network or remotely, from a distant server. When the server is deployed, it may serve imagery that may be viewed using QGIS, JOSM, and other relevant tools.
add 
The setup is fairly straightforward; all that is required is some patience to learn, a basic understanding of remote server management, and some knowledge of coding. Please share with us any better suggestions you may have for making this more useful.

## REQUIREMENTS…
- Linux operating system, If your using Window you should install putty (https://www.putty.org/)
- GDAL  library
- python
- QGIS (https://qgis.org/)
- git 
- Nginx (https://www.nginx.com/)
- Remote server (This could be any, AWS, Digital Ocean etc)

## PROCESSES

### Set up server
- This steps will focus on digital ocean, (https://docs.digitalocean.com/products/droplets/how-to/create/)
- While creating Instance, select ubuntu, ram 1 is enough and space it will depend on the size of your imagery
- Access the droplets using ssh, if your using linux (https://docs.digitalocean.com/products/droplets/how-to/connect-with-ssh/openssh/), If you are using window (https://docs.digitalocean.com/products/droplets/how-to/connect-with-ssh/putty/)
- Install the NGINX
  - sudo apt update 
  - sudo apt install nginx
  - After that, when you load your VM ip adress in the browser you should see "Welcome to NGINX"

### Uploading the imagery to the server 
After we are sure that, we can access the server from our local machine, the next procedure is to upload the imagery in to our tile server.
In this procedure, we are expecting to process the imagery in the remote server, but on other note the processing could be done 
in local machine then you just upload tiles directories.
- Prepare you imagery to be process, make sure is working fine by open it in qgis and pan around.
- Just for now, upload the imagery to the server using rsync, more detail here https://www.liquidweb.com/kb/how-to-securely-transfer-files-via-rsync-and-ssh-on-linux/

### Processing the imagery in the server
The main process is to read the imagery and export the individual tile leve in folder.
For the task, we will use the script made by our friend @ivangayton, 

- Clone the git repo https://github.com/HumanitarianStuff/tilehuria.git
- Navigate to the that gi repository
- Then execute the process; python3 read_mbtile.py $indfile then wait
  - The above script will give directories of the imagery tiles, from 0 to 21

### Setting up the server
The last procedure, dealing with files to set up the server
- ssh to the server, copy all the tiles directories to /var/www/html/
- copy the index script from this repo, to /var/ww/html/
- Modfy script a bit, most the set view, add coordinates of your areas of interest
