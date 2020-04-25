# Prometheus Lab

## Instructions

You are to instrument the given server to display the data given below. Then take a screenshot of the Grafana dashboard displaying the information scraped from the running server.

1. **Instrument the Main.java file**

_Instrumenting Java code is done by creating a metric object and then using this metric object to increment, decrement, keep track of a timer, or keep track of anything else the metric is capable of doing. By creating and registering the metric object, the data it collects becomes viewable by the Prometheus Server when your server is running._

- The specific metrics and java code you will need to instrument the server is described in the Prometheus Java Guide in the link below: [https://docs.google.com/document/d/1lTysUo1-1vW8Epqyx6LKSEl9vd9Ns4dSd5dC\_guTdUs/edit?usp=sharing](https://docs.google.com/document/d/1lTysUo1-1vW8Epqyx6LKSEl9vd9Ns4dSd5dC_guTdUs/edit?usp=sharing)

- The example metric is there to show you how a counter is initialized and how it is used to keep track of the number of times the server runs through its thread. It can be ignored or deleted.

The data you will need to collect for this Lab is shown below:

1. Count the number of failed removes **(use Counter Metric)**

    - Increment a counter when the server fails to remove a number for any reason

1. Count the number of failed adds **(use Counter metric)**

    - Increment a counter when the server fails to add a number for any reason

1. Keep track of the number of nodes currently on the Server **(use Gauge metric)**

    - Describes the number of BST nodes currently on the server

1. Measure the amount of time it takes for the BST add method to run **(use Summary Metric)**

    - You will have to use a timer to measure how long it takes for the add method to run.

To verify your instrumentation, navigate to [http://localhost:8080/metrics](http://localhost:8080/metrics)

    - This page will display the raw data being collected by Prometheus from port 8080.
    - **Note:** Data will only be collected while your server is running

**2. Display the data you gather in your Main.java file on a Grafana Dashboard**

Once the data is being collected, you will create your own Grafana Dashboard with panels to display the data you collect.

**Create a new Grafana Dashboard**

1. On the left menu of Grafana, **Click the plus symbol,** then **Click &quot;Dashboard&quot;** from the menu displayed by the Plus Symbol
  1. This will create a new empty Dashboard. We will be adding 4 panels to this dashboard.

**Create**** Four Grafana Panels** that displays the following information about the server:

1. The total number of failed removes **(use Counter Metric)**

1. The total number of failed adds **(use Counter metric)**

1. The number of nodes currently on the Server **(use Gauge metric)**

    - Use a Gauge Grafana visual to display this data

- Follow the picture guide at the bottom of this document if you don&#39;t know how to use a Gauge Visual

1. The average duration of the BST add method**(use Summary Metric)**

    - In your Main.java instrumentation, you kept track of the time it took to iterate through the add function. Using prometheus query expressions, we can use the data collected to get the average duration.
    - **The section below explains how to use a Prometheus query expression to calculate the values for this panel**

At the end your Grafana Panels should look similar to the screenshot below

![](RackMultipart20200425-4-1dxjp97_html_1b4216e6aaa1a510.png)

To expose the data gathered by your metrics to Prometheus, **run the main method** found in the Main.java file. Your server will then expose data gathered by the metric objects you created. Prometheus will then be able to collect this data from localhost:8080.

**3. Take a screenshot of the Grafana Dashboard you created**

## How to get Average Rate from a Prometheus Query

1. To display the Average duration of the add function you will use the Prometheus Query Function: Rate.

![](RackMultipart20200425-4-1dxjp97_html_1ad334bb5dbb8881.png)

1. A summary metric has a few different parts that can be pulled out.
  1. Adding &quot;\_sum&quot; to the end of your summary metric query gets the sum of the observations
  2. Adding &quot;\_count&quot; to the end of your summary metric query gets the number of observations
2. In Grafana, this is done by placing the metric within the rate function in the Query field of the dashboard. ![](RackMultipart20200425-4-1dxjp97_html_37006e0d46abebcc.png)
