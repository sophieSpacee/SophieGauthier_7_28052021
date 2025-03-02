# Groupomania - Projet 7 of Web Developper course with OpenClassrooms

## Project Goals 

This project is the last project of my course to become a full stack developer. The goal was to create from scratch a social media for a company. //
To code this project, I used ReactJS, Sass and Bootstrap for my frontend and NodeJS, Express, MySQL and Sequelize for my backend. //
//
I was not provided any specifications or mock up, I just had to develop a social media with a feature that allowed people to share images and gifs (like 9GAG). I worked on a mockup using Figma, tested my APIs using Postman and learned to use ReactJS to develop my application. 


## Project walkthrough

For this project, I created a signup page as well as a login page. //
I encrypted email in base64 and I hashed password with bcrypt before sending user information into the database. 

![Signup](/app/images/signup.png)

* Once connected, a user can post a gif or an image, like gifs others posted or comment them. 
* A user can decide to delete a post he made, of course he cannot delete another person's post. Once a post is deleted, the image is automatically deleted from the database to avoid useless space loss. 
* Image/Gif size is limited so that it does not affect website's performances. 
* A user can only like an image once, he can also stop liking it. 

![Feed](/app/images/feed.png)

* A user can choose to change his profile information on the user page. 
* He can also delete his profile. 
* A user can logout from the application. 

![User](/app/images/user.png)

I used AdminBro to have a control panel of my database. From there, the website administrator can: 
* delete or modify a post,
* view, delete or modigy a comment,
* delete a user 

![admin-dash](/app/images/admin-dash.png)

Of course, AdminBro's access is secure, the website administrator will need to set up an email and password to connect to the admin panel. 

![admin-log](/app/images/admin-log.png)


## Launch Groupomania application

1. From your terminal, clone this repository :
   `git clone https://github.com/sophieSpacee/SophieGauthier_7_28052021.git`
2. With your terminal, go to Front folder
   `cd SophieGauthier_7_28052021/` and then `cd Front/`
3. Type `git submodule update --init`to clone the frontend repository
4. Type `npm install` or `sudo npm install`
5. Type `npm start`
   <br/>
   You now have the front end up and running, now for the backend :
   <br/>

6. In a new terminal window, Go to SophieGauthier_7_280521 folder
7. Type `npm install` or `sudo npm install`
8. Install nodemon, `npm install nodemon`
9. Close this terminal window, you will not need it anymore
   <br/>

You are almost ready, now we need to set up the database
<br/>

11. In a third terminal, install Mysql (if you don't already have it installed), you can use this link https://dev.mysql.com/downloads/mysql/#downloads
12. Type `mysql`and choose a username and password `mysql --host=localhost --user=root --password=motdepassetopsecret`
13. Connect to mysql `mysql -h localhost -u root -p`
14. Create a new Database called Groupomania `CREATE DATABASE groupomania;`
15. Type `USE groupomania;`
16. In your editor, in the root of Sophie_Gauthier_7_280521, create a .env file <br/>

Follow this model : <br/>
DB_User="root"<br/>
DB_Password="your mysql root password"<br/>
DB_AdminEmail="admin@groupomania.com"<br/>
DB_AdminPassword="groupomania"<br/>

DB_User and DB_Password allow your application to connect to your local database, do not forget to change your username and password <br/>
DB_AdminEmail and DB_AdminPassword will allow you to access the admin panel at this address : http://localhost:3001/admin/

17. Save your .env file
18. Open a terminal in your editor and Type `nodemon server.js`

Your application is now running on http://localhost:3000


## Create User

POST `/api/users`

| Parameters | Type |                               Conditions |
| ---------- | :--: | ---------------------------------------: |
| email      | body | email must be valid and unique, required |
| password   | body |               6 min characters, required |
| first_name | body |                                 required |
| last_name  | body |                                 required |

---

| Error Code       |              Description               |
| ---------------- | :------------------------------------: |
| MISSINGFIELDS    |        all fields are required         |
| EMAILNOTUNIQUE   |          email must be unique          |
| PASSWORDTOOSHORT | password must be at least 6 characters |
| EMAILNOTVALID    |          email must be valid           |

## Login

POST `/api/users/login`

| Parameters | Type | Conditions |
| ---------- | :--: | ---------: |
| email      | body |   required |
| password   | body |   required |

---

| Error Code  | Description  |
| ----------- | :----------: |
| LOGINFAILED | login failed |

## Modify User

PUT `/api/users/:id`

| Parameters    |  Type  | Conditions |
| ------------- | :----: | ---------: |
| first_name    |  body  |   optional |
| last_name     |  body  |   optional |
| id            |  path  |   required |
| authorization | header |   required |

---

| Error Code   |  Description  |
| ------------ | :-----------: |
| UPDATEFAILED | update failed |

## Create Gif

POST `/api/gifs`

| Parameters | Type | Conditions |
| ---------- | :--: | ---------: |
| title      | body |   required |
| image      | file |   required |

---

| Error Code    |                  Description                  |
| ------------- | :-------------------------------------------: |
| MISSINGFIELDS |            all fields are required            |
| WRONGFORMAT   | Wrong image format, must be in jpg, jpeg, png |

## Get all Gifs

GET `/api/gifs`

| Parameters | Type  | Conditions |
| ---------- | :---: | ---------: |
| page       | query |   required |

## Delete Gif

DELETE `/api/gifs/:id`

| Parameters |  Type  | Conditions |
| ---------- | :----: | ---------: |
| id         | params |   required |

## Create Comment

POST `/api/comments`

| Parameters | Type | Conditions |
| ---------- | :--: | ---------: |
| content    | body |   required |

---

| Error Code   |                  Description                  |
| ------------ | :-------------------------------------------: |
| EMPTYCONTENT |            all fields are required            |
| WRONGFORMAT  | Wrong image format, must be in jpg, jpeg, png |
