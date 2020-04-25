# Application Monitoring with Prometheus and Grafana

## What to learn
-	What does Prometheus do?
-	What does Grafana do? 
-	What is instrumentation? 
-	What is an exporter?
-	What are metrics?
-	What are the metrics used by Prometheus?
-	What are Prometheus expressions? 
-	What does a Grafana dashboard do?

## Read about Prometheus
5  min - https://www.techopedia.com/definition/29133/application-monitoring

10 min - https://prometheus.io/docs/introduction/overview/

## Setting up Prometheus 
To install Prometheus, follow the instructions found at this link: https://prometheus.io/docs/prometheus/latest/getting_started/ 

  +	Windows users: extract the files and run the Prometheus.exe file 
  +	Mac users: follow these steps to install using homebrew:
    + 	Homebrew is a package manager for Mac OS that makes it easy to install software on a Mac. Start by confirming that you have Homebrew installed,
by typing the following in a terminal: `brew -v`
    + 	If you see a Homebrew version, you have Homebrew installed and can proceed to the next step. If not, paste the following command 
into your terminal, hit Enter, and wait for Homebrew to install:
```/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"'```
    + Make sure your Homebrew installation is up-to-date by typing `brew update`
    + Type `brew install prometheus` and wait for Prometheus to install
    + Download this prometheus.yml configuration file to tell Prometheus how to run. Copy it to a directory of your choice and run the following from the command line:
`prometheus --config.file=<directory for your config file>/prometheus.yml`



2.	After starting Prometheus, navigate to localhost:9090. If running properly, your screen should look like the screenshot below

![](https://github.com/jasonxris/Application-Monitoring-with-Prometheus-and-Grafana-Tutorial/blob/master/Student%20Files/Screenshots/ScreenShot1.png )

## Next Steps
[Complete the Grafana preparation](https://github.com/jasonxris/Application-Monitoring-with-Prometheus-and-Grafana-Tutorial/blob/master/GrafanaBackground.md)
