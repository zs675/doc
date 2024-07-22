# gitlab deployment manual

## 1.  official home page

[Install GitLab by using Docker](https://docs.gitlab.com/ee/install/docker.html)

## 1. image

```
docker pull gitlab/gitlab-ce:16.2.0-ce.0
```

## 2. crate directory

```
mkdir -p /data/gitlab
```

## 3.  add  env `GITLAB_HOME`

```
echo 'export GITLAB_HOME1=/data/gitlab' >>  ~/.bashrc
```

reenter terminal

## 4. start docker container

```
sudo docker run --detach \
  --hostname 192.168.168.168 \
  --env GITLAB_OMNIBUS_CONFIG="external_url 'http://192.168.168.168:18080'; gitlab_rails['gitlab_shell_ssh_port'] = 18022" \
  --publish 18080:18080 --publish 18022:22 \
  --name gitlab \
  --restart always \
  --privileged=true \
  --volume $GITLAB_HOME/config:/etc/gitlab \
  --volume $GITLAB_HOME/logs:/var/log/gitlab \
  --volume $GITLAB_HOME/data:/var/opt/gitlab \
  --shm-size 256m \
  gitlab/gitlab-ce:16.2.0-ce.0
```

## 5. login

- enter gitlab container

  ```
  docker exec -it gitlab bash
  ```

- view password

  ```
  cat /etc/gitlab/initial_root_password
  ```

- login

  username: root
  
  password: