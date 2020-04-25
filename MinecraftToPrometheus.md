# Connecting Minecraft Server to Prometheus and Grafana

## Connecting a Minecraft Server to Prometheus
_In the Pre-class assignment, you installed an exporter onto the Minecraft server by placing the minecraft-prometheus-exporter-2.0.0.jar into the minecraft-server&#39;s plugins folder. This exporter takes the metrics Minecraft is already creating and formats it in a way that Prometheus can understand. The exporter then exposes the data to a predetermined port. For this exporter, the data is exposed on port 9225._

1. Make sure that you have set up your Minecraft server according to the pre-class assignment.
2. Open your Minecraft server folder
3. **Run the Minecraft server** using the given start script
4. Verify that the exporter was successfully installed.
      + If it was installed successfully, your terminal should look like the screenshot below

![](https://github.com/jasonxris/Application-Monitoring-with-Prometheus-and-Grafana-Tutorial/blob/master/Student%20Files/Screenshots/Tutorial%20Screenshots/Tutorial-SCreenshot1.PNG)

1. **Navigate to the directory that contains the prometheus configuration file also known as the prometheus.yml file**
  1. **For Mac users:** Navigate to the directory where you placed the downloaded prometheus.yml during the pre-class assignment

![](https://github.com/jasonxris/Application-Monitoring-with-Prometheus-and-Grafana-Tutorial/blob/master/Student%20Files/Screenshots/Tutorial%20Screenshots/TutorialScreenshot2.PNG)

1. **Open the prometheus.yml** file
  1. **For Mac users:** Open the prometheus.yml you **set to be the prometheus config.file in step 1.V** of the pre-class assignment

_The Prometheus.yml file contains all the configuration for Prometheus. By configuring the Prometheus.yml file, you can tell Prometheus when, how, and where to scrape for data. We are going to configure it to scrape for data from our Minecraft server._

1. Scroll to the bottom of the file **to scrape\_config:**
2. **Add a new job name, and target** for the Minecraft server
  1. Since the exporter is exposing the data on port 9225, we need to tell Prometheus to look for data on localhost:9225
  2. Copy and paste the scrape\_config text below **over the old scrape config** in your prometheus.yml

_scrape\_configs:_

_# The job name is added as a label `job=\&lt;job_name\&gt;` to any timeseries scraped from this config._

_- job\_name: &#39;prometheus&#39;_

_static\_configs:_

_- targets: [&#39;localhost:9090&#39;]_

_- job\_name: &#39;minecraft&#39;_

_static\_configs:_

_- targets: [&#39;localhost:9225&#39;]_

  1. The scrape\_configs section of your prometheus.yml file should look like the screenshot below. **Save and exit the file**.

![](https://github.com/jasonxris/Application-Monitoring-with-Prometheus-and-Grafana-Tutorial/blob/master/Student%20Files/Screenshots/Tutorial%20Screenshots/TScreenshot3.PNG)

1. **If Prometheus was already running, stop it.**
  1. You can do this by exiting out of the prometheus terminal that is shown below ![](https://github.com/jasonxris/Application-Monitoring-with-Prometheus-and-Grafana-Tutorial/blob/master/Student%20Files/Screenshots/Tutorial%20Screenshots/TScreenshot4.PNG)

1. **Run Prometheus**
  1. use the following command to run prometheus
    1. Mac: **prometheus --config.file=\&lt;directory for your config file\&gt;/prometheus.yml**
    2. Windows: Run the prometheus.exe file

**ADD GIF HERE**

1. Verify that the Minecraft server data **will be** collected by navigating to: [http://localhost:9090/targets](http://localhost:9090/targets). It should look like the screenshot below.

![](https://github.com/jasonxris/Application-Monitoring-with-Prometheus-and-Grafana-Tutorial/blob/master/Student%20Files/Screenshots/Tutorial%20Screenshots/TScreenshot5.PNG)

## Connecting a Minecraft Server to Grafana

_In order for Grafana to use data from Prometheus, Grafana needs to know where the Prometheus server is running. We will now create a data source in Grafana and connect it to our Prometheus server._

1. **Make sure Grafana is running**
  1. **Mac:** brew services start grafana
  2. **Windows:** execute the grafana-server.exe located in the grafana directory under the bin folder
2. **Make sure your minecraft server is running.**
  1. **Navigate to your minecraft server folder**
  2. Start the minecraft server by **executing the start.bat, start.command, or start.sh file** that you downloaded in the pre-class assignment
3. Verify that prometheus is scraping data from minecraft by navigating to [http://localhost:9090/targets](http://localhost:9090/targets). Your screen should look like the screenshot below

![](https://github.com/jasonxris/Application-Monitoring-with-Prometheus-and-Grafana-Tutorial/blob/master/Student%20Files/Screenshots/Tutorial%20Screenshots/TScreenshot6.PNG)

1. **Open up Grafana** at [http://localhost:3000](http://localhost:3000/)_(this is the default port number)_
2. **Click -\&gt; Add a data source**

![](https://github.com/jasonxris/Application-Monitoring-with-Prometheus-and-Grafana-Tutorial/blob/master/Student%20Files/Screenshots/Tutorial%20Screenshots/TScreenshot7.PNG)

1. Select the Prometheus time series database
2. **Enter in your Prometheus URL**. The default URL is : [http://localhost:9090](http://localhost:9090/)
  1. This is **NOT** the URL where you are exposing your Minecraft data.

![](https://github.com/jasonxris/Application-Monitoring-with-Prometheus-and-Grafana-Tutorial/blob/master/Student%20Files/Screenshots/Tutorial%20Screenshots/TScreenshot8.PNG)

1. Save and Test
  1. If you see what is shown in the screenshot below, you are good to continue.

![](https://github.com/jasonxris/Application-Monitoring-with-Prometheus-and-Grafana-Tutorial/blob/master/Student%20Files/Screenshots/Tutorial%20Screenshots/TScreenshot9.PNG)
