# Prometheus Java Guide

**Prometheus Metric Information:**

Prometheus metrics are the way that Prometheus categorizes types of data. The three that we will be using are shown and explained below:

When you use .build() to create a Metric, you use the following to describe/build your metric

.namespace()

- This call sets the namespace/identifier for your metric. In the tutorial the minecraft namespace was &quot;mc&quot;. All minecraft related metrics started with mc.

.name()

- This call sets the specific name for this data. If you are counting the number of times the server runs through its algorithm. You would want to call it something like &quot;server\_algorithum\_counter&quot;. Separating out the words with underscores is the standard.

.help()

- This call sets the help description. Here, you can add more information on how to use this metric.

.register()

- This call makes the metric available to the server
- When the server is accessed on the port it is listening on, it sends information about every metric **that has been registered with it.**

![](RackMultipart20200425-4-7m115r_html_afe1f2d6f3d0cd53.png)

**To Initialize a counter in java**

Counter numberOfIterations = Counter.build()

.namespace(&quot;AnyIdentifierYouWant&quot;)

.name(&quot;Name\_You\_Want\_To\_Give\_To\_This\_Counter&quot;)

.help(&quot;Describe What this Metric Does&quot;)

.register();

**How to use a counter in java**

**When you want to increment the counter**

numberOfIterations.inc();

- **Note:** You are incrementing the counter object you created
- **Note:** You can&#39;t decrement a counter

![](RackMultipart20200425-4-7m115r_html_b02d19ee65819be4.png)

**To Initialize a Gauge in java**

Gauge numberOfNodes = Gauge.build()

.namespace(&quot;AnyIdentifierYouWant&quot;)

.name(&quot;Name\_You\_Want\_To\_Give\_To\_This\_Gauger&quot;)

.help(&quot;Describe What this Metric Does&quot;)

.register();

**How to use a Gauge in java**

**When you want to Increment the Gauge metric**

numberOfNodes.inc();

- **Note**** :** you are incrementing the counter gauge object you created

**When you want to decrement the Gauge metric**

numberOfNodes.dec();

- **Note**** :** you are decrementing the counter gauge object you created

![](RackMultipart20200425-4-7m115r_html_e45a0eb511412d33.png)

**To Initialize a Summary java**

Summary insertionTime = Summary.build()

.namespace(&quot;AnyIdentifierYouWant&quot;)

.name(&quot;Name\_You\_Want\_To\_Give\_To\_This\_Summary&quot;)

.help(&quot;Describe What this Metric Does&quot;)

.register();

**How to use Summary to measure the duration of a method**

**Define a summary timer object**

Summary.Timer timer;

**Start the Summary timer before the method you want to time**

timer = insertionTime.startTimer();

- **Note:** you are running the .startTimer() method on the Summary Object you created and initialized earlier

**Mark the end of the method to measure the duration of a method**

timer.observeDuration();

- **Note:** you are running the .observerDuration() method on the Summary Object you created and initialized earlier
- **Note:** This will measure the time it took to run between the .startTimer() and the .observeDuration() methods

# Further Documentation

[https://github.com/prometheus/client\_java](https://github.com/prometheus/client_java)

- This is the official Java client documentation
