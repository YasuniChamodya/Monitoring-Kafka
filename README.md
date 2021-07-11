# Monitoring-Kafka

Set up Kafka monitoring on a Grafana dashboard using Prometheus. Use Prometheus to pull metrics from Kafka and then visualize the important metrics on a Grafana dashboard (You can refer [this blog post](https://www.blogger.com) or [this YouTube video](https://www.youtube.com) for complete tutorial).
<div>
<h6 align="center">Overall Process</h6>
<p align="center">
  <img src="https://user-images.githubusercontent.com/48217165/125206288-264c9880-e2a4-11eb-87f0-406a85ad559e.PNG" />
</p><br/>
</div>

<h4>1. Setting up the Docker file, configuring Prometheus.yml and running the instances</h4>
<p>I assume you have installed Docker desktop on your PC. If not, you should download and install Docker desktop before you begin</p>
<p>First, create a folder with any name you want (In my case folder name is VAUED)</p>
<p>You shoud keep following files inside the folder you created</p>
<ul>
<li>prom-jmx-agent-config.yml</li>
<li>Dockerfile</li>
<li>docker-compose.yml </li>
<li>prometheus.yml</li>
</ul>
<p>Open the command prompt inside the folder you created or navigate to the directory you have created your files.You are required to run the following line in order to create all the images to start Grafana visualization</p>
<code>docker-compose up -d</code>
<p></p>
<img src="https://user-images.githubusercontent.com/48217165/125193716-87a44580-e26b-11eb-86d5-88c2bc887662.PNG" />

<p>Now you can look into Docker desktop and you will be able to see all the images are created and running as follows.</p>
<img src="https://user-images.githubusercontent.com/48217165/125195907-6d6f6500-e275-11eb-95d2-664343eb1ea1.png" width="800"/>

<h4>2. Monitoring visualization on Grafana</h4>
<p>Now we have configured Kafka JMX metrics to pipe into Prometheus, it's time to visualize it in Grafana. Open your favorite web browser and browse to http://localhost:3000 . You will be able to log in using the username and password as admin (If you need you can change them after your 1st login).
Now you need to add Prometheus as a data source. 
</p>

<p>Now you can create your own dashboard on Grafana by manually configuring the panels one by one or you can download my dashboard JSON file and import it into Grafana.</p>
<img src="https://user-images.githubusercontent.com/48217165/125198034-da86f880-e27d-11eb-8575-c8431f26caae.png" width="700" height="400"/>

<p>Make sure to choose the correct data source, which is “Prometheus” in our case, and click on the Import button. You should immediately see the dashboard reporting the following metrics.</p>
<img src="https://user-images.githubusercontent.com/48217165/125195604-feddd780-e273-11eb-988f-ba4dd32f34d4.PNG" width="800"/>

<h4>Gauges</h4>
•	CPU Usage - total user and system CPU time spent in seconds / rate of the CPU counter changes in five minutes of range.<br/>
•	JVM Memory Used - Sum of memory usage of JVM memory area.

<h4>Counters</h4>
•	Partition count - total number of global partitions across all topics in the Kafka cluster (excluding replicas).<br/>
•	Offline partitions- number of partitions that are offline in the cluster. This number should always be zero. If a partition is offline / down, means that the topics are also down).<br/>
•	URP - number of under-replicated partitions for the broker. Should always be zero. Otherwise, partitions are lagging behind the rest of the clusters.<br/>
•	Active controller count - one of the brokers is an active controller and all the ones are not controllers. This number should always be one. Zero means the Kafka cluster is not working/ there are no active controllers.<br/>
•	Topic count - total number of topics across all brokers in the cluster.<br/>
•	Total message count - Total number of producer requests to a broker.<br/>
•	Total consumer requests - The total number of fetch requests.<br/>
•	Total producer request - The total number of fetch requests.<br/>

<h4>Histograms</h4>
•	Prometheus scrape duration - how long Prometheus scrape took.<br/>
•	JMX exporter scrape duration - how long JMX exporter took for scraping.

<h4>Graphs</h4>
•	Message in per topic.<br/>
•	Bytes in per topic.<br/>
•	Bytes out per topic.<br/>
•	Time spent in GC (Garbage Collection).<br/>
<br/>

Refer [this blog post](https://www.blogger.com) or [this YouTube video](https://www.youtube.com) for creating topics, producing and consuming messages.
