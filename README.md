# Alfarroba
A complete hackathon tool!

Alfarroba is a hackathon management system designed to integrate most hackathon operations, both on the admin as on the participant side. It serves as an event management tool on the admin side and a working tool on the participant side. It builds on Quill, HackMIT's registration system designed especially for hackathons. For hackers, it’s a clean and streamlined interface to use, from registration to team formation, project tracking, project feedback receipt and having access to all event resources. For hackathon organizers, it’s an easy way to centralize operations by being able to manage registrations, view stats, reimburse expenses and more!

![Login Splash](./docs/images/screenshots/login.png)

# Features
## Alfarroba for Users
### Dashboard
![Dashboard](./docs/images/screenshots/dashboard.png)

After users login, the Dashboard displays the user’s application status and status-specific prompts to resend a verification email, view/edit their application or confirmation forms.

Statuses:
- Unverified: users have not verified the email address they registered with
- Incomplete, registration open: the user has not submitted their application, but the registration deadline has not passed
- Incomplete, registration closed: the user has not submitted, but the registration deadline has passed
- Submitted, registration open
- Submitted, registration closed
- Admitted / unconfirmed: the user has been admitted to the event, but has not confirmed their attendance and submitted their confirmation form
- Admitted / confirmation deadline passed: the user has been admitted, but did not confirm their attendance before the deadline
- Waitlisted: the user was not admitted to the event
- Confirmed: the user has been admitted and has confirmed their attendance
- User declined admission: the user has been admitted, but will not be attending the event

### Application
![Application](./docs/images/screenshots/application.png)

The Application tab takes users to their registration or confirmation form. 

### Team Registration
Hackathons commonly allow participants to register and be admitted as a team. The Team tab allows users to create or join a team with other users.

## Alfarroba for Admins
Admins can view stats, look through applications, or edit settings from the Admin panel.

### Stats
![Stats](./docs/images/screenshots/stats.png) 

The Stats tab summarizes useful registration statistics on the number of users in each stage of the process, demographic information, and miscellaneous event preferences like shirt sizes, dietary restrictions, or reimbursement requests.

### Users Table
![Users table](./docs/images/screenshots/admin-users.png)

The Users tab displays a table of users where admins can:
1. Search for a user by name
2. Quick-view user applications in a pop-up modal
3. See a user’s application status (verified, submitted, admitted, and confirmed) at-a-glance
4. See responses to other miscellaneous fields on the application
5. Open and edit an individual application
6. Admit users manually
7.  Mark users as checked-in at the event day-of

### Settings 
![Settings](./docs/images/screenshots/settings.png)

On the Settings tab, admins can easily control their event application timeline by setting registration / confirmation deadlines. They can also write custom waitlist, acceptance, and confirmation copy that users will see on their dashboard throughout the application process. The custom copy is interpreted as Markdown, so HTML and images can be added.

# Setup
### Quick deploy with Heroku
[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy)

### Deploying locally
Getting a local instance of Quill up and running takes less than 5 minutes! Start by setting up the database. Ideally, you should run MongoDB as a daemon with a secure configuration (with most linux distributions, you should be able to install it with your package manager, and it'll be set up as a daemon). Although not recommended for production, when running locally for development, you could do it like this

#### If you have docker-compose, this is the super quick way
```
docker-compose up
```
And the app will be waiting for you at http://localhost:3000/

In case you'r interested in docker-compose, here is the quick and clean [install guide](https://docs.docker.com/compose/install/#install-as-a-container)

#### The Database

You can either install `mongod` locally or use `docker` or something else, as long as you have mongo up and running somewhere!

Using mongod installed locally:
```
mkdir db
mongod --dbpath db --bind_ip 127.0.0.1 --nohttpinterface
```

**OR**

Using docker:

```
docker pull mvertes/alpine-mongo
```
and run it like so, remember to specify the absolute path of the repo:

```
docker run -d --name mongo -p 27017:27017 -v {absolute path to repo}/db:/data/db mvertes/alpine-mongo
```

#### Install the necessary dependencies

You must have `npm`, `bower` and `gulp` installed on your system.
There's no spcified node version but it works on version 9+ so that's what we recommend!

You can install npm using your package manager, or `nvm` or whatever you prefer. Installing `bower` and `gulp` is pretty straigth forward:
`npm install -g bower` and `npm install -g gulp`. Or if your `npm` is installed using root, run the commands with `sudo`.

Now, once that's done, install the system using the following lines:

```
npm install
bower install
npm run config
```

Edit the configuration file in `.env` for your setup.
If your mongo is not on localhost and not on port 27017, you want to edit this file.

#### Run the application
```
gulp server
```

# Customizing for your event

###### _If you're using Quill for your event, please add yourself to this [list][users]. It takes less than a minute, but knowing that our software is helping real events keeps us going ♥_ 
### Copy
If you’d like to customize the text that users see on their dashboards, edit them at `client/src/constants.js`.

### Branding / Assets
Customize the color scheme and hosted assets by editing `client/stylesheets/_custom.scss`. Don’t forget to use your own email banner, favicon, and logo (color/white) in the `assets/images/` folder as well! 

### Application questions
If you want to change the application questions, edit:
- `client/views/application/`
- `server/models/User.js`
- `client/views/admin/user/` and `client/views/admin/users/` to render the updated form properly in the admin view

If you want stats for your new fields:
- Recalculate them in `server/services/stats.js`
- Display them on the admin panel by editing `client/views/admin/stats/` 

### Email Templates
To customize the verification and confirmation emails for your event, put your new email templates in `server/templates/` and edit `server/services/email.js`

# Contributing
Contributions to Quill are welcome and appreciated! Please take a look at [`CONTRIBUTING.md`][contribute] first.

# Feedback / Questions
If you have any questions about this software, please contact [quill@hackmit.org][email].

# License
Copyright (c) 2015-2016 Edwin Zhang (https://github.com/ehzhang). Released under AGPLv3. See [`LICENSE.txt`][license] for details.

[contribute]: https://github.com/techx/quill/blob/master/CONTRIBUTING.md
[license]: https://github.com/techx/quill/blob/master/LICENSE.txt
[email]: mailto:quill@hackmit.org
[users]: https://github.com/techx/quill/wiki/Quill-Users
