# Building a SOC + Honeynet in Azure (Live Traffic)
![Cloud Honeynet / SOC](https://i.imgur.com/ZWxe03e.jpg)

## Introduction

In this project, I build a mini honeynet in Azure and ingest log sources from various resources into a Log Analytics workspace, which is then used by Microsoft Sentinel to build attack maps, trigger alerts, and create incidents. I measured some security metrics in the insecure environment for 24 hours, apply some security controls to harden the environment, measure metrics for another 24 hours, then show the results below. The metrics we will show are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls
![Screenshot 2024-04-24 160741](https://github.com/seanmarqueling/Azure-SOC-Honeynet/assets/103546379/541be184-7078-44a6-9bf1-77f7ff7045a3)


## Architecture After Hardening / Security Controls
![image](https://github.com/seanmarqueling/Azure-SOC-Honeynet/assets/103546379/f67b4d34-32d1-48b5-a886-1c497b9e69ea)

The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were originally deployed, exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources are deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint

## Attack Maps Before Hardening / Security Controls
![Screenshot 2024-04-24 155217](https://github.com/seanmarqueling/Azure-SOC-Honeynet/assets/103546379/de0c6fc1-f473-4d78-afc6-49f09a182464)
![Screenshot 2024-04-08 203141](https://github.com/seanmarqueling/Azure-SOC-Honeynet/assets/103546379/0184c9b0-62f3-4068-987a-defc4bd6004f)
![Screenshot 2024-04-08 203301](https://github.com/seanmarqueling/Azure-SOC-Honeynet/assets/103546379/aebda4d3-a671-415f-95f2-63bf37829832)


## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2024-04-1 20:16:29
Stop Time 2024-04-2 20:16:29

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 21897
| Syslog                   | 1583
| SecurityAlert            | 0
| SecurityIncident         | 91
| AzureNetworkAnalytics_CL | 2768

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2024-04-10 16:45
Stop Time	2024-04-11 16:45

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 7
| Syslog                   | 0
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.
