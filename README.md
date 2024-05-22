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
<img src="https://i.imgur.com/3H0FGXs.png" height="50%" width="50%" alt="Network Settings Win Server 2019"/>
<br />
<img src="https://i.imgur.com/xhlKpnr.png" height="80%" width="80%" alt="Win Server 2019  Network Adapters"/>
<br />

<h3>Windows 10 Enterprise Template</h3>
Now, we'll create a new VM and give it a name such as <b><i>Win10EnterpriseTemplate</i></b>.
<br/>
<img src="https://i.imgur.com/5NUCs6B.png" height="80%" width="80%" alt="Create Win10EnterpriseTemplate"/>
<br />
<img src="https://i.imgur.com/qcZ29aP.png" height="80%" width="80%" alt="Hardware"/>
<br />
<img src="https://i.imgur.com/XLLFNp9.png" height="80%" width="80%" alt="Virtual Hard disk"/>
<br />
Again, click <b>Finish</b>, but do not start the VM yet! We'll go to the network settings of the VM.
<br/>
<img src="https://i.imgur.com/z236WTf.png" height="60%" width="60%" alt="Win10Enterprise Network Settings"/>
<br />
<img src="https://i.imgur.com/4EKyJtJ.png" height="80%" width="80%" alt="Win10EnterpriseTemplate Network Adapter"/>
<br />
Make sure to save the settings of the VM and now we'll start the installation of the operating systems.
<br />
<h3>Windows Server 2019</h3>
We'll hover over our newly created Windows Server 2019 VM and double-click to start the VM. Once booting finishes, Choose languge > Click <b>Install Now</b>.
<img src="https://i.imgur.com/Gnh0EGN.png" height="75%" width="75%" alt="Choose Language"/>
<br />
Choose <b>Windows Server 2019 Standard Evaluation (Desktop Experience)</b>
<img src="https://i.imgur.com/e9H4q1x.png" height="75%" width="75%" alt="Choose Standard Evaluation (desktop experience)"/>
<br />
We'll click <b>Next</b> and accept the terms and conditions. Then, we'll choose a <b>Custom</b> installation of Windows.
<br />
<img src="https://i.imgur.com/Zgy0KNX.png" height="75%" width="75%" alt="Custom: Install Windows..."/>
<br />
Click <b>Next</b> and wait for the installation to finish.
<br />
<img src="https://i.imgur.com/iDtp03c.png" height="55%" width="55%" alt="Installing Windows"/>
<br />
Enter a local administrator password and keep it in your records.
<br />
<img src="https://i.imgur.com/YfhVRHt.png" height="75%" width="75%" alt="Customize Settings"/>
<br />
Now, with VirtualBox, we'll click <b>Input</b> > <b>Keyboard</b> > <b>CTRL + ALT + DEL</b> to enter <b>CTRL + ALT + DEL</b> into the VM, and log in with your local Administrator password.
<br />
<img src="https://i.imgur.com/8JxQdlk.png" height="75%" width="75%" alt="Administrator Login"/>
<br />
Now, we'll configure the Server's Network Interface. In my environment, the pfSense DHCP service has been disabled for the AD (Active Directory) lab LAN, because we want the domain controller to act as the DHCP server for the client Windows computers. Therefore, we'll need to manually configure the domain controller.

<br />
To get started, on the Windows Server 2019 VM, we'll right-click the network interface icon and choose <b>Open Network & 
 Internet Settings</b>
 
<br />
<img src="https://i.imgur.com/2DV62M9.png" height="15%" width="15%" alt="Network Interface Icon"/>
<br />
<img src="https://i.imgur.com/pT0crPJ.png" height="35%" width="35%" alt="Open Network & Internet Settings"/>
<br />
Scroll down and choose <b>Change adapter options</b>
<br />
<img src="https://i.imgur.com/Kxz9gZD.png" height="50%" width="50%" alt="Change adapter options"/>
<br />
Right-click the adapter and choose <b>Properties</b>
<br />
<img src="https://i.imgur.com/JfJF1qu.png" height="60%" width="60%" alt="Properties"/>
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
