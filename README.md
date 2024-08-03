# Sentinel-Threat-Map

## Description 
This project's goal was to collect logs of failed RDP logon attempts on an exposed virtual machine to graphicly present the data on a map. 
</br>
</br>
![image](https://github.com/JimmyDuong00/Azure-Sentinel-Threat-Map/assets/95601798/6d57e145-b613-4888-9477-c2f5f7bdfd79)

The project uses Windows 10 security event logs which are then collected and sent to an API IP geolocation service which will give us the latitude and longitude of where the attempts are being made. 
</b>
The data is saved on to a .log in the virtual machine which is exported to Azure Log Analytics Workspace. We are able to visualize the data using Azure Sentinel Workbooks to plot the locations on a map. 

The project is inspired by Josh Makador's Azure Sentinel's Youtube Video: https://www.youtube.com/watch?v=RoZeVbbZ0o0 </br>
All credits go to Josh and his powershell script that allowed me to transform the data. 

## Getting started
In order to begin this project, you would need an Azure account. I created a free account that gave me $200 worth of credits which is plenty for the amount of time and resources I am planning to use.
</br>
Create a Windows2010 virtual machine with 2gib of RAM. I ran into an issue where the lower tiers were too slow to navigate the settings:

After the machine is running, note the public IP address as we will need this for later. 

## Disable Windows Firewall
We will need to disable Windows Firewall to allow external traffic to communicate with our machine. 
In the Windows start, enter 'wf.msc' to locate the firewall settings and disable the public facing firewall:

After the firewall has been disabled, we can now test to see if external traffic is able to ping the machine.
</br>
On your computer, open CMD and type 'ping [enter ip address of machine here] -t' </br> 
This will allow us to see if packets are able to reach the honeypot VM and are able to make it through the firewall. 
</br>
Once you can confirm that the firewall is disabled, we can now begin on the log collection. 

## Configure and run the PowerShell script
Copy the powershell script inside this repository Custom_Security_Log_Exporter.ps1 (Courtesy of Josh Madakor) and open Powershel ISE. Create a new file (In the top left corner click on File>New) and paste the code here. 
Notice line 2 where the '$APIKey' is at. 

### Create a https://ipgeolocation.io/ account
Creat a free account and copy the API key the website generates. 
</br>
Paste the website's API key into line 2 of the PowerShell script and save the file to Desktop.

## Creating a Workspace in Log Analytics Workspace 
We need to enable data connectors on the target VM in order to export the logs. 

## Querying the data 
In order to clean up the fields where our precious latitiude and longitude data is, we need to have a query that can parse out the Jumbled 

## Displaying IP locations in Azure Sentinel
The final step would be taking the parsed data and display it using Sentinel.
Navigate to Azure Sentinel and create a workbook. Here, you will 
Note: Azure Sentinel only displays 10,000 results and all other data after will be truncated </br>
See here: https://learn.microsoft.com/en-us/azure/azure-monitor/visualize/workbooks-limits
