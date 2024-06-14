# How to deploy (agro-api)

## Database:
You can use any database that strapi supports:
- postgres
- mysql
- sqlite

Important to set cyrilic localization in database so search will work properly.
If you are going to use docker compose from this repo it will happen automatically for postgres database.

## Hosting
You can use your own server and setup deploy from terminal or you can use something like google cloud run.

 - ### [Google Cloud Run](https://cloud.google.com/run?hl=en) 
To use Google Cloud Run you need to build an image with the following command:

`docker buildx build --platform linux/amd64 -t  <yourImageName:tag> .`

Google Cloud Run requires the image to be build on linux64 architecture

After you build your image you need to push your image to docker hub or Artifact Registry

---

Then you need to create project and setup service
Also your billing method

<img width="1440" alt="339812361-dc6063cf-1a24-4e03-827b-5585b77196b7" src="https://github.com/Coderfy-com/agro-deploy-doc/assets/83612717/e76f14b9-d6ea-40f0-bc16-9cae89cb5eaf">

---

Create service interface

<img width="990" alt="339753790-79837b8b-522a-49be-aa74-5385ab1b095d" src="https://github.com/Coderfy-com/agro-deploy-doc/assets/83612717/816c434b-fa1c-4b1b-810b-e37c2fdfa935">

---

You should provide a link to your image that you can get from docker hub
It should look similar to this `docker.io/YOUR_USERNAME/YOUR_REPO_NAME:TAG` (TAG is optional but I recomend using it)

<img width="591" alt="339754283-ed5feac4-f11e-4b93-8172-e7d3718a814f" src="https://github.com/Coderfy-com/agro-deploy-doc/assets/83612717/ee1a5098-55ec-40ed-af47-793baddc1b06">

---

Name your service and pick server location
It is better to choose a server closer to your clients (in our case Ukraine)

<img width="571" alt="339755014-bb674f79-3685-4b38-9661-2db374c0e4df" src="https://github.com/Coderfy-com/agro-deploy-doc/assets/83612717/2fca2814-9c59-46cf-969c-012bf1cc14c2">

--- 

Pick 'Allow unauthenticated invocations'
CPU allocation and pricing:
1. CPU is only allocated during request processing - is cheaper but there might be cold starts (if server didn't get any requests it will be turned off and next request will take 4 sec to load)
2. CPU is always allocated - more expensive than first option but there is no cold starts

<img width="589" alt="339775330-3efd18c8-c2d4-4ef9-8705-10d6b4bcb3d1" src="https://github.com/Coderfy-com/agro-deploy-doc/assets/83612717/6186d576-acee-476a-a44c-ef31b71ab63e">

---

Set 1337 port (Api runs on this port)
And you might want to increase memory (I tested it with 2 gigs and I think it is optimal)

<img width="535" alt="339777070-8ad864bf-4b01-411d-8df6-10fcedd2d3df" src="https://github.com/Coderfy-com/agro-deploy-doc/assets/83612717/59d031d9-383f-49a6-b299-269023b9b82d">

---

Click 'Create' button and wait a little bit.
At the end should get a url to your deploy

Login as Admin and check that all endpoints are publicly awailable

<img width="1717" alt="339779135-c6c5a83c-1af6-48ee-b594-1ba2aa8d0984" src="https://github.com/Coderfy-com/agro-deploy-doc/assets/83612717/9d737baa-9b1e-44cc-948d-902bcfeaa50a">

- ## Self hosting with docker

- Docker is required

- Clone this repo
- Set your .env and docker.env (you can find examples in agro-api folder)
- Setup docker volume in docker-compose.yaml by default the volume is located at `/var/lib/data/agro/postgres` make shure this path exists and docker can read and create files in that directory.
- Run `docker compose up -d`
- Setup your webserver to make your deploy publicly available

# Data transfer

## [Strapi Data transfer](https://docs.strapi.io/dev-docs/data-management/transfer)

- You can transfer data from https://greenfort.coderfy.com/admin

---
  
<img width="1700" alt="339805530-c3fb77fe-88ec-44c4-99a8-3bd370a27609" src="https://github.com/Coderfy-com/agro-deploy-doc/assets/83612717/48b23f93-5728-4cb1-8c9b-5c4a35cc5e7c">

---

<img width="1208" alt="339806164-a448cb88-b4a0-448d-9d3b-17e9bcd15574" src="https://github.com/Coderfy-com/agro-deploy-doc/assets/83612717/5395835e-82f2-49ac-b077-243cd531d5fd">

---
Copy your token

<img width="1194" alt="339806318-553a3990-12bf-4668-82a9-d222fd29240d" src="https://github.com/Coderfy-com/agro-deploy-doc/assets/83612717/156c604c-597e-40a0-9ede-4d319bfcef59">

---

Use these commands to transfer data
For more detailed information read strapi docs

`npm run strapi transfer -- --to YOUR_DOMAIN/admin`

`npm run strapi transfer -- --from YOUR_DOMAIN/admin`

After you deploy api you need to change domain in the app





