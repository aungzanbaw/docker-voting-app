# Working examples for Docker using Docker compose and Docker Swarm
Images pull directly from dockersamples/ repo
* **Redis** - frontend voting, database redis
* **Voting** - frontend voting, python app on port 5000:80
* **DB** - backend database, postgres, default username & password
* **Result** - backend dashboard, express/nodejs app on port 5001:80
* **Worker** - backend processing, C# app need redis & DB

## Docker Swarm (single cluster 1 replica for all images)
`docker stack deploy STACK-NAME --compose-file=docker-stack.yml`
* replace STACK-NAME with voting-app maybe
* Check stack `docker stack ls`
* Check services `docker service ls`

## Docker Compose (single host, single task/container)
`docker compose up -d`
* Will remove obsolete links later
* Compose v3, old one might use `docker-compose up`
* Check `docker ps -a`