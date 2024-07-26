<br>

<h1 align="center">Enabling Microsoft Defender for Cloud</h1>

<br>

<p align="center">
<img width="800" src="https://github.com/user-attachments/assets/77162ed6-a76e-4475-a6e0-ecea427069b2" alt="Banner"/>
<br />

<br />

In this lab we're going to Enable Microsoft Defender for Cloud.

Microsoft Defender for Cloud gives us a highlevel view of our Azure Environment in terms of Security and Secure Score.

It also allows us to take Logs from Virtual Machines and NSGs and ingest them into our Log Analytics Workspace.

So that's what we will be doing in this lab ➜ Set Up Microsoft Defender for Cloud.

<br />

<details close> 
<summary> <h2> 1️⃣ Enable Microsoft Defender for Cloud for Log Analytics Workspace</h2> </summary>
<br>

> First thing we're going to do is Enable Defender for Cloud for our Log Analytics Workspace.
> 
> This will allow us to forward Logs from the Virtual Machines into the LAW.

<br>

Got to the **Azure Portal** ➜ search for **"Defender for Cloud***:

![azure portal](https://github.com/user-attachments/assets/259c4d7a-ca98-4046-93a0-3472a839f47d)

Then we'll click on **"Environment settings"**:

![azure portal](https://github.com/user-attachments/assets/259c4d7a-ca98-4046-93a0-3472a839f47d)

Expand the ```∨``` next to **"Azure subscription 1"**

All the way on the right side for the **"LAW--Cyber-Lab-01"** line ➜ click on ```...``` ➜ and then **"Edit settings"**:

![azure portal](https://github.com/user-attachments/assets/259c4d7a-ca98-4046-93a0-3472a839f47d)

First we'll go to the **"Defender plans"** tab.

So now we'll **Turn On** MDC for **"Servers"** as well as for **"SQL servers on machines"** ➜ since we do have a SQL Server instance.

<br>

>   <details close> 
>   
> **<summary> 💡 </summary>**
> 
> This will allow us to **Collect Logs** from these resources.
> 
>   </details>

<br>

Make sure you click the 💾 **Save** button:

![azure portal](https://github.com/user-attachments/assets/259c4d7a-ca98-4046-93a0-3472a839f47d)

Then we'll go to the **"Data collection"** tab ➜ and check **"All Events"**

<br>

>   <details close> 
>   
> **<summary> 💡 </summary>**
> 
> This will allow us to **Collect All Events from the Windows Security Log**.
> 
> Which is like the **Windows Event Viewer**, where we can see people attempting to **Log Into our Windows Machines over the Internet**.
> 
> We're going to be able to **Collect Logs** from that and then **Forward Them to this Log Analytics Workspace**.
> 
>   </details>

<br>

Again ➜ click the 💾 **Save** button:

![azure portal](https://github.com/user-attachments/assets/259c4d7a-ca98-4046-93a0-3472a839f47d)

  </details>

<h2></h2>

<details close> 
<summary> <h2>2️⃣ Enable Microsoft Defender for Cloud for the Subscription</h2> </summary>
<br>

Go back to the **MDC** ➜ **"Environment settings"**

This time for the **"Azure subsription 1"** line ➜ click on ```...``` ➜ and then **"Edit settings"**:

![azure portal](https://github.com/user-attachments/assets/259c4d7a-ca98-4046-93a0-3472a839f47d)

So now we'll Turn MDC On for **"Servers"**, **"Databases"**, **"Storage"** & **"Key Vault"**.

>   <details close> 
>   
> **<summary> 💡 </summary>**
> 
> We'll create a Storage Account and Key Vault instances in a subsequent lab.
> 
>   </details>

Then click on **"Settings >"** under **"Monitoring coverage"** for the **Servers**:

![azure portal](https://github.com/user-attachments/assets/259c4d7a-ca98-4046-93a0-3472a839f47d)

We'll now click on **"Edit configuration"** for the **Log Analytics agent**.

And for the **Workspace** ➜ pick our actual ```LAW--Cyber-Lab-01``` workspace

>   <details close> 
>   
> **<summary> 💡 </summary>**
> 
> We don't want it to automatically create a new LAW ➜ we want to use the one we created.
> 
> We're basically onboarding our Virtual Machines to our LAW and then forward the Logs to it
> 
>   </details>

Make sure you click **"Apply"** and then 💾 **Continue**:

![azure portal](https://github.com/user-attachments/assets/259c4d7a-ca98-4046-93a0-3472a839f47d)

After that we'll click on the 💾 **Save** button to save the **Defender plans for the Subscription**:

![azure portal](https://github.com/user-attachments/assets/259c4d7a-ca98-4046-93a0-3472a839f47d)

  </details>

<h2></h2>

<details close> 
<summary> <h2>3️⃣ Enable Microsoft Defender for Cloud Continuous Export in Environment Settings</h2> </summary>
<br>

Still inside the **"Edit settings"** for the Subscription ➜ we'll go to the **"Continous export"** blade now.

Click on the **"Log Analytics workspace"** tab ➜ and make sure **"Export enabled"** is **Turned On**:

>   <details close> 
>   
> **<summary> 💡 </summary>**
> 
> Doing this will **Export Alerts into our LAW** so we can **Query Them Later**.
> 
> So if **Defender for Cloud** discovers there's some problem with our Environment, like a **Brute-Force Attack** going on, or there's a **Poor Configuration** for example ➜ MDC will **Export those Alerts into our LAW** ➜ which will let us **Query Them Later**
> 
>   </details>

![azure portal](https://github.com/user-attachments/assets/259c4d7a-ca98-4046-93a0-3472a839f47d)

So we'll enable ☑️ **Exported data types** for all of the following options:

>   <details close> 
>   
> **<summary> 💡 </summary>**
> 
> We didn't actually configure **"Regulatory compliance"** yet, but we'll do that in a future lab.
> 
> This will basically enable **NIST 800-53** for our Environment to see what controls are missing in certain areas.
> 
>   </details>

![azure portal](https://github.com/user-attachments/assets/259c4d7a-ca98-4046-93a0-3472a839f47d)

For the **"Export configuration"** option let's just configure it to our **Resource group** ```RG-Cyber-Lab```

And also for the **"Export target"** we'll select our **Target Workspace** ```LAW-Cyber-Lab-01```

>   <details close> 
>   
> **<summary> 💡 </summary>**
> 
> This is the Target workspace where we want to Export the Alerts to ➜ so we have to select our LAW
> 
>   </details>

We'll then click 💾 **Save**

![azure portal](https://github.com/user-attachments/assets/259c4d7a-ca98-4046-93a0-3472a839f47d)

<h2></h2>

  </details>

<br>

<br>

<br>

# Summary

<br>

That wraps things up for this lab.

We just enabled **Microsoft Defender for Cloud**, which can show us our Security Posture and gives us Insights into a lot of things.

Primarily it will allow us to take **Logs from our Virtual Machines** and **Forward them into our Log Analyitcs Workspace**.

We also enabled Defender for Cloud for Storage Account & Key Vault which we will Set Up and Use in future labs.





We have to keep in mind hat if we have, let's say, 1000 computers in our Environment ➜  it would be too laborious to just login into each one of them, and analyse the each log indivudually this way.

That's why we are going to **Automatically Ingest all the Logs into a Central Repository**.

We'll Set Up Queries to Automatically look through the Logs and Alert us on certain Events.

This is the end of our **Logging and Monitoring Lab**, and in the next phases we're going to Inspect Logs, Create Incidents & Respond to those Incidents.

<br />

<br />

<br />  

<br /> 

<br />

<br />  

<br /> 
 
