## Strapi Application

### Headless CMS used as Backend for digital-camera-store application

### Database

* Create free database in Cloud Mongo (MongoDB Atlas)


### Strapi Installation - Using v3.6.8
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

The variable values ​​for Cloudinary are obtained from the Cloudinary interface.

**#Database - Mongo**
* DATABASE_HOST=s3cr3t
* DATABASE_SRV=true
* DATABASE_PORT=27017
* DATABASE_NAME=s3cr3t
* DATABASE_USERNAME=s3cr3t
* DATABASE_PASSWORD=s3cr3t
* AUTHENTICATION_DATABASE=s3cr3t
* DATABASE_SSL=true

Values for MongoDB connection were introduced in the application creation process (steps above), and were stored in the `.\config\database.js` file. As an extra step, I removed them from there and put them in the `.env` file.



## DEPLOY Strapi Application in HEROKU





