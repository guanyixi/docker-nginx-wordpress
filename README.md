# Boilder plate for install WordPress in Docker with nginx

## Before Start
1. Install docker desktop application in your computer.
2. Install brew.
3. Install mkcert globally: `brew install mkcert` and `brew install nss`.

## Steps
1. Clone this repo to your local computer. Rename the root folder to your project name.
2. Download the latest WordPress and copy the wordpress folder to the root folder. So the root folder should have 3 folders: /mysql/, /nginx/, and /wordpress/.
3. cd into /nginx/certs/, and run `mkcert yoursitename.dev`. 
4. Change domain name in docker-compose.yml from sitename.dev to yoursitename.dev.
5. Change domain name in /nginx/default.conf from sitename.dev to yoursitename.dev.
6. Stop other containers that may use the same port, cd into the root folder and run `docker-compose up -d --build`. This will build the container and start the container.
7. Add the domain to the host file by running `sudo code /etc/hosts` (for VSCODE), then add `127.0.0.1	yoursitename.dev` to the host file and save.
8. Visit https://yoursitename.dev and go through the installation process. The Database Host should be the server name: 'mysql', not 'localhost'.
9. Now the site should be running with SSL.
10. Connect to the database (Sequal Ace):
> * Host: 127.0.0.1
> * Username: yourusername
> * Password: yourpassword
> * Database: yourdatabasename
> * Port: 3306 (Same as the docker-compose.yml file under mysql)