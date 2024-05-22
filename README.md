# Plant An AD Forest
<h2>Utilities Used</h2>

- <b>Windows Server 2019 ISO File (And OS)</b>
- <b>Windows 10 Enterprise ISO File (And OS)</b>
- <b>A little bit of PowerShell</b>

<h2>Environments Used</h2>

- <b>VirtualBox Hypervisor </b>

<h2>Lab Walk-through:</h2>
<p>In this demonstration, we'll cover some steps to set up a small Active Directory forest in VirtualBox, including a Domain Controller and two client computers.</p>
<br />
<h3>Getting the Windows ISO Files</h3>
To prepare this lab, we'll be getting the ISO files from the Microsoft Evaluation Center. Most of the ISOs you encounter here will have a lifespan of 90 -- 180 days of usage.

<h4>Windows Server 2019</h4>
We'll start with downloading a <a href="https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2019" target="_blank">Windows Server 2019</a> ISO file. Next, fill out your information (uncheck the box for additional communications) and select your language. Then, click <b>Download</b>.
<br/>
<img src="https://i.imgur.com/7Q18kJ0.png" height="50%" width="50%" alt="Windows Server 2019 ISO Download"/>
<br />
<h4>Windows 10 Enterprise</h4>
Next, we'll download a <a href="https://www.microsoft.com/en-us/evalcenter/evaluate-windows-10-enterprise" target="_blank">Windows 10 Enterprise</a> ISO file. Next, fill out your information (uncheck the box for additional communications) and select your language. Then, click <b>Download</b>. Now, we'll prepare the VMs.
<img src="https://i.imgur.com/B1CGAMt.png" height="50%" width="50%" alt="Windows 10 Enterprise ISO Download"/>
<br />

<h3>Windows Server 2019</h3>
Let's first configure our Windows Server 2019 VM as our domain controller. On our VirtualBox VM Manager, create a new VM by clicking the <b>New VM</b> button. Configure the following:
<br/>
<img src="https://i.imgur.com/q62IZCb.png" height="80%" width="80%" alt="VM Name and OS"/>
<br />
<img src="https://i.imgur.com/30MXVBB.png" height="80%" width="80%" alt="Hardware"/>
<br />
<img src="https://i.imgur.com/hAIh2aX.png" height="80%" width="80%" alt="Virtual Hard disk"/>
<br />
Click <b>Finish</b>, but don't start the VM yet!
<br />
<img src="https://i.imgur.com/hAIh2aX.png" height="80%" width="80%" alt="Virtual Hard disk"/>
<br />
<img src="https://i.imgur.com/hAIh2aX.png" height="80%" width="80%" alt="Virtual Hard disk"/>
<br />
<br/>
<img src="https://i.imgur.com/6iAX7e2.png" height="75%" width="75%" alt="Save Changes to Group"/>
<br />

<h3>Sending Profiles</h3>
To send emails, Gophish requires us to configure some SMTP relay details called "Sending Profiles". On the left-hand sidebar of the dashboard, click <b>Sending Profiles</b>. During this configuration, it's important that the "SMTP From" address is a valid email address. We'll fill in the following fields as such and save our profile.
<br/>
<img src="https://i.imgur.com/zwMyhNU.png" height="45%" width="45%" alt="Sending Profile"/>
<br />
Ok, so we now have our Gophish server up and running. We’ve made a group of target recipients and we’ve established a Sending Profile that will launch the phishing campaign. Before we proceed, let’s go to our Kali Linux VM to setup the Credential Harvester tool. 
<br/>

<h3>Utilize the SET Toolkit to Create Malicious Link</h3>
Starting on our Kali Linux VM, let’s ensure connectivity with the Windows 10 VM. 
<br/>
<img src="https://i.imgur.com/5tGoJx5.png" height="75%" width="75%" alt="Kali ping to Windows 10"/>
<br />
<img src="https://i.imgur.com/Yh8LgQW.png" height="75%" width="75%" alt="Windows 10 ping to Kali"/>
<br />
It looks like there is connectivity between the two machines. Now, the credential harvester one of many available tools included in the massive framework called the Social Engineering Toolkit (a.k.a. SET). To start up the SET, we need super user rights to execute its boot command, that is what ‘sudo’ is for. Execute the following command, then press <b>Enter</b>.
<br />
<img src="https://i.imgur.com/0TxS0o3.png" height="75%" width="75%" alt="sudo setoolkit"/>
<br />
For your first time, you might be met with somewhat of a terms of service (TOS) to agree that this tool will not be used for any malicious or unethical reasons. You’re not going to go out in the real-world and utilize this to attempt to steal someone’s credentials. This is all designed for demonstrative purposes only. Agree and hit <b>Enter</b> and you should be met with the following menu:
<br />
<img src="https://i.imgur.com/v6VNBVZ.png" height="55%" width="55%" alt="SET MENU Welcome-page"/>
Now, we are going to be running a social engineering attack, so the first thing we are going to select is option <b>1</b> for <b>Social-Engineering Attacks</b>. Hit <b>Enter</b>. Now, we are met with another menu to choose a specific attack vector. Notice that option <b>2</b> says <b>Website Attack Vectors</b>. Remember, we will be generating a fake website. So, we'll choose option <b>2</b>. Hit <b>Enter</b>.
<br />
<img src="https://i.imgur.com/gU2wQyz.png" height="55%" width="55%" alt="Website Attack Vectors"/>
<br />
Another menu pops up! Here are some attacks that SET has within a web browser. There is a Metasploit attack, a Tabnabbing one, and a Web Jacking one. We're going to choose option <b>3</b>, <b>Credential Harvester Attack Method</b>. Type <b>3</b> and then hit <b>Enter</b>.
<br />
<img src="https://i.imgur.com/SMHprj8.png" height="55%" width="55%" alt="Credential Harvester"/>
<br />
We could clone websites. We can even create our own malicious website. For a quick demonstration, we'll choose option <b>1</b>, where there are templates already provided.
<br />
<img src="https://i.imgur.com/z6Rs54N.png" height="65%" width="65%" alt="Web Templates"/>
<br />
Here the tool will be asking for an IP address to send these captured credentials back to. Since we are keeping this local, we'll keep the IP address that is already provided (highlighted in white), sending it to the Kali Linux machine. We'll make sure to keep the IP address recorded for when we start setting up our phishing campaign.
<br />
<img src="https://i.imgur.com/JCpS1w2.png" height="60%" width="60%" alt="IP address for the POST"/>
<br />
Finally, we are going to create a fake Google login page. At the option menu, type in <b>2</b> and hit <b>Enter</b> to configure a fake Google login page.
<br />
<img src="https://i.imgur.com/u8G7NQA.png" height="60%" width="60%" alt="Select Google Template"/>
<br />
<br />
<img src="https://i.imgur.com/kvcqxJU.png" height="80%" width="80%" alt="google website cloned"/>
<br />
<h3>Send Out Da Phishing Campaign</h3>
<h4>Email Template</h4>
Now that we have a malicious website. We'll jump back to the Gophish admin dashboard on the Windows 10 VM. On the left-hand sidebar, we'll click the <b>Email Templates</b> tab to create our malicious email. This is a critical part of the phishing campaign. This element has a lot to do with what the victim will see once they receive the phishing email. Let's get started by naming this new email template. Provide an Envelope sender, this can virtually be any email. I made up the email address inside <b>Employee Sender</b> field; just to make it look like it's coming from someone affiliated with Google. Since we are planning to send a malicious Google sign-in URL to the victim. Then, we'll proceed to finish up this email template by providing a subject for the email message and creating the content of the email. Notice that I'm on the HTML sub-tab when working on the contents of the email.
<br />
<img src="https://i.imgur.com/zrJMS29.png" height="80%" width="80%" alt="Email Template"/>
<br />
Within the message, we'll embed the link containing the IP address of the Kali Linux VM, the address to where the captured credentials will be sent to. We want to ensure that the victim will open that malicious URL. The reason we use 'http' instead of 'https' is because the credential harvester (malicious URL) is running on port 80 (refers to HTTP). Once we finish the rest of the email message, click <b>Save Template</b>.
<br />
<img src="https://i.imgur.com/QBx7tjO.png" height="80%" width="80%" alt="href...and then save"/>
<br />

<h4>Landing Pages</h4>
The <b>Landing Pages</b> tab will help the phishing campaign redirect users to another website after they submit their credentials. Landing pages are the actual HTML pages that are returned to the users (victims) when they click the phishing links they receive. Hence, we can import the IP address of our Kali Linux VM to ensure that the victim is redirected to the malicious URL to submit their credentials.
<br />
<img src="https://i.imgur.com/1H0gNUO.png" height="75%" width="75%" alt="Landing Page configuration"/>
<br />
Next, we'll navigate to the <b>Campaigns</b> tab and click the <b>New Campaign</b> button.
<br />
<img src="https://i.imgur.com/XTJ7zAC.png" height="70%" width="70%" alt="New Campaign"/>
<br />
We'll provide a name for this campaign. Any name you come up with is fine. Then, we'll select an email template. Here, I will select the one we worked on earlier.
<br />
<img src="https://i.imgur.com/qOt7SJr.png" height="45%" width="45%" alt="Select Email Template"/>
<br />
Then we'll select the Landing Page we reviewed earlier.
<br />
<img src="https://i.imgur.com/NhUr8HW.png" height="45%" width="45%" alt="Select Landing Page"/>
<br />
Then the URL...
<br />
<img src="https://i.imgur.com/I2dXAVZ.png" height="25%" width="25%" alt="Either IP is fine"/>
<br />
Honestly, you can put your Kali's IP address or your local IP address for the URL, the credential harvester should still function the same with either or.
<br />
Then, we'll select our Sending Profile. Once all configurations are selected, click <b>Launch Campaign</b> to send it off.
<br />
<img src="https://i.imgur.com/XG6cHhz.png" height="75%" width="75%" alt="Launch campaign"/>
<br />
<img src="https://i.imgur.com/JRAgKZ2.png" height="40%" width="40%" alt="Campaign Scheduled!"/>
<br />
<h3>Harvest Credentials On Attack Machine</h3>
Now, we'll go check the sample victim emails we launched the campaign toward and it looks like the phishing emails were received!
<br />
<img src="https://i.imgur.com/AGCzKU3.png" height="60%" width="60%" alt="email inbox"/>
<br />
<img src="https://i.imgur.com/d6szVNU.png" height="70%" width="70%" alt="Contents of email"/>
<br />
Above, we can see the email template we created earlier with Gophish.
**A quick note**
In the real world, it's vital to examine every detail in suspicious emails. Big indicators of phishing emails are the grammatic errors. Despite the shady sense of authority from the message, the misspelling and improper email format is usually a dead giveaway, telling most that this email is a phishing attempt. 
<br />
<img src="https://i.imgur.com/FJpR1cQ.png" height="75%" width="75%" alt="Phishing indicators"/>
<br />
We’ll proceed by clicking the hyperlink in the email message, and we’re immediately redirected to a google page. But the URL looks different. It has the IP address of my Kali Linux VM inside the URL tab, which would not normally look right, but this is a good indication that the victim has been successfully redirected to credential harvester URL. I go back to my Kali Linux VM, and the feed shows the activity of the Windows 10 VM connecting to the malicious URL.
<br />
<img src="https://i.imgur.com/HtoxulG.png" height="75%" width="75%" alt="Credential Harvester feed"/>
<br />
So, on the Windows 10 VM, let’s try logging in as the victim who fell for the phishing email. To check our Google account, the victim will input some credentials to log in.
<br />
<img src="https://i.imgur.com/fUQEbez.png" height="80%" width="80%" alt="Sign in to Google..."/>
<br />
Once we click <b>Sign in</b>, we'll navigate back to our Kali machine, we should see what the SET credential harvester tool has captured in real-time, and it turns out that we have captured something!
<br />
<img src="https://i.imgur.com/3K3FwM6.png" height="85%" width="85%" alt="Captured Credentials"/>
<br />
Success! The feed shows the exact same credentials that we just put in as the victim on the Windows 10 VM. We have successfully captured a victim’s credentials through first creating a phishing email and then utilizing the Social Engineering Toolkit as the payload to capture the credentials that the victim would provide. One cool feature of the Credential Harvesting tool is that once a victims’ credentials are captured, the malicious site refreshes and is immediately replaced with the actual site it cloned. Hence, the victim would be directed to the actual Google website after submitting their credentials.
<br />
<img src="https://i.imgur.com/8hG24Zb.png" height="80%" width="80%" alt="Back to regular Google"/>
<br />
