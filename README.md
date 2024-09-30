# Day-12-Setting-Up-an-SSH-Server-and-Analyzing-Authentication-Logs


In today’s digital landscape, understanding server security is crucial. This guide walks you through setting up an SSH server on Vultr and analyzing its authentication logs. By the end, you’ll have hands-on experience with server deployment and basic security monitoring.

![Alt text](https://raw.githubusercontent.com/Virus192/Day-12-Setting-Up-an-SSH-Server-and-Analyzing-Authentication-Logs/refs/heads/main/Images/photo_5987967405093143043_w.jpg)
## Deploying Your SSH Server on Vultr

1. Log in to your Vultr account.
2. Click “Deploy” in the top-right corner to create a new server.
3. Choose the following specifications:
   - **Type**: Cloud Compute — Shared CPU
   - **Location**: Select your preferred region
   - **Image**: Ubuntu 24.04 LTS x64
   - **Plan**: Regular Cloud Compute
     - 25GB SSD
     - 1 vCPU
     - 1GB Memory
4. Name your server and click **“Deploy Server.”**

## Accessing and Updating Your Server

1. Wait for the deployment to complete.
2. Use PowerShell to SSH into your server using the credentials provided by Vultr.
3. Once connected, update and upgrade the system:

    ```bash
    apt-get update && apt-get upgrade
    ```

## Exploring Authentication Logs

1. Navigate to the log directory:

    ```bash
    cd /var/log
    ```

2. List the contents and locate `auth.log`:

    ```bash
    ls
    ```

3. View the contents of `auth.log`:

    ```bash
    cat auth.log
    ```

    > **Note**: If you’ve just created the server, it may take some time before meaningful logs appear.

    ![Alt text](https://raw.githubusercontent.com/Virus192/Day-12-Setting-Up-an-SSH-Server-and-Analyzing-Authentication-Logs/refs/heads/main/Images/photo_5987967405093143046_w.jpg)

## Analyzing Failed Authentication Attempts

After an hour or so, you should start seeing failed authentication logs. Let’s analyze them:

1. View all failed authentication attempts:

    ```bash
    grep -i failed auth.log
    ```
   ![Alt text](https://raw.githubusercontent.com/Virus192/Day-12-Setting-Up-an-SSH-Server-and-Analyzing-Authentication-Logs/refs/heads/main/Images/photo_5987967405093143047_w.jpg)

2. Filter failed attempts for the `root` user:

    ```bash
    grep -i failed auth.log | grep -i root
    ```

3. Extract IP addresses of failed `root` login attempts:

    ```bash
    grep -i failed auth.log | grep -i root | cut -d ' ' -f 9
    ```

## Investigating Suspicious IPs

Take the IP addresses you’ve found and investigate them using the following tools:

- **[VirusTotal](https://www.virustotal.com/)**
- **[AbuseIPDB](https://www.abuseipdb.com/)**

These tools will help you determine if the IPs are associated with malicious activities.

## Conclusion

Congratulations! You’ve successfully set up an SSH server on Vultr and learned how to analyze its authentication logs. This practical exercise offers valuable insights into server management and basic security monitoring.

As you continue your journey in server administration, remember that regular log analysis is key to maintaining a secure environment. By understanding these logs, you can identify potential security threats and take proactive measures to protect your server. Keep exploring and stay vigilant in your server management practices!
