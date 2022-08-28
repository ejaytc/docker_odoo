## Docker and Odoo Cheat Sheet


#### Logs via Docker
```
  docker logs -f [container]
```
#### Keyboard Shortcut `ESC + u (undo)`


#### Docker Restore and DB AND Create Database
```
docker exec -i [db_container] createdb [db_name] -O odoo -U odoo
```

## Restoring Databases via command line

  1. `docker exec -i [db_container] createdb [Database Name] -O odoo -U odoo [db_name]`
  2. `cat [backup_db] | docker exec -i [db_container] psql -U odoo -d [db_name]`
  3. `gunzip [backup_file] -c | docker exec -i odoodocker_db_1 psql -U odoo -d [db_name]`


#### Delete Model
```
docker exec -i [db_container] psql -U odoo -d [db_name]
delete from ir_model where model = [model_name];
```


#### Update Admin Password
```
docker exec -i [db_container] psql -U odoo -d [db_name]
update res_users set password = 1 where id = 2;

```
- `\q` to quit


#### Scaffold
```
docker exec -it --user root [web_container] bash /usr/bin/odoo scaffold [module_name] /mnt/extra-addons


ctrl + D
chmod 755  the_path_to_target
sudo chmod 775 -R projectname/   
sudo chown username -R projectname/
```


#### Checking Logs
```
docker logs [container]

docker logs [container] | grep [search_text]

docker logs -f [container]

docker-compose logs -f

docker-compose logs

docker-compose restart web && docker-compose logs -f --tail=10 web

docker-compose logs -f --tail=10 web
```

#### Removing of volume specific container
```
docker rm [container]
docker volume rm [container]
```

#### Build Dockerfile
```
docker-compose up --build
```

## Run Docker commands without sudo (Linux)
1. Add the docker group if it doesn't exist
    ```
    $ sudo groupadd docker
    ```

2. Add the connected user $USER to the docker group
    - Optionally change the username to match your preferred user.
    ```
    $ sudo gpasswd -a $USER docker
    ```


#### Access bash of docker
```

docker exec -it [web_container] /bin/bash
```

#### Scaffold within the bash
```
usr/bin/odoo scaffold [new_module_name] /mnt/extra-addons
```

#### Copy Within the Container
```
docker cp [web_container]:"mnt/extra-addons/[new_module_name]" "C:\Users\<User>\Documents\[project_folder]\[odoo_folder]\addons"
```


#### Install Python Depedencies for Odoo
Create Docker file: `DockerFile`
- Temnplate
```
From odoo: [version]
USER: root
RUN [Commands for installing packages.]
```

- To rebuild
- uncomment `build: .` in `docker-compose.yml`
- Then run  the command
```
docker-commpose up --build
```


