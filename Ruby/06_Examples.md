

Ruby on Rails - Examples
Advertisements
 Previous Page Next Page  
In this chapter, we will create a simple but operational online library system for holding and managing the books.

This application has a basic architecture and will be built using two ActiveRecord models to describe the types of data that is stored −

Books, which describes an actual listing.
Subject, which is used to group books together.
Workflow for Creating Rails Applications
A recommended work flow for creating Rails Application is as follows −

Use the rails command to create the basic skeleton of the application.

Create a database on the PostgreSQL server to hold your data.

Configure the application to know where your database is located and the login credentials for it.

Create Rails Active Records (Models), because they are the business objects you'll be working with in your controllers.

Generate Migrations that simplify the creating and maintaining of database tables and columns.

Write Controller Code to put a life in your application.

Create Views to present your data through User Interface.

So, let us start with creating our library application.

Creating an Empty Rails Web Application
Rails is both a runtime web application framework and a set of helper scripts that automate many of the things you do when developing a web application. In this step, we will use one such helper script to create the entire directory structure and the initial set of files to start our Library System application.

Go into ruby installation directory to create your application.

Run the following command to create a skeleton for library application. It will create the directory structure in the current directory.

tp> rails new library
This will create a subdirectory for the library application containing a complete directory tree of folders and files for an empty Rails application. Check a complete directory structure of the application. Check Rails Directory Structure for more detail.

Most of our development work will be creating and editing files in the library/app subdirectories. Here's a quick run down of how to use them −

The controllers subdirectory is where Rails looks to find controller classes. A controller handles a web request from the user.

The views subdirectory holds the display templates to fill in with data from our application, convert to HTML, and return to the user's browser.

The models subdirectory holds the classes that model and wrap the data stored in our application's database. In most frameworks, this part of the application can grow pretty messy, tedious, verbose, and error-prone. Rails makes it dead simple.

The helpers subdirectory holds any helper classes used to assist the model, view, and controller classes. This helps to keep the model, view, and controller code small, focused, and uncluttered.

Starting Web Server
Rails web application can run under virtually any web server, but the most convenient way to develop a Rails web application is to use the built-in WEBrick web server. Let's start this web server and then browse to our empty library application −

This server will be started from the application directory as follows. It runs on port number 3000.

tp> cd ruby\library 
tp\ruby\library\> Rails server
It generates the auto code to start the server as shown below −

Rails Server
This will start your WEBrick web server.

Now open your browser and browse to http://127.0.0.1:3000. If everything is gone fine, then you should see a greeting message from WEBrick, otherwise there is something wrong with your setting. If everything goes well it will generate the output as follows.

Web Server
What is next?
The next chapter explains how to create databases for your application and what is the configuration required to access these created databases.

Further, we will see what Rails Migration is and how it is used to maintain database tables.
