#Wordpress for Dokku

This repository exists as a starting point from which to create Wordpress websites within Git which can then be easily deployed to Dokku or Heroku.

This repository is heavily inspired on two very good guides:

- https://davidwinter.me/install-and-manage-wordpress-with-git/
- http://shincoding.com/docker/tutorial-deploying-wordpress-with-dokku/

The first being on developing Wordpress on Git and, the second being on deploying Wordpress on Dokku. Both of which I recommend reading before continuing with this repository.

###Getting Started
Wordpress is included as a sub-repository. This allows us to separate it from our Git repository so we don't have to carry around all the files. Dokku will automatically fetch the sub-repository for us when deploying which makes life easier.

####Running Locally
If you wish to run Wordpress locally before deploying to Dokku then you can download the submodule by running:

    git submodule update --init

Because Wordpress is loaded from a sub-repository we have to add our files in from outside of that directory, this is fine as Wordpress natively supports loading the wp-config.php from one directory above the installation.

####Setting up wp-config.php
You'll notice that a range of things have changed in our wp-config.php including the definition of the wp-content folder location. This allows us to notify Wordpress of our own wp-content folder.

You'll want to make sure you replace `$_SERVER['SERVER_NAME']` with the domain of your website where Wordpress will be running, as setting these settings through the `$_SERVER[]` property is not typically advised as best practice.

We also enter the database information through environment variables, this is the way our Dokku installation passes this information to our applications, but you can also define these in Apache for running locally. Preventing the hassle of ensuring you don't pass database credentials through Git.

As an example, you can do this by adding the following to your server configuration files.

    SetEnv DB_HOST thehost
    SetEnv DB_NAME thedbname
    SetEnv DB_PASSWORD thedbpassword
    SetEnv DB_PORT thedbport
    SetEnv DB_USER thedbuser

In MAMP Pro this can be done by inserting this under `Additional parameters for <VirtualHost>`
