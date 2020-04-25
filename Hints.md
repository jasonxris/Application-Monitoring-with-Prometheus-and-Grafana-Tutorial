# Hints
- Make sure your Prometheus.yml is configured to target your Intellj server and collect data from it
- Use [http://localhost:9090/targets](http://localhost:9090/targets) to make sure that your server&#39;sdata is being collected
- Use [http://localhost:8080/metrics](http://localhost:8080/metrics) to see what your defined metrics look like
- **If you change or add a Metric in your java program, make sure to update the DataSource on Grafana to get updated metrics.**
  - You do this by going to Configure -\&gt; Data Source -\&gt; Your\_Data\_Source -\&gt; Save &amp; Test. This is shown in screenshots below
- If Grafana doesn&#39;t seem to be displaying your data, refresh the data by making Grafana display the last 5 minutes of data.

### How to Change the Visualization of A Panel (in Dashboard Edit menu)

![](RackMultipart20200425-4-1dxjp97_html_f631a34e4ff056ef.png)

### How to Change Grafana Time Range

![](RackMultipart20200425-4-1dxjp97_html_95d180cd130298f4.png)
