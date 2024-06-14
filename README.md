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

<img width="1440" alt="Screenshot 2024-06-14 at 14 42 07" src="https://github.com/Coderfy-com/agro/assets/83612717/303510c8-7005-4b1c-b01a-7ba7b5dac020">

---

Create service interface

<img width="990" alt="Screenshot 2024-06-14 at 14 44 51" src="https://github.com/Coderfy-com/agro/assets/83612717/79837b8b-522a-49be-aa74-5385ab1b095d">

---

You should provide a link to your image that you can get from docker hub
It should look similar to this `docker.io/YOUR_USERNAME/YOUR_REPO_NAME:TAG` (TAG is optional but I recomend using it)

<img width="591" alt="Screenshot 2024-06-14 at 14 46 09" src="https://github.com/Coderfy-com/agro/assets/83612717/ed5feac4-f11e-4b93-8172-e7d3718a814f">

---

Name your service and pick server location
It is better to choose a server closer to your clients (in our case Ukraine)

<img width="571" alt="Screenshot 2024-06-14 at 14 49 53" src="https://github.com/Coderfy-com/agro/assets/83612717/bb674f79-3685-4b38-9661-2db374c0e4df">

--- 

Pick 'Allow unauthenticated invocations'
CPU allocation and pricing:
1. CPU is only allocated during request processing - is cheaper but there might be cold starts (if server didn't get any requests it will be turned off and next request will take 4 sec to load)
2. CPU is always allocated - more expensive than first option but there is no cold starts

<img width="589" alt="Screenshot 2024-06-14 at 16 05 20" src="https://github.com/Coderfy-com/agro/assets/83612717/3efd18c8-c2d4-4ef9-8705-10d6b4bcb3d1">

---

Set 1337 port (Api runs on this port)
And you might want to increase memory (I tested it with 2 gigs and I think it is optimal)

<img width="535" alt="Screenshot 2024-06-14 at 16 12 46" src="https://github.com/Coderfy-com/agro/assets/83612717/8ad864bf-4b01-411d-8df6-10fcedd2d3df">

---

Click 'Create' button and wait a little bit.
At the end should get a url to your deploy

Login as Admin and check that all endpoints are publicly awailable

<img width="1717" alt="Screenshot 2024-06-14 at 16 18 30" src="https://github.com/Coderfy-com/agro/assets/83612717/c6c5a83c-1af6-48ee-b594-1ba2aa8d0984">

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
  
<img width="1700" alt="Screenshot 2024-06-14 at 17 42 56" src="https://github.com/Coderfy-com/agro/assets/83612717/c3fb77fe-88ec-44c4-99a8-3bd370a27609">

---

<img width="1208" alt="Screenshot 2024-06-14 at 17 45 12" src="https://github.com/Coderfy-com/agro/assets/83612717/a448cb88-b4a0-448d-9d3b-17e9bcd15574">

---
Copy your token

<img width="1194" alt="Screenshot 2024-06-14 at 17 45 35" src="https://github.com/Coderfy-com/agro/assets/83612717/553a3990-12bf-4668-82a9-d222fd29240d">

---

Use these commands to transfer data
For more detailed information read strapi docs

`npm run strapi transfer -- --to YOUR_DOMAIN/admin`

`npm run strapi transfer -- --from YOUR_DOMAIN/admin`

After you deploy api you need to change domain in the app





