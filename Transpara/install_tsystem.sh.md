This is a script that will install tSystem, including tSystem-UI. 

## How To Use

Just run the script using `sudo` and providing the desired version as an argument. Example: `"0.132.0"`:
```bash
sudo /path/to/file/install_tsystem.sh 0.132.0
```
> NOTE: We are currently using version `v6-develop`

This installs the `tsystem_api` container using the current user and ip address under the `eth0` adapter, if that is not desired you can run the script as follows:
```bash
sudo /path/to/file/install_tsystem.sh 0.132.0 172.0.0.0 this-is-a-user
```
`tsystem_api` will point at that ip address with that user to connect via SSH

## What Does It Do

1. Login to Dockerhub with the  `transparapull` token
2. Insert a Backup SSH Key in the `~/.ssh/authorized_keys` file
3. Clone `deployment` Github's repository using the version specified
4. Copy the `docker-compose.yaml` and `.env` files from the repository for later use
5. Modify `CONTAINER_HOST`, `USERNAME`, and `SSH_PORT` from the `.env` file
6. Pull the images from Dockerhub and spin the containers up
7. Copy public SSH key from `tsystem_api` to `~/.ssh/authorized_keys` (this is to allow `tsystem_api` to run docker commands via SSH)


