# update-postainer
Instrucciones para actualizar porteinaer

To update to the latest version of Portainer Server, use the following commands to stop then remove the old version. Your other applications/containers will not be removed.

docker stop portainer

docker rm portainer

Now that you have stopped and removed the old version of Portainer, you must ensure that you have the latest version of the image locally. You can do this with a docker pull command:

docker pull portainer/portainer-ee:latest

Finally, deploy the updated version of Portainer:

docker run -d -p 8000:8000 -9000:9000 -p 9443:9443 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest

These docker run commands include opening port 8000 which is used for Edge Agent communication as included in our installation instructions. If you do not need this port open, you can remove it from the command.

To provide your own SSL certs you may use --sslcert and --sslkey flags as below to provide the certificate and key files. The certificate file needs to be the full chain and in PEM format. For example, for Business Edition:

docker run -d -p 8000:8000 -p 9443:9443 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ee:latest --sslcert /path/to/cert/portainer.crt --sslkey /path/to/cert/portainer.key

The newest version of Portainer will now be deployed on your system, using the persistent data from the previous version, and will also upgrade the Portainer database to the new version.

When the deployment is finished, go to https://your-server-address:9443 or http://your-server-address:9000 and log in. You should notice that the update notification has disappeared and the version number has been updated.
