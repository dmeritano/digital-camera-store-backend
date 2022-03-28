## Strapi Application (Headless CMS)

### Used as Backend for digital-camera-store application

### Database

* Create free database in Cloud Mongo (MongoDB Atlas)


### Strapi Installation - Using v3.6.8  (Community Edition)

**Node version:** 16.14.2 (required by strapi 3.6.8). 
I had to install this version on my machine and the `nvm` (Node Version Manager) utility to select the required Node version in order to create de strapi application.

<u>Steps</u>

* `npx create-strapi-app@3.6.8`
* Set proyect name (folder)
* Select Custom Installation
* Discard using template option (Select N)
* Choose database
    * `mongo`
    * Mongo settings like host, user, pass, etc should be taken from the previous step, when the DB was created in Mongo Cloud.
        

* `npm run develop` to start server


### Images on Cloudinary
Configured plugin to store images in Cloudinary instead of a local application directory. Created `plugins.js` in `./config/` folder. File content:

```javascript
module.exports = ({ env }) => ({
    upload: {
      provider: 'cloudinary',
      providerOptions: {
        cloud_name: env('CLOUDINARY_NAME'),
        api_key: env('CLOUDINARY_KEY'),
        api_secret: env('CLOUDINARY_SECRET'),
      },
      actionOptions: {
        upload: {},
        delete: {},
      },
    },
  });
```

### Environments Variables  (.env)

**#Cloudinary**
* CLOUDINARY_NAME=s3cr3t
* CLOUDINARY_KEY=s3cr3t
* CLOUDINARY_SECRET=s3cr3t

> The values ​​of the precedent variables were obtained from the Cloudinary web interface.

**#Database - Mongo**
* DATABASE_HOST=s3cr3t
* DATABASE_SRV=true
* DATABASE_PORT=27017
* DATABASE_NAME=s3cr3t
* DATABASE_USERNAME=s3cr3t
* DATABASE_PASSWORD=s3cr3t
* AUTHENTICATION_DATABASE=s3cr3t
* DATABASE_SSL=true

> Values for MongoDB connection were introduced in the application creation process (steps above), and were stored in the `.\config\database.js` file. As an extra step, I removed them from there and put them in the `.env` file.

**#Other - Strapi API**
ADMIN_JWT_SECRET=s3cr3t

> Move this variable value from `.\config\server.js` to `.env` file


## Deploying Strapi Application on HEROKU

We are going to use some of CI/CD techniques

First, we create repository on GitHub

Second, we move to the project folder and do the following:

```bash
  $ git init
  $ git add README.md
  $ git commit -m "Commiting for automating deploying in Heroku"
  $ git branch -M main
  $ git remote add origin git@github.com:user/project-name.git
  $ git push -u origin main
```

If we do not have a Heroku account, we proceed to create it

If we haven't done so already, install **Heroku CLI**. In my case (Linux Ubuntu) I installed the utility like this::

```bash
  $ sudo snap install --classic heroku
```

In the project folder we do the following:

```bash 
  $ heroku login
```
> This opens the default browser and makes us log in to Heroku; immediately afterwards, we return to the terminal

```bash 
  $ heroku create
```
> This will create an application on Heroku, to which it will assign a random name

```bash 
  $ git push heroku main
```
> This will link our repository on GibHub to Heroku, so if we later have improvements to the app, we'll push them to GitHub as usual `git push origin main` , then running `git push heroku main` again will update our application in production.

> TIP: If we want to change the randomly generated name of our application in Heroku, we do not have to do it from the Dashboard(web interface), but with Heroku CLI:

```bash 
  $ heroku apps:rename new_name_of_application  
```


### Creating environment variables on Heroku

If we try to access the application deployed on Heroku we will see that it tells us "APPLICATION ERROR". 

We can see the logs from the Heroku web interface or from the console by running `heroku logs`. 

In this case we will see in logs that App it is not being able to connect to the Mongo DB, and that is because we have not yet added the environment variables for the application in Heroku. 

Therefore, from the Heroku web interface we enter (click) on the application and then we choose "Settings" (a top right) and locate the "Config Vars" section.  There we must add all our environment variables with the values ​​for production.

**After this we will be able to access the Strapi application/console on Heroku as we did locally on our computer**







