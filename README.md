# <p style="text-align: center;">Setting up Grafana with Graphite and Node Exporter</p> 

## Linux Distribution: 

- Distributor ID:  Ubuntu
- Version: 23.04

## System Configuration:

- RAM : 4GB
- CPU :  4 CORE
- STORAGE : 1TB



## AGENDA:
Monitoring and visualization for system metrics

## Monitoring:
- In the world of computers and technology, monitoring means watching over computer systems, networks, or applications to ensure they are running smoothly and to catch any problems or errors early. Monitoring helps prevent issues and keeps everything running smoothly.


##  Grafana 
- Grafana is an open-source plateform for data visualisation and monitoring 

- Grafana is like a super tool for making data look pretty, keeping an eye on things, and helping us make decisions based on what we see.



##  Features of Grafana :
- Completely opensource
- Supports all majordatabases like InfluxDB,prometheus, graphite and etc.
- Explore metrics and logs 
- Alerting and visualisation.





##  Graphite 
- Graphite is a time-series database and graphing tool often used for monitoring and graphing metrics and performance data.



##  Carbon Exporter 
  Carbon Exporter is a software tool used to send metric data from various sources to a Graphite monitoring system, where it can be stored, visualized, and analyzed. It "exports" or forwards metrics to Graphite for centralized monitoring and graphing.


## Grafana Setup




## Step 1: Download podman Images:

First, download the podman images for Grafana , Graphite, and Graphite Exporter. You can do this using the command line:

```
  podman pull docker.io/grafana/grafana:latest

```


<img src="pull girfana.png" alt="your-image-description" style="border: 2px solid  black;">

```
podman pull docker.io/graphiteapp/graphite-statsd:latest

```



<img src="pull graphite.png" alt="your-image-description" style="border: 2px solid  black;">




```



 podman run -d --name graphite-exporter --pod dj docker.io/prom/graphite-exporter
```

<img src="graphite exporter.png" alt="your-image-description" style="border: 2px solid  black;">



## Step 2: Create a Docker Network:

- Create a Docker network to connect these containers:


```
podman network create grafana-net

```

<img src="create grafana.png" alt="your-image-description" style="border: 2px solid  black;">


## Step 5: Run the Grafana Container:
Now, run the Grafana container:
```
podman run -d \
  --name grafana \
  -p 3000:3000 \
  --network grafana-net \
  grafana/grafana:latest

```
<img src="3000.png" alt="your-image-description" style="border: 2px solid  black;">


## Step 3: Run the Graphite Container:
Now, run the Graphite container. This container is used to set up the Graphite database:



```
podman run -d \
  --name graphite \
  -p 8080:80 \
  -p 2003-2004:2003-2004 \
  --network grafana-net \
  graphiteapp/graphite-statsd:latest

```

<img src="8080.png" alt="your-image-description" style="border: 2px solid  black;">


## Step 4: Run the Graphite-Exporter
If you want to use Graphite-Exporter  to collect system metrics:

```

podman run -d --name graphite-exporter -p 9108:9108 docker.io/prom/graphite-exporter

```

<img src="graphite exporter.png" alt="your-image-description" style="border: 2px solid  black;">




## Step 6: Configure Grafana:

Open a web browser and go to http://localhost:3000. Configure Grafana with the default username/password (admin/admin), which you can change. Configure Grafana to use the Graphite data source with the URL http://graphite:8080.


## welcome to Grafana Homepage

<img src="Screenshot from 2023-09-14 17-40-45.png" alt="your-image-description" style="border: 2px solid  black;">

## Grafana Dashboard 

<img src="welcome grafana.png" alt="your-image-description" style="border: 2px solid  black;">

## Graphite Exporter 


<img src="metrix.png" alt="your-image-description" style="border: 2px solid  black;">





## Step 7: Click Menu Button

<img src="m.png " alt="your-image-description" style="border: 2px solid  black;">


## Step 8: Tap Connection
<img src="con.jpg" alt="your-image-description" style="border: 2px solid  black;">

- After that we will search the graphite form connect the grafana 

<img src="add new connection.png" alt="your-image-description" style="border: 2px solid  black;">



## 9. Search Graphite 

<img src="serach graphite.png" alt="your-image-description" style="border: 2px solid  black;">


## 10.Add New Data  Source

<img src="add connection.jpg" alt="your-image-description" style="border: 2px solid  black;">

## 11 Connect Graphite to Grafana With your IP Adress 

<img src="url  connection .png" alt="your-image-description" style="border: 2px solid  black;">


## 12 Connect Graphite to Grafana With your IP Adress 

<img src="save&test.png
" alt="your-image-description" style="border: 2px solid  black;">

## 13 Tap Dashboard

<img src="select carbon.png
" alt="your-image-description" style="border: 2px solid  black;">






