# Prepare Lab
## Introduction

While there are many exporters that automatically collect data from certain programs, exporters will not always collect the data you want or be available at all. **Instrumenting is how you can manually expose data** you want to Prometheus.

The program that you will instrument today is a very simple server. It runs a binary search tree that randomly adds and deletes a value every second. Even though you probably will not encounter a server like this one in the workforce, it will provide a simplified environment to practice exposing data to Prometheus.

## The Lab

**Create a new Maven IntelliJ project**. Then download the source files found at the link below and place the .java files in the src folder of your IntelliJ project.

**Source Files:** [https://drive.google.com/file/d/1CiKD3vPLbD-PKH4XS3M1EufPXwH7tOkp/view?usp=sharing](https://drive.google.com/file/d/1CiKD3vPLbD-PKH4XS3M1EufPXwH7tOkp/view?usp=sharing)

**Main.java**

- The main method:
  - Runs the algorithm in a background thread
  - Creates an HTPPServer which is a Prometheus exporter
  - Runs the server on a port

- The Main.java has a single counter metric defined as an example to follow.
- Make sure to read comments in the Main.java file to understand how the different functions work.

**Dependencies**

- **Add the dependencies and maven compiler plugin** that are found in the link below to your pom file:

[https://docs.google.com/document/d/1UsHdoW6hyX2yJexgFwRV4Z5g4p9n44L4kSXseFQRCDE/edit?usp=sharing](https://docs.google.com/document/d/1UsHdoW6hyX2yJexgFwRV4Z5g4p9n44L4kSXseFQRCDE/edit?usp=sharing)

- The maven compiler plugin sets the java language level to 8
- The dependencies allow you to expose data in a format that Prometheus can read

**BST, BSTNode, and FailedRemoveException**

- These are the classes of the Binary Search Tree that the main method will be using.
- **DO NOT MODIFY**
- You do not need to touch these files to instrument your code.

**Configure Prometheus:**

1. **Stop Prometheus**
2. **Update your prometheus.yml** to make Prometheus scrapes data from your server .

  1. Copy and paste the scrape\_config text below **over the old scrape config** in your prometheus.yml

_scrape\_configs:_

_# The job name is added as a label `job=\&lt;job_name\&gt;` to any timeseries scraped from this config._

_- job\_name: &#39;prometheus&#39;_

_static\_configs:_

_- targets: [&#39;localhost:9090&#39;]_

_- job\_name: &#39;minecraft&#39;_

_static\_configs:_

_- targets: [&#39;localhost:9225&#39;]_

_- job\_name: &#39;javaSever&#39;_

_static\_configs:_

_- targets: [&#39;localhost:8080&#39;]_

1. **Start Prometheus** again
  1. use the following command to run prometheus
    1. Mac: **prometheus --config.file=\&lt;directory for your config file\&gt;/prometheus.yml**
    2. Windows: Run the prometheus.exe file
