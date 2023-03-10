# kafka-distributed-system

## Introduction
This project is an implementation of a distributed system for processing IoT captor data using Kubernetes, Kafka and Elastic Cloud.

## Target Architecture
![project architecture](project-workflow.png "Project Architecture")

# Tutorial

## Deploy Strimzi Kafka Operator
<code>kubectl create namespace kafka</code>

<code>kubectl create -f 'https://strimzi.io/install/latest?namespace=kafka' -n kafka</code>

## Deploy Kafka broker and Zookeper
<code>kubectl apply -f kafka-base/kafka-persistent.yaml -n kafka</code>

## Deploy Kafka Bridge
<code>kubectl apply -f kafka-base/kafka-bridge -n kafka</code>

## Ingress Controller
<code>kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.5.1/deploy/static/provider/cloud/deploy.yaml</code>

## Nginx and Ingress
<code>kubectl get svc --all-namespaces</code>

Next you should lookup for the CLUSTER-IP of the kafka-bridge service and paste it the conf file on nginx upstream. 

<code>kubectl create configmap nginx-config --from-file=ingress/nginx.conf -n kafka</code>

<code>kubectl apply -f ingress/nginx.yaml -kafka</code>

<code>kubectl apply -f ingress/ingress-bridge.yaml -n kafka</code>

<code>kubectl get ingress -n kafka</code>

You can now see the public IP that you can use to interact with your kafka cluster.

To test, use curl:

<code> curl -v <INGRESS_IP>/healthy </code>

You should get a status response of 200.

## Kafka Connect


## Deploy ElasticSearch

<code> kubectl create -f https://download.elastic.co/downloads/eck/2.5.0/crds.yaml</code>

<code> kubectl apply -f https://download.elastic.co/downloads/eck/2.5.0/operator.yaml -n elastic-system </code>

<code> kubectl create namespace elastic </code>

<code> kubectl create -f elastic/elasticsearch.yaml -n elastic </code>




### Useful ressources:
https://www.elastic.co/guide/en/cloud-on-k8s/current/k8s-deploy-eck.html
https://strimzi.io/blog/2020/05/07/camel-kafka-connectors/
https://strimzi.io/blog/2019/11/05/exposing-http-bridge/
