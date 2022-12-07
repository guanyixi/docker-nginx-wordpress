# Boilerplate for setting up a WordPress site in Docker with nginx

## Before Start
* Install docker desktop application in your computer.
* Install brew. This is for installing mkcert. You can also use Curl.
* Install mkcert globally: `brew install mkcert` and `brew install nss`. The first command installs mkcert. The second command installs a certutil to allow Firefox to trust the CA.

## Steps
1. Clone this repo to your local computer. Rename the root folder to your project name.
2. Download the latest WordPress and copy the wordpress folder to the root folder. So the root folder should have 3 folders: /mysql/, /nginx/, and /wordpress/.
3. cd into /nginx/certs/, and run `mkcert yoursitename.dev`. 
4. Change domain name in docker-compose.yml from sitename.dev to yoursitename.dev.
5. Change domain name in /nginx/default.conf from sitename.dev to yoursitename.dev.
6. Stop other containers that may use the same port, cd into the root folder and run `docker-compose up -d --build`. This will build the container and start the container.
7. Add the domain to the host file by running `sudo code /etc/hosts` (for VSCODE), then add `127.0.0.1	yoursitename.dev` to the host file and save.
8. Visit https://yoursitename.dev and go through the installation process. The Database Host should be the server name: 'mysql', not 'localhost'.
9. Now the site should be up and running with SSL.
10. Connect to the database (Sequal Ace):
> * Host: 127.0.0.1
> * Username: yourusername
> * Password: yourpassword
> * Database: yourdatabasename
> * Port: 3306 (Same as the docker-compose.yml file under mysql)

## Notes
* When building containers with custom configurations, you can't user images directly. Instead, you need to use docker files. Eg. nginx.dockerfile, php.dockerfile. For building containers like this, you need to run `docker-compose build` instead of `docker-compose up`. You can also just run `docker-compose up -d --build` to build and start the container.
* The /mysql/ directory is to store the mysql volume, so when you stop the container, you won't lose any data.
* in docker-compose.yml `platform: linux/x86_64` is used to avoid error "no matching manifest for linux/arm64/v8 in the manifest list entries" when building the container. This happens when you are using a Mac with M1 chip.
* Your database root password can not be "root". Otherwise it will cause error Access denied for user 'root'@'172.27.0.1’ when trying to connect the database.