# Deploy-nodejs-application-lightsail-instance

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


- Install Nginx 
```
sudo apt-get install nginx 
```
- <img width="1384" alt="image" src="https://user-images.githubusercontent.com/63963025/206402408-2a214485-2bda-4884-baf8-6c5c6a1280f9.png">

- Edit conf file of Nginx 
```
sudo vi /etc/nginx/sites-enabled/default
```
<img width="760" alt="image" src="https://user-images.githubusercontent.com/63963025/206402872-03d627fa-ea2f-4aac-9af4-7a0f300bc530.png">

- Add this content in conf file 
<img width="730" alt="image" src="https://user-images.githubusercontent.com/63963025/206403646-b9979a9f-014e-49a0-85dd-7e3854e3890b.png">

- Restart nginx service
```
sudo systemctl restart nginx 
```


