


Ruby on Rails - Introduction
Advertisements
 Previous Page Next Page  
What is Ruby?
Before we ride on Rails, let us recapitulate a few points of Ruby, which is the base of Rails.

Ruby is the successful combination of −

Smalltalk's conceptual elegance,
Python's ease of use and learning, and
Perl's pragmatism.
Ruby is −

A high-level programming language.
Interpreted like Perl, Python, Tcl/TK.
Object-oriented like Smalltalk, Eiffel, Ada, Java.
Why Ruby?
Ruby originated in Japan and now it is gaining popularity in US and Europe as well. The following factors contribute towards its popularity −

Easy to learn
Open source (very liberal license)
Rich libraries
Very easy to extend
Truly object-oriented
Less coding with fewer bugs
Helpful community
Although we have many reasons to use Ruby, there are a few drawbacks as well that you may have to consider before implementing Ruby −

Performance Issues − Although it rivals Perl and Python, it is still an interpreted language and we cannot compare it with high-level programming languages like C or C++.

Threading model − Ruby does not use native threads. Ruby threads are simulated in the VM rather than running as native OS threads.

Sample Ruby Code
Here is a sample Ruby code to print "Hello Ruby"

# The Hello Class
class Hello
   
   def initialize( name )
      @name = name.capitalize
   end

   def salute
      puts "Hello #{@name}!"
   end
   
end

# Create a new object
h = Hello.new("Ruby")

# Output "Hello Ruby!"
h.salute
Output − This will produce the following result −

Hello Ruby!
Embedded Ruby
Ruby provides a program called ERB (Embedded Ruby), written by Seki Masatoshi. ERB allows you to put Ruby codes inside an HTML file. ERB reads along, word for word, and then at a certain point, when it encounters a Ruby code embedded in the document, it starts executing the Ruby code.

You need to know only two things to prepare an ERB document −

If you want some Ruby code executed, enclose it between <% and %>.

If you want the result of the code execution to be printed out, as a part of the output, enclose the code between <%= and %>.

Here's an example. Save the code in erbdemo.rb file. Note that a Ruby file will have an extension .rb −

<% page_title = "Demonstration of ERB" %>
<% salutation = "Dear programmer," %>

<html>

   <head>
      <title><%= page_title %></title>
   </head>
	
   <body>
      <p><%= salutation %></p>
      <p>This is an example of how ERB fills out a template.</p>
   </body>
	
</html>
Now, run the program using the command-line utility erb.

tp> erb erbdemo.rb
This will produce the following result −

<html>

   <head>
      <title>Demonstration of ERb</title>
   </head>
	
   <body>
      <p>Dear programmer,</p>
      <p>This is an example  of how ERb fills out a template.</p>
   </body>
	
</html>
What is Rails?
An extremely productive web-application framework.

Written in Ruby by David Heinemeier Hansson.

You could develop a web application at least ten times faster with Rails than you could with a typical Java framework.

An open source Ruby framework for developing database-backed web applications.

Configure your code with Database Schema.

No compilation phase required.

Full Stack Framework
Includes everything needed to create a database-driven web application, using the Model-View-Controller pattern.

Being a full-stack framework means all the layers are built to work seamlessly together with less code.

Requires fewer lines of code than other frameworks.

Convention over Configuration
Rails shuns configuration files in favor of conventions, reflection, and dynamic runtime extensions.

Your application code and your running database already contain everything that Rails needs to know!

Rails Strengths
Rails is packed with features that make you more productive, with many of the following features building on one other.

Metaprogramming
Where other frameworks use extensive code generation from scratch, Rail framework uses Metaprogramming techniques to write programs. Ruby is one of the best languages for Metaprogramming, and Rails uses this capability well. Rails also uses code generation but relies much more on Metaprogramming for the heavy lifting.

Active Record
Rails introduces the Active Record framework, which saves objects into the database. The Rails version of the Active Record discovers the columns in a database schema and automatically attaches them to your domain objects using metaprogramming.

Convention over configuration
Most web development frameworks for .NET or Java force you to write pages of configuration code. If you follow the suggested naming conventions, Rails doesn't need much configuration.

Scaffolding
You often create temporary code in the early stages of development to help get an application up quickly and see how major components work together. Rails automatically creates much of the scaffolding you'll need.

Built-in testing
Rails creates simple automated tests you can then extend. Rails also provides supporting code called harnesses and fixtures that make test cases easier to write and run. Ruby can then execute all your automated tests with the rake utility.

Three environments
Rails gives you three default environments: development, testing, and production. Each behaves slightly differently, making your entire software development cycle easier. For example, Rails creates a fresh copy of the Test database for each test run.


