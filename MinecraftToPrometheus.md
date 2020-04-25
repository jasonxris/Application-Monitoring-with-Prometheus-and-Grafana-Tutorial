# Connecting Minecraft Server to Prometheus and Grafana

## Connecting a Minecraft Server to Prometheus
_In the Preparation, you installed an exporter onto the Minecraft server by placing the minecraft-prometheus-exporter-2.0.0.jar into the minecraft-server&#39;s plugins folder. This exporter takes the metrics Minecraft is already creating and formats it in a way that Prometheus can understand. The exporter then exposes the data to a predetermined port. For this exporter, the data is exposed on port 9225._

1. Make sure that you have set up your Minecraft server according to the Preparation steps.
2. Open your Minecraft server folder
3. Run the Minecraft server using the given start script
4. Verify that the exporter was successfully installed.
      + If it was installed successfully, your terminal should look like the screenshot below
![](https://github.com/jasonxris/Application-Monitoring-with-Prometheus-and-Grafana-Tutorial/blob/master/Student%20Files/Screenshots/Tutorial%20Screenshots/Tutorial-SCreenshot1.PNG)

5. Navigate to the directory that contains the prometheus configuration file also known as the prometheus.yml file
      + For Mac users: Navigate to the directory where you placed the downloaded prometheus.yml during the pre-class assignment
![](https://github.com/jasonxris/Application-Monitoring-with-Prometheus-and-Grafana-Tutorial/blob/master/Student%20Files/Screenshots/Tutorial%20Screenshots/TutorialScreenshot2.PNG)

6. Open the prometheus.yml file
      + For Mac users: Open the prometheus.yml you set to be the prometheus config.file in step 1.V of the pre-class assignment

_The Prometheus.yml file contains all the configuration for Prometheus. By configuring the Prometheus.yml file, you can tell Prometheus when, how, and where to scrape for data. We are going to configure it to scrape for data from our Minecraft server._

7. Scroll to the bottom of the file to scrape\_config:
8. Add a new job name, and target for the Minecraft server
      + Since the exporter is exposing the data on port 9225, we need to tell Prometheus to look for data on localhost:9225
      + Copy and paste the scrape\_config text below over the old scrape config in your prometheus.yml
      + The scrape\_configs section of your prometheus.yml file should look like the screenshot below the scrap config text. **Save and exit the file**.

```
  # The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
  - job_name: 'prometheus'
    static_configs:
    - targets: ['localhost:9090']

  - job_name: 'minecraft'
    static_configs:
    - targets: ['localhost:9225']
```


![](https://github.com/jasonxris/Application-Monitoring-with-Prometheus-and-Grafana-Tutorial/blob/master/Student%20Files/Screenshots/Tutorial%20Screenshots/TScreenshot3.PNG)

9. If Prometheus was already running, stop it.
  1. You can do this by exiting out of the prometheus terminal that is shown below 
  ![](https://github.com/jasonxris/Application-Monitoring-with-Prometheus-and-Grafana-Tutorial/blob/master/Student%20Files/Screenshots/Tutorial%20Screenshots/TScreenshot4.PNG)

10. Run Prometheus
+ use the following command to run prometheus
      + Mac: `prometheus --config.file=\&lt;directory for your config file\&gt;/prometheus.yml`
      + Windows: Run the prometheus.exe file

**ADD GIF HERE**

11. Verify that the Minecraft server data will be collected by navigating to: [http://localhost:9090/targets](http://localhost:9090/targets). It should look like the screenshot below.

![](https://github.com/jasonxris/Application-Monitoring-with-Prometheus-and-Grafana-Tutorial/blob/master/Student%20Files/Screenshots/Tutorial%20Screenshots/TScreenshot5.PNG)

## Connecting a Minecraft Server to Grafana

_In order for Grafana to use data from Prometheus, Grafana needs to know where the Prometheus server is running. We will now create a data source in Grafana and connect it to our Prometheus server._

1. Make sure Grafana is running
      + Mac: brew services start grafana
      + Windows: execute the grafana-server.exe located in the grafana directory under the bin folder
2. Make sure your minecraft server is running.
      + Navigate to your minecraft server folder
      + Start the minecraft server by executing the start.bat, start.command, or start.sh file that you downloaded in the pre-class assignment
3. Verify that prometheus is scraping data from minecraft by navigating to [http://localhost:9090/targets](http://localhost:9090/targets). Your screen should look like the screenshot below

![](https://github.com/jasonxris/Application-Monitoring-with-Prometheus-and-Grafana-Tutorial/blob/master/Student%20Files/Screenshots/Tutorial%20Screenshots/TScreenshot6.PNG)

4. Open up Grafana at [http://localhost:3000](http://localhost:3000/)_(this is the default port number)_
5. Click Add a data source

![](https://github.com/jasonxris/Application-Monitoring-with-Prometheus-and-Grafana-Tutorial/blob/master/Student%20Files/Screenshots/Tutorial%20Screenshots/TScreenshot7.PNG)

6. Select the Prometheus time series database
7. Enter in your Prometheus URL. The default URL is : [http://localhost:9090](http://localhost:9090/)
      + This is **NOT** the URL where you are exposing your Minecraft data.

![](https://github.com/jasonxris/Application-Monitoring-with-Prometheus-and-Grafana-Tutorial/blob/master/Student%20Files/Screenshots/Tutorial%20Screenshots/TScreenshot8.PNG)

8. Save and Test
      + If you see what is shown in the screenshot below, you are good to continue.

![](https://github.com/jasonxris/Application-Monitoring-with-Prometheus-and-Grafana-Tutorial/blob/master/Student%20Files/Screenshots/Tutorial%20Screenshots/TScreenshot9.PNG)
