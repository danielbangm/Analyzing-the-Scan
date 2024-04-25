<p align="center">
<img src="https://www.simplilearn.com/ice9/free_resources_article_thumb/bfintropic.PNG" />
</p>

<h1>OpenVAS: Analyzing the Scan</h1>

The goal of vulnerability scanning is to identify and address weaknesses in systems, networks, or applications to prevent potential cyber attacks and enhance overall security. 

<h2>Objectives</h2>

-  Learning how to interpret a scan.
-  Getting more familiar with Risk mitigation.
-  Gain a better understanding of identifying weaknesses and preventing security breaches.

<h2>Environments and Technologies Used</h2>

- OpenVAS
- VMWare Workstation
- Greenbone Security Manager website

<h2>Operating Systems Used</h2>

- Linux

<h2>List of Prerequisites</h2>

- You need to download VMWare Workstation and have a computer of at least 8GB of RAM

<h2>Results of the Scan</h2>

Once the Scan is complete, the Tasks Dashboard (Scans > Tasks) Should look similar to the image below. Notice that the Scan result status shows <b>“Done”</b>.

![image](https://github.com/danielbangm/Analyzing-the-Scan/assets/22795502/b02976e9-54b7-49e1-866b-cdc249bd555f)

Click on Scans > Results .Notice and confirm the IP Address of the Scan. (192.168.106.157 as an example)

![image](https://github.com/danielbangm/Analyzing-the-Scan/assets/22795502/e71543c6-34ae-452d-93d1-53ce69902b03)

<h2>Analyzing the Scan: Password Issues</h2>

As we can see on the image below from my scan results, there are 25 high vulnerabilies and 34 medium vulnerabilities. 

![image](https://github.com/danielbangm/Analyzing-the-Scan/assets/22795502/31fc8bac-0ad8-432b-923a-1f4ea38ac808)

One of them is a well known vulnerbility. <b>The rlogin Passwordless Lo</b> service which allows root access without a password. This vulnerability allows an attacker to gain complete control over the target system. The mitigation is to Disable the rlogin service and use alternatives like SSH instead.
![image](https://github.com/danielbangm/Analyzing-the-Scan/assets/22795502/fcf5c5bc-1851-46be-b244-546bf7c3db78)

The scan reveals another password issue "PostgreSQL weak password". It was possible to login as user postgres with password "postgres". The mitigation solution here is to Change the password as soon as possible.
![image](https://github.com/danielbangm/Analyzing-the-Scan/assets/22795502/f077abd0-ad21-41f2-be02-8f5451ce676f)

<h2>Analyzing the Scan: Backdoors Detected</h2>

The program is the <b>“Ingrelock”</b> which is a backdoor installed on the remote host. The service is answering to an 'id;' command with the following response: uid=0(root) gid=0(root). Attackers can exploit this issue to execute arbitrary commands in the context of the application. Successful attacks will compromise the affected system. The mitigation is to Workaround A whole cleanup of the infected system.

![image](https://github.com/danielbangm/Analyzing-the-Scan/assets/22795502/29a1def8-a3de-4041-b698-ae30f376a1a1)

<h2>Analyzing the Scan: Brute Force</h2>

The scan reveals a Brute Force attempt. The program is the “FTP Brute Force Logins reporting. It was possible to login into the remote FTP server using weak/known credentials. As the VT 'FTP Brute Force Logins' (OID: 1.3.6.1.4.1.25623.1.0.108717) might run into a timeout the actual reporting of this vulnerability takes place in this VT instead. It was possible to login with the following credentials <User>:<Password>; msfadmin:msfadmin; postgres:postgres; service:service; user:user.  The mitigation is to Change the password as soon as possible.

![image](https://github.com/danielbangm/Analyzing-the-Scan/assets/22795502/1fca3541-d2b4-4d94-ae95-ab48707cf9be)

<h2>Analyzing the Scan: Unencrypted Logins</h2>

The program is “rsh Unencrypted ClearText Login”  This remote host is running a rsh service. The rsh service is misconfigured so it is allowing conntections without a password or with default root:root credentials. rsh (remote shell) is a command line computer program which can execute shell commands as another user, and on another computer across a computer network. The mitigation is to disable the rsh service and use alternatives like SSH instead.

![image](https://github.com/danielbangm/Analyzing-the-Scan/assets/22795502/c130348b-bfa5-4e36-8440-13f7f4e3a698)
