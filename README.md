# Working examples for Docker using Docker compose and Docker Swarm
Images pull directly from dockersamples/ repo
* **Redis** - frontend voting, database redis
* **Voting** - frontend voting, python app on port 5000:80
* **DB** - backend database, postgres, default username & password
* **Result** - backend dashboard, express/nodejs app on port 5001:80
* **Worker** - backend processing, C# app need redis & DB

## Docker Swarm (single cluster, 1 replica for all images)
`docker stack deploy STACK-NAME --compose-file=docker-stack.yml`
* replace STACK-NAME with voting-app maybe
* Check stack `docker stack ls`
* Check services `docker service ls`

## Docker Compose (single host, single task/container)
`docker compose up -d`
* Will remove obsolete links later
* Compose v3, old one might use `docker-compose up`
* Check `docker ps -a`

## k8 single cluster, single pod setup
* Apps' name were hard coded inside source codes e.g Redis(host="redis"), OpeRedisConnection("redis") (no3 of 12factor)
* We will use Service name exactly like their hard coded in code based, except **Worker** no service/user consume this
* **DB**, **Redis** don't need to expose to external (least privilege), ClusterIP 
* Expose **Voting**, **Result**, NodePort

`kubectl get pod,svc,deploy` to check running services, deployments and pods (`all` could do the job)

### Running pods
`kubectl create -f voting-app.yaml` 
### Running services
* We don't need to access worker pod
* First we will exposse NodePort to user facing service like voting & result
* We will have ClusterIP to make a stable connection, redis and db services 
* Later we will change NodePort to LoadBalancer to host on aws, gcp or azure
### Running deployments

