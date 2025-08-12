# Bounty Hacker

Bounty Hacker

![FirstPage.png](Bounty%20Hacker%20246b66e397c980019701ee14db4c0e62/FirstPage.png)

After we start the machine it will gives us a target ip address `10.10.189.161`

we will paste it on the browser to see if there is a hint given on the web page . then we will get the below information

![secondPage.png](Bounty%20Hacker%20246b66e397c980019701ee14db4c0e62/secondPage.png)

 **scan a target system to detect open ports and the services running on those ports**, **including version information**.we will run the following command `nmap -sV 10.10.189.161`

![nmapConfig.png](Bounty%20Hacker%20246b66e397c980019701ee14db4c0e62/nmapConfig.png)

## **TASK 1**

The First Question ask us **“who wrote the task list?”**  and also we have given

**Question Hint:      To Use FTP**

After we checked every open ports and running services we will jump to Navigate Using 

`ftp [TARGET_ADDRESS]` 

`ftp 10.10.189.161`

![ftpTarget.png](Bounty%20Hacker%20246b66e397c980019701ee14db4c0e62/ftpTarget.png)

### NOTE:   we will use name = anonymous   It's a way to **access an FTP server without needing a real user account**.

⇒ After Accessing remotely using `ftp` we should see all the contents of the remote Device by using `ls`  command .   We will get the following files yet not downloaded 
…………………………….      locks.txt

…………………………….      task.txt

![listingFTPfile.png](Bounty%20Hacker%20246b66e397c980019701ee14db4c0e62/listingFTPfile.png)

### ⇒ Then we should download these two remote files to local device

![DownloadingFtpFile.png](Bounty%20Hacker%20246b66e397c980019701ee14db4c0e62/DownloadingFtpFile.png)

We can see them on our local device 

![seeDownloadedFile.png](Bounty%20Hacker%20246b66e397c980019701ee14db4c0e62/seeDownloadedFile.png)

Now We have got the first task we were asked to discover **“who wrote the task list”** by using 

`cat task.txt` file we will get the writer 

![whoWroteIt.png](Bounty%20Hacker%20246b66e397c980019701ee14db4c0e62/whoWroteIt.png)

**task 1 finished** 

## TASK 2

**What service can you buruteForce with text file found ?**

Consider We have given hint on the challenge

**HINT: its on port 22**    

See the picture where we navigate the target address with `nmap` command  to scan the open ports . we get the port 22 service is running on **`ssh`**

![nmapConfig.png](Bounty%20Hacker%20246b66e397c980019701ee14db4c0e62/c322d059-b052-46d6-8043-a501ebc50c2a.png)

## TASK 3

**What is the user password?**

Consider We have given hint on the challenge 
**HINT: Using hydra will help you**

So we will find the password of the user using hydra command from the file named Locks.txt

`hydra -l lin -p locks.txt ssh://10.10.189.161 -t 1`

This command will Gives us the requested password 

![buruteForcingUsingHydra.png](Bounty%20Hacker%20246b66e397c980019701ee14db4c0e62/88ad7620-a68b-4309-9a2b-d269e8d1ecb4.png)

**password: RedDr4gonSynd1cat3     ⇒ Task finished**

## TASK 4

**What is the content in User.txt file?**

> After we get all necessary information and credential of the remote user, we need to access remote  Device by using the remote user name and its password. we use `ssh` command to perform remote access .    `ssh lin@10.10.189.161`
> 

Our task is to read the content of **User.txt** file from remote device 

![RemoteAccessing.png](Bounty%20Hacker%20246b66e397c980019701ee14db4c0e62/RemoteAccessing.png)

Now we have successfully logged in to remote device using credentials Our next task is to interact with remote Device!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

We will try to see the items of the remote user using `ls` command

- In the Desktop directory we will get User.txt file so to read the content of the file we will use

`cat user.txt`  command then Will find our first FLAG 

> THM{CR1M3_SyNd1C4T3}
> 

## TASK 5

**What is the content in root.txt file ?**

To get the root.txt file we must be in root directory so first we will ask the machine what kinds of command will we use the user on *bountyhacker* machine to be a root user from remote by using the following command `sudo -l`

- the command line will ask us to provide the user password so we will enter the previous password of the user which is : **RedDr4gonSynd1cat3**

it will show us the user can use the following commands on the *bountyhacker* machine using sudo

**(root) /bin/tar**

we can use the following `sudo tar` command to be a root on the remote machine 

**Sudo**

> If the binary is allowed to run as superuser by sudo, it does not drop the elevated privileges and may be used to access the file system, escalate or maintain privileged access.
> 

```
sudo tar -cf /dev/null /dev/null --checkpoint=1 --checkpoint-action=exec=/bin/sh

```

When we run the above command on on the remote machine it will makes us the root user .

then we will change our current directory to root   `cd  /root` 

then we will list out the items of root directory we will see a file named **root.txt**

Our final task is to read the content of **root.txt** file  …… `cat root.txt` it will gives us the final FLAG

> **THM{80UN7Y_h4cK3r}**
> 

We Have Finished Our Tasks!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!

## Prepared by Sirajudin

# **THANK YOU**