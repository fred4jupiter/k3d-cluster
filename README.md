# simple k3d cluster with config

This creates a simple k3d cluster with a docker registry.

Creating the cluster

    k3d cluster create --config docker-cluster-config.yaml

Deleting the cluster:

    k3d cluster delete --config docker-cluster-config.yaml

Starting the cluster:

	k3d cluster start docker-cluster

Stopping the cluster:

    k3d cluster stop docker-cluster

Be sure to map your local registry in your hosts file:

    127.0.0.1 docker-registry.localhost

Check that the registry is running:

    docker ps -f name=docker-registry.localhost

Tag image and upload in local running docker registry:

    docker tag nginx docker-registry.localhost:5000/nginx
    docker push docker-registry.localhost:5000/nginx

You can check if the image has been uploaded successfully:

    curl http://docker-registry.localhost:5000/v2/_catalog

Run that image in k3d:

    kubectl run nginx --image=docker-registry.localhost:5000/nginx