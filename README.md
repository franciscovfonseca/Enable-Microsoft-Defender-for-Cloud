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

  </details>

<h2></h2>

<details close> 
<summary> <h2>4️⃣ Ensure MDC didn’t create another Log Analytics Workspace ➜ Delete it if so</h2> </summary>
<br>
















> Lastly, we're going to induce some **Failed Authentications against the Linux Server**.
> 
> This will allow us to **Generate some Logs in our Linux VM** & and analyse them later as well

<br>

Going back to the **Azure Portal** > Go to **Virtual machines** > Open the ```linux-vm``` > copy its **Public IP Address** 

  ![VM create](https://github.com/user-attachments/assets/cf625627-4567-452b-b13e-d07a8f4cb4b9)

  ![VM create](https://github.com/user-attachments/assets/4668916b-869d-4065-8274-99063e0625ba)

Then inside the Attack VM ➜ we'll open **Powershell**

  ![VM create](https://github.com/user-attachments/assets/8426567a-374f-42f1-b2bf-bf01ad2c2f9e)

Now we can **SSH** ➜ use a **Fake Username** ```josh``` ➜ this Username doesn't exist on the **Linux VM**

So we'll type: ```ssh "FAKE USERNAME"@"DESTINATION (which is the Linux VM)"```  ➜ press "Enter" to attempt to connect:

  ![VM create](https://github.com/user-attachments/assets/7fb6f2d1-c152-43e3-b771-f1bc10716e71)

Type **"yes"** to Accept the Certificate:

  ![VM create](https://github.com/user-attachments/assets/bf5dc7e4-245f-4864-b849-5105d1fa1b4d)

Then it'll ask us to **Enter our Password**

This **User doesn't even exist**: so whatever Password we put ➜ it's going to **Fail to Login & Create a Log**.

Basically we're attempting to **Brute-Force into the Linux VM**  ➜ do it 3 times to **Generate 3 Failed Logins**:

  ![VM create](https://github.com/user-attachments/assets/fab202f7-a7a0-4007-a1ae-df4dc01e9097)

Then we can actually Shut Down our **Attack VM** ➜ we won't be using it anymore for this Lab ➜ and go back to our own Computer

  ![VM create](https://github.com/user-attachments/assets/6922b5a7-bf0e-46b9-ac0b-b79be1074f97)

  </details>

<h2></h2>
<details close>
  
<summary> <h2>5️⃣ Inspect the Logs for RDP & SQL Server in the Windows VM</h2> </summary>
<br>

> So now we're going to connect back to the **Windows VM** ➜ take a look at the **Event Viewer** ➜ and look at the **Logs we Generated**
> 
> We'll do the same thing with the **Linux VM** after ➜ look at the **Logs we Generated** by attempting to Log into it

<br>

Inside our **Windows Vm** > Copy the **Public IP Address**:

  ![VM create](https://github.com/user-attachments/assets/8119aa20-9f4f-4424-a1f8-0630ec596de2)

Open **Remote Desktop** > connect to the **Windows VM**

  ![VM create](https://github.com/user-attachments/assets/7ad32938-0e9a-4b11-8c2b-c05a7ad42f10)

Then open **Event Viewer**:

  ![VM create](https://github.com/user-attachments/assets/926e5fa9-2c64-4711-b66d-5f887bf8a554)

Again, this is where the logs are ➜ First we're going to check out the **"Security"** ones.

These are the logs for when someone attempts to **Connect with Remote Desktop** or even try to **Map a Remote File Share**.

Event ```4625``` is the **Failed Logon Event** ➜ and we can see a whole bunch of them here:

  ![VM create](https://github.com/user-attachments/assets/4784cf0d-b0a6-456b-90d6-f4ad67433c18)

We didn't generate most of these.

If we **"Filter Current Log"** > and type ```4625``` just to see the **Failed Logons** ➜ it'll show us only the **Failed Logons**:

  ![VM create](https://github.com/user-attachments/assets/1cf93df3-ff56-4530-bde5-4d96953ba8c2)

We can see the the **"Account Name"** is different for each Event ➜ and these are **actual bad actors or bots** on the Internet.

These are not our **Intentional Failed Logons** ➜ these are other randon entities trying to **Logon to our VM**, since it's been on for the previous 10 hours.

  ![VM create](https://github.com/user-attachments/assets/ba3540e9-6dbe-4787-b3f1-c12cf654065f)

If we scroll down we can actually find **Our Own Failed Logon** with the **Username** ```josh```

  ![VM create](https://github.com/user-attachments/assets/369ab5b2-bc4f-454d-9920-e7715fdaea48)

⚠️ Aside from our 3 **Intentionally Generated Failed Logs**:
- We can see that there were almost **2000 different Attempts to Break Into our Windows VM**:

  ![VM create](https://github.com/user-attachments/assets/5f796671-51d0-456a-874f-4692309a73e9)

<br>

<h2></h2>

<br>

> Next, because SQL Server is actually installed on this Windows VM ➜ we're going to check the **"Application"** Logs.
> 
> In the Windows Event Viewer, the **SQL Logs** get registered in the **Application Tab** instead of the **Security Tab**.

<br>

Right away ➜  we can see our Successful Login with the User ```sa```:

  ![VM create](https://github.com/user-attachments/assets/e2da67ee-82d6-49f5-9ff5-9622555f97b8)

We're also able to see the **Failed Logins** into the **SQL Server** using the made up **Username** ```josh``` ➜  which does not exist in the **Windows VM**:

  ![VM create](https://github.com/user-attachments/assets/4669752d-99a4-4bac-8223-7ff7eccfc025)

<br>

>   <details close> 
>   
> **<summary> 💡 Summary</summary>**
> 
> From our own Computer ➜ we **RDP into the Windows VM**. 
> 
> We then inspected the **Login Failures and Successes** for both **RDP** as well as the **SQL Server**.
> 
> We looked at the event IDs:
>   - **4625** for the **RDP Failed Logins**
>   - **18456** for the **Failed Logins for the SQL Server**
> 
>   </details>

<br>

  </details>

<h2></h2>

<details close> 
<summary> <h2>6️⃣ Inspect the Logs for the Linux VM</h2> </summary>
<br>

> The next thing we're going to do is **Login to the Linux VM**.
> 
> And then we're going to take a look at the **Failed Logs** and finish this lab.

<br>

To **Attempt to Connect to the Linux VM** ➜ we first need the get the **IP Address of the Linux VM**:

  ![VM create](https://github.com/user-attachments/assets/8e383e43-822b-406f-83d6-7ed9692019dc)

From our Computer:
- if you're using a **Mac** ➜ **open Terminal**
- if you're using **Windows** ➜ **open Powershell**

And type in the following:

```commandline
ssh labuser@PUBLIC IP ADDRESS OF THE LINUX VM
```
<br>

Press **"Enter"** > then type the **Password**: ```Cyberlab123!``` > then press **"Enter"** again

  ![VM create](https://github.com/user-attachments/assets/96d6e073-43de-413b-9371-97b70d671a65)

We are now Logged Into the **Linux VM**

To see the **Logs** we can type in the following **Linux Command**:

```commandline
cd /var/log
```
<br>

☝️ This will basically change our Directory to the **Log's Directory**

  ![VM create](https://github.com/user-attachments/assets/71f782a5-c731-4926-bc70-7af4558e9e4d)

And then we can type ```cat auth.log | grep password``` to pull out all the "lines" that have the word **"Password"** in it:

  ![VM create](https://github.com/user-attachments/assets/f73e017f-4b09-4685-bc6c-ea81a1ea614c)

We can see a whole bunch of **Failed Password for Invalid User** Events:
- Meaning ➜ some entities were trying to **Login to our Linux VM** from **Random IP Addresses** using **Wrong Credentials**.

We can also see our **Successful Logins** using the **Username** ```labuser```:

  ![VM create](https://github.com/user-attachments/assets/33d290c3-390f-4ead-bd48-f58e662a7eb5)

If we filter through:
- ```Accepted``` ➜  we can see that only we were able to **Successfully Login**:

```commandline
cat /var/log/auth.log | grep Accepted
```
<br>

- ```josh``` ➜  we can see all the **Unsuccessful Login Attempts** with the Username "josh":

```commandline
cat /var/log/auth.log | grep josh
```
<br>

  ![VM create](https://github.com/user-attachments/assets/0618dcc7-8548-4f5a-8a0a-bf95eb5759b0)


✅ This is Cybersecurity!


  </details>

<br>

<br>

<br>

# Conclusion


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
 
