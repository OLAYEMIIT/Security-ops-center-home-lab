# Sysmon Installation & Configuration

[← Back to project overview](README.md)

## Installing Sysmon

With the transport layer between the VM and Splunk confirmed working, attention turned to the actual source of meaningful security telemetry: Sysmon. Sysmon (version 15.2) was installed on the Windows VM. Rather than running it with default settings, the SwiftOnSecurity configuration file was applied — a widely used, community-maintained Sysmon configuration that is tuned to capture high-value security events (process creation, file creation, network connections, and more) while filtering out noisy, low-value events. This is the same approach used in many real SOC environments, since raw default Sysmon output can be overwhelming and includes a large amount of noise.

<p align="center">
  <img src="figure18_sysmon_download.png" width="900" alt="Downloading Sysmon">
</p>

<p align="center"><em>Figure 18. Downloading Sysmon from Microsoft Sysinternals.</em></p>

---

<p align="center">
  <img src="figure19_sysmon_config.png" width="900" alt="SwiftOnSecurity Sysmon configuration">
</p>

<p align="center"><em>Figure 19. SwiftOnSecurity Sysmon configuration file retrieved from GitHub.</em></p>

---

## Adding Sysmon as a log source

Installing Sysmon makes it generate events locally in Windows Event Viewer, but by default the Splunk Universal Forwarder does not know to collect that specific event log — it has to be told explicitly. The Forwarder's `inputs.conf` file was edited to add a new input stanza pointing at the Sysmon Operational event log, alongside the existing stanzas for Security, Application, and System logs. After saving the change, the Forwarder was restarted so the new configuration would take effect.

<p align="center">
  <img src="figure20_inputs_conf.png" width="900" alt="inputs.conf updated with Sysmon log input">
</p>

<p align="center"><em>Figure 20. inputs.conf updated with the Sysmon Operational log input.</em></p>

---

<p align="center">
  <img src="figure21_forwarder_restart.png" width="900" alt="Universal Forwarder restarted">
</p>

<p align="center"><em>Figure 21. Universal Forwarder restarted to apply the new Sysmon input.</em></p>

---

## Verifying Sysmon locally

Before worrying about whether Sysmon data was reaching Splunk, it was important to confirm Sysmon was actually generating events at all. A test file was created on the Windows VM specifically to trigger a FileCreate event, and Windows Event Viewer was checked to confirm Sysmon Event ID 11 (FileCreate) appeared as expected. A general search was also run in Splunk Enterprise for events associated with the VM's hostname, to get an early read on what data was already flowing in.

<p align="center">
  <img src="figure22_event_viewer.png" width="900" alt="Sysmon Event Viewer verification">
</p>

<p align="center"><em>Figure 22. Sysmon Event ID 11 (FileCreate) confirmed in Windows Event Viewer.</em></p>

---

<p align="center">
  <img src="figure23_splunk_host_search.png" width="900" alt="Splunk search by host">
</p>

<p align="center"><em>Figure 23. Splunk Enterprise search showing events from the Windows VM host.</em></p>

---

Next: [Troubleshooting: Sysmon Forwarding Issue →](Troubleshooting%20-%20Sysmon%20Forwarding%20Issue.md)
