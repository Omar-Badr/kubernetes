# kubernetes
1- Install kubectl

2- Install minikube

3- Install docker

4- Expose the docker environment from minikube to host
> eval $(minikube docker-env)

5- Creat the Project pod mapping a hostpath as a volume for the project to use the generated files in dockerizing the application. You must change hostpath path value below to match your environment and access permissions. the file is called:
- drkiq-first-step.yml

6- Run the "drkiq-first-step.yml" deployment file:
>$ kubectl create -f ./drkiq-first-step.yml

7- Go to the path specified in step "4" and modify the project files as advised

8- Delete the created pod
>$ kubectl delete pod drkiq

9- Created a Dockerfile and created the docker image drkiq:v1
>$ docker build -t drkiq:v1 .

10- Created a configmap file to contain the environmental variables instead of the env file

11- Created .dockerignore file as specified

12- Create two Persistent Volume Claims of a size of 200MiB with the following names:
- drkiq-postgres-pvc.yaml
- drkiq-redis-pvc.yaml

13- Run the Persistent Volumes claim files this would automatically create Persistent Volumes of type hostpath and pointing to the following path on the minikube host /tmp/hostpath-provisioner/"pvname"

14- To check the provisioned PVs use:
>$ kubectl get pv

15- Create a service file of NodePort type and selector app: drkiq to expose the needed ports of the drkiq container. Specify port the mapping between drkiq container port 8000 and host port 30001 in the service with the following name:
- drkiq-svc.yml

16- Create a service file expose the needed ports of postgres and redis containers with the following names:
- postgres-svc.yml
- redis-svc.yml

17- Create the deployment file for postgres, redis, drkiq and sidekiq with the following names:
- redis.yaml
- postgres.yaml
- drkiq.yaml
- sidekiq.yaml

18- Make sure that both drkiq and sidekiq share the same volume /drkiq which should be mapped to the same path on the host (it should be the same one specified in step 4)

19- Create a pod file to initialize the database for drkiq called:
- drkiq-second-step.yml

20- Run the service, configmap, postgres deployment, drkiq-second-step deployment and redis deployment files

21- Run the "drkiq-second-step.yml" file [Note: if you try to run the drkiq.yml it would fail with an error that database doesn’t exist]

22- Make sure that the db/schema.rb file was created in your work directory (it should be the same one specified in step 4)

23- Delete the drkiq pod
>$ kubectl delete pod drkiq

24- Run the drkiq deployment and sidekiq deployment file

25- Check the minikube ip

26- Head over to http://minikube_ip:30001/
You should be greeted with the typical Rails introduction page.
