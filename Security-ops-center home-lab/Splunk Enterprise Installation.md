# Splunk Enterprise Installation (Host Machine)

[← Back to project overview](README.md)

With the endpoint in place, the next step was standing up the SIEM that would receive and analyze its logs. Splunk Enterprise was downloaded and installed directly on the host machine rather than inside a VM, so that it could act as a stable, always-available collection point regardless of what was happening inside the lab's virtual machines. During installation, administrator credentials were created for the instance, and after setup completed, a login to the Splunk web interface was used to confirm the installation had succeeded and the platform was ready to receive data.

<p align="center">
  <img src="figure05_splunk_download.png" width="900" alt="Downloading Splunk Enterprise">
</p>

<p align="center"><em>Figure 5. Downloading Splunk Enterprise on the host machine.</em></p>

---

<p align="center">
  <img src="figure06_splunk_wizard.png" width="900" alt="Splunk setup wizard">
</p>

<p align="center"><em>Figure 6. Splunk Enterprise setup wizard.</em></p>

---

<p align="center">
  <img src="figure07_splunk_install.png" width="900" alt="Splunk installation in progress">
</p>

<p align="center"><em>Figure 7. Splunk Enterprise installation in progress.</em></p>

---

<p align="center">
  <img src="figure08_splunk_credentials.png" width="900" alt="Creating administrator credentials">
</p>

<p align="center"><em>Figure 8. Creating administrator credentials during setup.</em></p>

---

<p align="center">
  <img src="figure09_splunk_signin.png" width="900" alt="Splunk sign-in page">
</p>

<p align="center"><em>Figure 9. Splunk Enterprise sign-in page.</em></p>

---

<p align="center">
  <img src="figure10_splunk_homepage.png" width="900" alt="Splunk home page">
</p>

<p align="center"><em>Figure 10. Splunk Enterprise home page, confirming the installation completed successfully.</em></p>

---

Next: [Splunk Universal Forwarder Installation & Configuration →](Splunk%20Universal%20Forwarder%20Installation%20and%20Configuration.md)
