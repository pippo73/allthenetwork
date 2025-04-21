This is a repository to try to understand how to deploy CF with traefik
Hera are the instructions how I did it

The idea is to have the following  schema

Here are the steps I've done

1) creat a swarm
2) create a network
docker network create --driver overlay traefik-network
3) on cloudflare create a tunnel and copy the string to deploy a docker (we will need the tocken)
4) create the docker secret string
printf "the cf token" | docker secret create my_secret_data -

5) deploy the cloudflared service
docker stack deploy -c CF.yaml cloudflare_tunnel
6) check if everything is ok
$ docker service ls
ID             NAME                           MODE         REPLICAS   IMAGE                           PORTS
qjx9ik0r4o38   cloudflare-stack_cloudflared   replicated   1/1        cloudflare/cloudflared:latest

If everything is ok now it is time do deploy traefik

7) 
