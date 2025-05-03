# Minecraft-AWS-Server
Commands used to create, and manage my AWS 1.21.1 All The Mods 10 Minecraft Modded Server

Important Setup:
Step 1: Install Modded Minecraft Server Files:
- Using CurseForge, find the server you'd like to use, and click the install server files button
Step 2: Create S3 Bucket:
- Open AWS S3, click on Create bucket, give it a name and click Create.
- Open the new bucket and upload your downloaded Server-Files zip you just got from CurseForge
Step 3: Setting up the IAM Policy
- This is a crucial step as it will allow you to give EC2 instances permissions to access your uploaded file, this step can be bypassed by creating an IAM policy with every EC2 and S3 bucket permission, but this isn't recommended as it's best that you lay out the permissions of file access to manage your servers security. Plus you might learn something!
- On my GitHub page open my IAM Policy JSON file
- Open AWS IAM, click on Policies and create a new policy, feel free to copy and paste my JSON code into it. There is a JSON explanation file on my git if you'd like to read about what it's doing.
- After you've created the policy, go into IAM roles and create a new role. The trusted entity type should be AWS service, and the Use Case set to EC2. Click next, and search for your newly created policy, click next, and then give it a name and create it.
Step 4: Create an EC2 instance
- Go to AWS EC2, and click on Create an instance, I highly recommend using Amazon Linux as it's the cheapest option for computing. Also, Linux terminals aren't too bad.
- In instance type I highly recommend using t2.large or t2.xlarge, modded minecraft is very heavy on RAM usage, so the bigger the better, note it is more expensive the higher you go. So choose carefully. AWS billing is brutal and confusing.
- Don't worry about key pairs, they're not necessary for what we're trying to do, so just set it to "Proceed Without A Key Pair"
- In Network Setting click "edit" and add two new security groups, the first being a custom TCP and the second being a custom UDP, you'll need to set the port for both of these to 25565-25565. This is the port Minecraft uses if you're server has started but no one can join it, this is most likely why.
- Finally, open advanced details, click on the IAM instance profile and select the role you created in IAM.

You're done! Now launch your EC2 instance, connect to it, and follow the EC2 commands found in my git hub. NOTE: my ec2 commands will only work for Forge Serevers past Minecraft 1.18, as they changed how you start servers, the process is similar, but my ec2 commands will not start your server.

Common Issues I ran into:
- if you run into any access denied error it's due to your IAM policy, make sure that your policy JSON files are being applied to the bucket and the items inside the bucket (apply to items in the bucket by adding /*)
- if you're server won't start/instance crashes, increase your EC2 instance size by stopping it, and changing its type.
