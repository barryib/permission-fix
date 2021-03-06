What is the purpose of this permission fix?
See this issue:
https://github.com/docker/docker/issues/22258#issuecomment-247059898

What is this solution doing?
It's a simple mapping from your user/group to a user/group inside the docker.

How to use this?

1) Clone the Repo

2) Go inside your repo folder and set the permissions
```
chmod +x tools/entrypoint tools/permission_fix
```

3) Fit the docker-compose.yml to your settings
```
VOLUME: '/www' (The Volume you want to chown after setting the permission fix)
DOCKER_USER: 'www-data' (The User inside the docker)
DOCKER_GROUP: 'www-data' (The group inside the docker)
HOST_USER_ID: 1002 (Your User ID, by default in the docker it's 0 for the root user)
HOST_GROUP_ID: 999 (Your Group ID, by default in the docker it's 0 for the root user)
```

4) Let's go
```
docker-compose up -d
```

5) Need proof? OK!
```
docker-compose exec nginx bash
```

6) Inside the Docker...
```
ls -la /www
```

Now we mapped this:
User: 
Host 1002 <-> Docker www-data
Host 999 <-> Docker www-data



If you have any questions, feel free to ask! I just want everybody to understand :-)
