# Application Monitoring with Prometheus and Grafana

## Setting up Minecraft Spigot Server 
In order to practice using Grafana we need data. To create data for Prometheus to collect and for Grafana to display, we will use a Minecraft server. Minecraft is a popular game that has a client and a server. We will set up a Minecraft server through a special service named Spigot.  A Spigot Minecraft server will allow the use of a Prometheus exporter with minimal effort. You will not need to buy minecraft to start up the server and get data from it. 
We will be getting the data from the minecraft server by adding a prometheus Exporter plugin to Minecraft. The definition of an exporter is found below: 
1. Verify you have the correct tools needed to Build the Jar
 +	Have Java JRE 8  installed : 
 +	Have Git Installed :  
   +	Follow the instructions found at the link below if you do not have Git installed. https://www.atlassian.com/git/tutorials/install-git
2. Build the minecraft Server.jar 
Because of copyright restrictions, we need to compile the specific spigot Minecraft Server.jar ourselves. We will do it using a Buildtools.jar provided by Spigot.

 + Download the BuildTools.jar from : https://drive.google.com/file/d/1VMBOtsy1uJjTC0_7yJHjvBNPAOXUHCyj/view?usp=sharing 
 + Create a folder named ‘minecraft-server’
 + Place the BuildTools.jar in it 

## Run the BuildTools.jar according to the directions for your OS

Build tools automatically downloads, compiles, and creates the files that your minecraft server will need to run. 
When using the following commands, make sure you open the folder containing the Buildtools.jar file with the terminal or the  “Git Bash” tool

It will take between 5-10 minutes to build the server jar and create the files and folders needed for the server.

During this time many files and folders will be downloaded and created in the folder that contains the build.jar. 

When it is finished, your terminal and folder containing the build jar should look like the screenshot below:

### Windows
 + `java -Xmx1024M -jar BuildTools.jar`
###	Mac
 + `export MAVEN_OPTS="-Xmx2G"` 
 + `java -Xmx2G -jar BuildTools.jar`
###	Linux
 + `git config --global --unset core.autocrlf`
 + `java -jar BuildTools.jar`

![](https://github.com/jasonxris/Application-Monitoring-with-Prometheus-and-Grafana-Tutorial/blob/master/Student%20Files/Screenshots/MinecraftServerScreenshot.PNG )

  +	If the spigot-1.15.2.jar did not appear in the folder, check the BuildTools.log.txt
    + 	Chances are Java is not included in your path. You will need to add the Java Bin to your Environmental Variables path. 
  + If you need further instruction or help, refer to the official Spigot Buildtools guide found here : https://www.spigotmc.org/wiki/buildtools/
 
 ## Start Minecraft Server
To start the minecraft server, we need to run the `spigot-version-Name.jar`. I have provided some scripts that can be used to run the server. Each script just runs the jar and allocates the amount of RAM that the server needs to run. 

 +	When you install the spigot jar, it will have a name like spigot-1.15.1.jar 
    + 	Make sure this is the jar you are targeting in the .bat or .command file you are using to start your server 
    
###	Windows
+	Download the startup batch file found here : https://github.com/jasonxris/Application-Monitoring-with-Prometheus-and-Grafana-Tutorial/blob/master/Student%20Files/start.bat 
+	Drop the batch file into your “minecraft-server” folder
+	Double click the batch file.  
### Mac
+	Download the startup script found here : https://github.com/jasonxris/Application-Monitoring-with-Prometheus-and-Grafana-Tutorial/blob/master/Student%20Files/start.command
+	Drop the start.command file into your“minecraft server” folder
+	Open terminal, navigate to your ‘minecraft-server’ directory and set permissions with the following command:
1.	`chmod a+x  ./start.command`
2.	Double click your startup script (or execute it from the command line with ./start.command)

### Linux
+	Download the startup script found here : https://github.com/jasonxris/Application-Monitoring-with-Prometheus-and-Grafana-Tutorial/blob/master/Student%20Files/start.sh
+	place the start.sh file into your“minecraft-server” folder
+	Set permissions with : `chmod +x start.sh`
+	Run the startup script with ./start.sh


When you run the server for the first time it will stop and require you to open a eula.txt and change “eula=false” to “eula=true”

Start the server again to finish setting up the minecraft server

If the minecraft server is running correctly you should see the following in the terminal and see the dashboard shown in the screenshot below

![](https://github.com/jasonxris/Application-Monitoring-with-Prometheus-and-Grafana-Tutorial/blob/master/Student%20Files/Screenshots/MinecraftServerScreenshot2.PNG )
 
Stop the server by typing “stop” into the terminal
 
If you need further help starting the server, refer to the official Spigot guide here : https://www.spigotmc.org/wiki/spigot-installation/ 


##	Install Prometheus minecraft exporter onto your server.
By installing the exporter onto your server, you allow prometheus to use the data that the minecraft server creates. 

+	Download the Prometheus minecraft Exporter Version 2.0.0.jar here : https://dev.bukkit.org/projects/prometheus-exporter/files 
+	Navigate to the file containing your Minecraft Server 
+	Navigate to the folder named “plugins” 
+	Move the minecraft-prometheus-exporter.jar into the plugins folder, it should look like the screenshot below

![](https://github.com/jasonxris/Application-Monitoring-with-Prometheus-and-Grafana-Tutorial/blob/master/Student%20Files/Screenshots/PluginScreenshot.PNG )   

+	Run the server 
### Verification
After the server is started, if running correctly your terminal should look like the screenshot below: 

![](https://github.com/jasonxris/Application-Monitoring-with-Prometheus-and-Grafana-Tutorial/blob/master/Student%20Files/Screenshots/TerminalScreenshot.PNG)   

This minecraft server is now using the minecraft-exporter.jar to convert metrics/data the server has already created into a format that prometheus can understand. 
