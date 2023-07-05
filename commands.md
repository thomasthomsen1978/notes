thth's command list
====================================

# git

``` shell


    git checkout -b <new_branch_name> <origin_branch_name>

    git checkout -b some_branch origin/some_branch

```

# Powershell

```shell
    
    # Set alias. Note: is deleted when teminal is closed
    Set-Alias <shortcut> <command>
    
    # ex.: Set alias
    Set-Alias k kubectl

```

# Bash

``` shell

    # https://linuxconfig.org/bash-scripting-tutorial
    
    # get date in year, month and day
    # execution of a bash script inside another script: $(...some command, eg. 'uname -o', or $(date) as below)
    file_name=myhome_directory_$(date +%Y%m%d).tar.gz
    
    # https://www.tutorialspoint.com/linux-tar-command

    # create tar file
    # c: create an archive file
    # z: create a tar file using gzip compression
    # f: specifiy the name of the archive file
    tar -czf $file_name . 

    # result: an archived file with the name (depending on date) 'myhome_directory_20230531.tar.gz'


    # https://linuxconfig.org/bash-scripting-tutorial

    # using passed arguments

    # use arguments
    echo $1 $2 $3

    # arguments can be stored in a special array
    args=("$@")

    # echo arguments to the shell
    echo "Whole list of arguments: " $@
    echo "Selected arguments: " ${args[0]} ${args[2]}
    echo "Number of arguments: " $#


```

# Helm

### repositories

``` shell

    # https://helm.sh/docs/intro/using_helm/

    # https://helm.sh/docs/helm/helm_repo_add/

    # add repository
    helm repo add <repository_name> <url>

    # ex.: specific repositories
    helm repo add stable https://charts.helm.sh/stable
    helm repo add bitnami https://charts.bitnami.com/bitnami

    # https://helm.sh/docs/helm/helm_repo_list/

    # list of added repositories
    helm repo list


    # https://helm.sh/docs/helm/helm_repo_update/

    # update information of available charts locally from chart repositories
    helm repo update


    # https://helm.sh/docs/helm/helm_search_repo/

    # search within all repositories
    helm search repo <keyword>

    # search within specific repository
    helm search repo <repository>/<keyword>

    # see versions
    helm search repo <whatever_method> --versions

    # ex.: search
    helm search repo mysql
    helm search repo stable/mysql
    
```

### install/upgrade/rollback/uninstall release

```shell

    # https://helm.sh/docs/helm/helm_install/

    # deploy a chart based on its name
    helm install <release_name> <repository>/<chart>

    # ex.: deploy a chart based on its name
    helm install my-sql stable/mysql

    # deploy a chart based on a file in the local folder
    helm install -f <file> <release_name>

    # deploy a chart from a certain folder
    # the folder path must contain a valid file structure of a chart 
    # - see 'helm create ...'
    helm install <release_name> <path_to_folder_with_helm_files>        

    # deploy a chart based on a repository
    helm install --repo <url>

    # install a specific version
    helm install <whatever_method> --version <version_string>

    # ex.: install specific version
    helm install my-sql stable/mysql --version 1.6.3 

    # ex.: install and set a flag (in this case to be able to push a chart to it)
    helm install chartmuseum stable/chartmuseum --set env.open.DISABLE_API=false

    
    # https://helm.sh/docs/helm/helm_upgrade/

    # upgrade release
    helm upgrade <release_name> <repository>/<chart> --version <new_version>

    
    # https://helm.sh/docs/helm/helm_rollback/

    # rollback a deployment
    helm rollback <release_name> <revision_number>

    # ex.: rollback a deployment (assume latest revision number to be '5')
    helm rollback my-sql 2


    # https://helm.sh/docs/helm/helm_uninstall/

    # Uninstall a release
    helm uninstall <release_name>

    # Uninstall a release and keep history to show uninstalled state
    helm uninstall <release_name> --keep-history


```

### get information

#### releases
```shell

    # https://helm.sh/docs/helm/helm_get_all/

    # get all information about a release
    helm get all <release_name>


    # https://helm.sh/docs/helm/helm_get_manifest/

    # get manfest of a release
    helm get manifest <release_name>


    # https://helm.sh/docs/helm/helm_get_values/

    # get values from release
    helm get values <release_name>


    # https://helm.sh/docs/helm/helm_get_notes/

    # get notes about repository
    helm get notes <release_name>


    # https://helm.sh/docs/helm/helm_status/

    # status of a release
    helm status <release_name>


    # https://helm.sh/docs/helm/helm_list/
    
    # show all running releases
    helm list

    # show all releases, incl. any uninstalled ones
    helm list --all

```

#### repositories

```shell


    # https://helm.sh/docs/helm/helm_history/

    # get helm history
    helm history <repository>


    # https://helm.sh/docs/helm/helm_show_all/

    # show all information of a chart
    helm show all <repository>/<chart>


    # https://helm.sh/docs/helm/helm_show_chart/

    # show chart's definition
    helm show chart <repository>/<chart>
    
    # ex.: show chart's definition
    helm show chart stable/mysql


    # https://helm.sh/docs/helm/helm_show_readme/

    # show chart's readme file
    helm show readme <repository>/<chart>

    # show chart's readme file
    helm show readme stable/mysql


    # https://helm.sh/docs/helm/helm_show_values/

    # show chart's values
    helm show values <repository>/<chart>
 ```

#### helm
 ```shell

    # https://helm.sh/docs/helm/helm_env/

    # helm environment
    helm env


    # https://helm.sh/docs/helm/helm/

    # use help to find certain paths, eg. the file containing repository names and urls: C:\\Users\\<some_user>\\AppData\\Roaming\\helm\\repositories.yaml
    helm --help

```

#### packages

```shell

    # https://digitalvarys.com/helm-part-2-helm-chart-files-and-folder-structure-tutorial/

    # https://helm.sh/docs/chart_template_guide/functions_and_pipelines/

    # https://helm.sh/docs/helm/helm_pull/

    # download and unpack a chart's file structure from a repository and (optionally) unpack it in local directory
    helm pull <repository>/<chart> --untar


    # https://helm.sh/docs/helm/helm_create/
    
    # create default chart structure in local folder
    helm create <chart_name>

    # file & folder structure:
    # |-- ./charts
    # |-- ./templates
    # |   |-- ./tests
    # |   |-- _helpers.tpl
    # |   |-- deployment.yaml
    # |   |-- hpa.yaml
    # |   |-- ingress.yaml
    # |   |-- NOTES.txt
    # |   |-- service.yaml
    # |   |-- serviceaccount.yaml
    # |-- .helmignore
    # |-- Chart.yaml
    # |-- values.yaml


    # https://helm.sh/docs/helm/helm_package/

    # package a chart directory into a chart archive (<chart_name>-<version>.tgz)
    helm package <chart_path>

    # package a chart directory into a chart archive in some specified folder
    helm package <chart_path> --destination <path>

```

# Docker

### general

```shell

    # general info
    docker info

```


### pull images

``` shell

    # https://docs.docker.com/engine/reference/commandline/pull/
    
    # Download image from docker repo
    docker pull <image_name>:<version>

    # Download image from docker repo (alternative)
    docker image pull <image>:<version>

    # ex. (OS) : will download the latest version
    docker pull ubuntu

    # ex. (OS) : will download a specific version
    docker pull ubuntu:jammy

    # ex. (web server) : show message if running successfully
    docker pull nginx

    # ex. (terminal) : print message in terminal
    docker pull hello-world

    # ex. (wordpress) : sample page
    docker pull bitnami/wordpress

    # pull all images from the repo
    # be careful: may pull a lot
    docker pull --all-tags <image>
```

### list images

```shell

    # https://docs.docker.com/engine/reference/commandline/images/

    # list all images
    docker images
    docker image ls

    # ex.: list images from the ubuntu repo
    docker images ubuntu

    # ex.: list image from repo with version
    docker images ubuntu:jammy

    # list untagged images
    docker images --filter "dangling=true"

    # ex.: list images prior to an image
    docker images --filter "before=ubuntu"

    # ex.: list images later than an image
    docker images --filter "since=ubuntu"

    # ex.: list images in a certain format
    docker images --format "{{.ID}} : {{.Tag}} : {{.Size}}"

```

### list containers

```shell

    # https://docs.docker.com/engine/reference/commandline/ps/

    # list running containers
    docker ps
    docker container ls

    # list all containers incl. non-running
    docker ps -a

    # list only running container's IDs
    docker ps -q

```

### create and run containers

```shell

    # https://docs.docker.com/engine/reference/commandline/run/
    
    # create and run a container from an image
    docker run <image>

    # create and run a container in the background and print container id
    docker run --detach <image>
    docker run -d <image>

    # create and run a container and remove it, when it terminates
    docker run --rm <image>

    # create and run a container with specified name
    docker run --name <some_name> <image>

    # create and run a container and publish its port(s) to the host
    docker run --publish <host_ip>:<host_port>:<container port> <image>
    docker run -p <...>

    # ex.: create and run nginx, publish its port 80 to 127.0.0.1
    docker run -p 127.0.0.1:8000:80 nginx
    docker run -p localhost:8000:80 nginx
    docker run -p 8000:80 nginx

    # all three commands will give the same results -> check in browser:
    # 127.0.0.1:8000 -> "Welcome to nginx"
    # localhost:8000 -> "Welcome to nginx"

    # log into an interactive shell on the container
    docker run --interactive --tty <image> /bin/bash
    docker run -it <image> /bin/bash

```

### start/stop containers

```shell
 
    # https://docs.docker.com/engine/reference/commandline/start/

    # start container
    docker start <container_name>
    docker start <container_id>

    # stop container
    docker stop <container_name>
    docker stop <container_id>

    # stop container after a specified time interval
    docker stop --time=<time_in_seconds> <container_name/id>
    docker stop -t=<time_in_seconds> <container_name/id>

    # stop all running containers
    docker stop $( docker ps -aq )

```

# remove images/containers

```shell

    # https://docs.docker.com/engine/reference/commandline/rmi/
    # https://docs.docker.com/engine/reference/commandline/rm/

    # remove image by image id
    docker rmi <image_id>

    # remove image by name and tag
    docker rmi <repo>:<tag>

    # ex.: remove image by name and tag
    docker rmi nginx:1.11.12
    docker rmi nginx:latest

    # force removal
    docker rmi --force <image_id>
    docker rmi -f <image_id>

    # remove stopped container
    docker rm <container_name>
    docker rm <container_id>

    # remove running container
    docker rm --force <container_name/id>
    docker rm -f <container_name/id>

    # remove a container and its volume
    docker rm --volumes <container_name/id>
    docker rm -v <container_name/id>

    # remove all stopped/running containers
    docker rm $( docker ps --filter status=exited -q )
    docker rm --force $( docker ps --filter status=running -q )

```

### commands in container 

```shell

    # execue commands in container
    docker exec <container_name/id> <command>

    # ex.: create file
    docker exec <container_name/id> touch /tmp/some_file.txt

    # log into an interactive shell
    docker exec -it <container_name/id> /bash/bin

    # log in as some user
    docker exec -u <user> -it <container_name/id> /bin/bash

    # ex.: log in as root
    docker exec -u root -it <container_name/id> /bin/bash

```

# Kubernetes

### cluster

```shell

    # https://birthday.play-with-docker.com/kubernetes-docker-desktop/

    # https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#cluster-info
    kubectl cluster-info
```

### create/update resources

```shell

    # https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#create

    # create a new resource from a file
    # if the resource is already running, an error will be shown
    kubectl create -f <file_name>

    # ex.: create a new resource from a file
    kubectl create -f nginx.pod.yaml

    # save the current configuration in the file
    kubectl create -f <file_name> --save-config


    # https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#-em-deployment-em-

    # create deployment
    kubectl create deployment <deployment_name> --image=<image_name>

    # create a deployment that can be piped to a file (deployment.yaml) and used in a helm chart (in the 'templates'-folder)
    kubectl create deployment <deployment_name> --image=<image_name_to_build_from> --dry-run=client --output=yaml

    # create a service that can be piped to a file (services.yaml) and used in a helm chart (in the 'templates'-folder)
    kubectl expose deployment <deployment_name> --type=<type_of_service> --port=<port_number> --dry-run=client --output=yaml

    # ex.: create service that can be piped to a file (services.yaml)
    kubectl expose deployment nginx --type=LoadBalancer --port=80 --dry-run=client --output=yaml


    # https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply

    # apply configuration to a running resource
    # if it is not running, a new one will be created
    kubectl apply -f <file_name>


    # https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#delete

    # delete a running resource immediately
    kubectl delete -f <file_name>

```


### get information

``` shell

    # https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get

    # show all
    kubectl get all

    # show specific resource
    kubectl get <resource_kind>

    # ex.: show specific resources
    kubectl get pods     
    kubectl get services
    kubectl get storageclasses
    kubectl get nodes

    # determine output format
    kubectl get <resource_kind> <resource_name> -o <extension>

    # ex.: describe pod in yaml and json
    kubectl get <resource_name> -o yaml
    kubectl get <resource_name> -o json


    # https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#describe

    # describe resources
    kubectl describe <resource_kind> <resource_name>


    # https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#logs

    # show logs
    kubectl logs <resoruce_name> 


    # https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#exec

    # execute commands in a container
    kubectl exec --stdin --tty <resource_name> -- <command>

    # ex.: step into shell
    kubectl exec --stdin --tty <resource_name> -- sh

```

# curl