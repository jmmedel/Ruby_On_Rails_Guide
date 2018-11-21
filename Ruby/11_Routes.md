

Ruby on Rails - Routes
Advertisements
 Previous Page Next Page  
The routing module provides URL rewriting in native Ruby. It's a way to redirect incoming requests to controllers and actions. It replaces the mod_rewrite rules. Best of all, Rails' Routing works with any web server. Routes are defined in app/config/routes.rb.

Think of creating routes as drawing a map for your requests. The map tells them where to go based on some predefined pattern −

Rails.application.routes.draw do
   Pattern 1 tells some request to go to one place
   Pattern 2 tell them to go to another
   ...
end
Example
Let us consider our library management application contains a controller called BookController. We have to define the routes for those actions which are defined as methods in the BookController class.

Open routes.rb file in library/config/ directory and edit it with the following content.

Rails.application.routes.draw do
   get 'book/list'
   get 'book/new'
   post 'book/create'
   patch 'book/update'
   get 'book/list'
   get 'book/show'
   get 'book/edit'
   get 'book/delete'
   get 'book/update'
   get 'book/show_subjects'
end
The routes.rb file defines the actions available in the applications and the type of action such as get, post, and patch.

Use the following command to list all your defined routes, which are useful for tracking down routing problems in your application, or giving you a good overview of the URLs in an application you're trying to get familiar with.

library> rake routes
What is Next?
Next, we will create the code to generate screens to display data and to take input from the user.
