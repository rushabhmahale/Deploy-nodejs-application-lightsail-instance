# Deploy-nodejs-application-lightsail-instance


https://user-images.githubusercontent.com/63963025/207778386-cffd99d6-f4ff-4f29-a0f3-8675a4ac98a2.mp4


## What is Amazon Lightsail? 
Amazon Lightsail is a virtual private server (VPS) provider and is the easiest way to get started with AWS for developers, small businesses, students, and other users who need a solution to build and host their applications on cloud. Lightsail provides developers compute, storage, and networking capacity and capabilities to deploy and manage websites and web applications in the cloud. Lightsail includes everything you need to launch your project quickly – virtual machines, containers, databases, CDN, load balancers, DNS management etc. 

Refer this document:- https://lightsail.aws.amazon.com/ls/docs/en_us/articles/what-is-amazon-lightsail

## What is a Virtual Private Server?
A virtual private server, also known as an "instance", allows users to run websites and web applications in a highly secure and available environment, while being cost effective.

Refer this document:- https://aws.amazon.com/lightsail/faq/#

## What is Node Js?
Node.js is an open-source server environment. Node.js is cross-platform and runs on Windows, Linux, Unix, and macOS. Node.js is a back-end JavaScript runtime environment. Node.js runs on the V8 JavaScript Engine and executes JavaScript code outside a web browser.

Refer this document:- https://www.w3schools.com/nodejs/nodejs_intro.asp

## Lightsail support? 
Lightsail offers a range of operating system and application templates that are automatically installed when you create a new Lightsail instance. Application templates include WordPress, Drupal, Joomla!, Ghost, Magento, Redmine, LAMP, Nginx (LEMP), MEAN, Node.js, Django, and more.


## Steps to be followed
### Step 1 Create Lightsail instance
- Go to Home console search lightsail service.
<img width="1109" alt="image" src="https://user-images.githubusercontent.com/63963025/206380044-027782c6-c8e2-4c57-934e-bbf2c6cc62c0.png">

- Create instance select india region <b>ap-south-1a (Mumbai)</b>. Select platform os linux/unix.
<img width="707" alt="image" src="https://user-images.githubusercontent.com/63963025/206380538-ace961b5-89b1-487d-b3a6-700f5a1493fc.png">

- Select blueprint i want to deploy nodejs application so ia mselccting nodejs. 
<img width="772" alt="image" src="https://user-images.githubusercontent.com/63963025/206384312-b3d7a55b-2028-4343-84a7-c2a8a9d7fb99.png">

- Create new key 
<img width="650" alt="image" src="https://user-images.githubusercontent.com/63963025/206384603-5e8f3199-2ad4-476b-a326-3416041dc891.png">

- Select plan 
<img width="905" alt="image" src="https://user-images.githubusercontent.com/63963025/206384839-681af2f7-c993-46cb-9132-704a883b9167.png">

- Name your instance
<img width="646" alt="image" src="https://user-images.githubusercontent.com/63963025/206384968-0a57b292-5e3c-4691-b4e4-461f16d06b27.png">

- Machine is ready lets ssh into the machine and deploy our Nodejs application. 
<img width="1030" alt="image" src="https://user-images.githubusercontent.com/63963025/206385220-70862e62-8679-42e7-932d-be13b1eb9dda.png">


### Step 2 install code in lightsail instance
- Now go to termainal icon you will able to ssh directly into machine. 
<img width="482" alt="image" src="https://user-images.githubusercontent.com/63963025/206385758-0a8d5a08-e528-4787-ba3f-de1b54f75c97.png">

- Terminal
<img width="991" alt="image" src="https://user-images.githubusercontent.com/63963025/206385951-a0dd9a65-ac6b-4701-8ecd-3f9b16fd6e84.png">

- LightSail NodeJs the root directory is.
```
cd /opt/bitnami/apache2/htdocs
```
<img width="752" alt="image" src="https://user-images.githubusercontent.com/63963025/206386301-03854a7e-7d59-432e-8254-1f0ab38e93d5.png">

- Bydefault webpage of Bitnami Node.js.
<img width="1209" alt="image" src="https://user-images.githubusercontent.com/63963025/206387468-4a232980-a5e7-45cf-ac1b-ccde529ae89c.png">

- Now download your code from github 
```
git clone https://github.com/rushabhmahale/Deploy-nodejs-application-lightsail-instance.git
```
<img width="995" alt="image" src="https://user-images.githubusercontent.com/63963025/206399865-2b5c8426-5911-44ec-aec4-432ca2af10b2.png">


- install node package
```
npm install
```
<img width="1081" alt="image" src="https://user-images.githubusercontent.com/63963025/206400289-6d351b53-029d-45f9-9b01-4d69b05c70bb.png">

### Step 3 Deploy application in lightsail instance 

- Let's run the following commands to install and start our application with pm2.
```
sudo npm i -g pm2
pm2 start index.js
```
<img width="1391" alt="image" src="https://user-images.githubusercontent.com/63963025/206401581-65d5f88c-3ed2-4e21-9b93-a57117dcb380.png">

- create a conf folder 
```
sudo mkdirsudo mkdir /opt/bitnami/conf
```
- Go inside that directory you have created 
```
cd /opt/bitnami/conf
```
<img width="610" alt="image" src="https://user-images.githubusercontent.com/63963025/206466992-e8a11742-cfdd-4d5b-9fb1-af2479d5bda5.png">

- Create a new file httpd-prefix.conf (exit with wq!).
```
sudo vi /opt/bitnami/conf/httpd-prefix.conf
```
<img width="473" alt="image" src="https://user-images.githubusercontent.com/63963025/206467273-c525190f-e9a5-46dc-9dbb-b2bda382a7c9.png">

- Now go to config file httpd-app.conf(exit with wq!).
```
sudo vi /opt/bitnami/conf/httpd-app.conf
```
- Add this content inside the file
```
Add ProxyPass / http://127.0.0.1:3000/

ProxyPassReverse / http://127.0.0.1:3000/
```

<img width="462" alt="image" src="https://user-images.githubusercontent.com/63963025/206470606-c9de7574-5919-43a7-a436-ff4abfba5c7a.png">

- Now go to Apache file location
```
cd /opt/bitnami/apache2/conf/bitnami
```
- Open the file 
```
sudo vi bitnami.conf
```
- Include inside in the file 
```
Include "/opt/bitnami/conf/httpd-prefix.conf"
```
<img width="661" alt="image" src="https://user-images.githubusercontent.com/63963025/206471585-b4a981e6-9a1f-4abb-875e-da63b8c1c229.png">

- Restart apache service using the below commands.
```
sudo /opt/bitnami/ctlscript.sh restart apache
```
- Now start node js application where your index.js is located. 
```
npm start
```
<img width="980" alt="image" src="https://user-images.githubusercontent.com/63963025/206631745-ea355f74-a620-44fe-9b3f-c7744a4982f7.png">

- Now go to Lightsail Home --> Instance --> Manage.
<img width="506" alt="image" src="https://user-images.githubusercontent.com/63963025/206473716-276a908a-5007-4a59-92c8-71fa2e830663.png">

- Now go to Networking section edit firewall (Security Group). In the Ipv4 section. 
<img width="995" alt="image" src="https://user-images.githubusercontent.com/63963025/206474407-4e386887-c0f4-4bbc-9c48-b50809cefcbe.png">

- Add rule --> Custom TCP 3000 Your node js application is running on port number 3000.
<img width="826" alt="image" src="https://user-images.githubusercontent.com/63963025/206631924-4afe00a5-0eba-4bec-aef8-08f8774f813c.png">

<img width="795" alt="image" src="https://user-images.githubusercontent.com/63963025/206632094-43c4b783-0a8d-4de7-81f6-5b94c396e857.png">

- Copy your ip address and open in the browser. 
<img width="813" alt="image" src="https://user-images.githubusercontent.com/63963025/206632443-0c5abe88-21d0-4c88-b5eb-f176118b89fb.png">

- Here we go our application is exposed on port 3000. 
<img width="409" alt="image" src="https://user-images.githubusercontent.com/63963025/206632398-2dea4b1f-41e9-47af-a596-ed684f1ad4af.png">

