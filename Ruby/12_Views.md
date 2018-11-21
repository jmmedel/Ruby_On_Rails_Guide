

Ruby on Rails - Views
Advertisements
 Previous Page Next Page  
A Rails View is an ERb program that shares data with controllers through mutually accessible variables.

If you look in the app/views directory of the library application, you will see one subdirectory for each of the controllers, we have created: book. Each of these subdirectories was created automatically when the same-named controller was created with the generate script.

Rails let's you know that you need to create the view file for each new method. Each method you define in the controller needs to have a corresponding erb file, with the same name as the method, to display the data that the method is collecting.

So let's create view files for all the methods we have defined in the book_controller.rb. While executing these views, simultaneously check these actions are applicable into the database or not.

Creating View File for list Method
Create a file called list.html.erb using your favourite text editor and save it to app/views/book. After creating and saving the file, refresh your web browser. You should see a blank page; if you don't, check the spelling of your file and make sure that it is exactly the same as your controller's method.

Now, display the actual content. Let us put the following code into list.html.erb.

<% if @books.blank? %>
<p>There are not any books currently in the system.</p>
<% else %>
<p>These are the current books in our system</p>

<ul id = "books">
   <% @books.each do |c| %>
   <li><%= link_to c.title, {:action => 'show', :id => c.id} -%></li>
   <% end %>
</ul>

<% end %>
<p><%= link_to "Add new Book", {:action => 'new' }%></p>
The code to be executed is to check whether the @books array has any objects in it. The .blank? method returns true if the array is empty, and false if it contains any objects. This @books object was created in controller inside the list method.

The code between the <%= %> tags is a link_to method call. The first parameter of link_to is the text to be displayed between the <a> tags. The second parameter is what action is called when the link is clicked. In this case, it is the show method. The final parameter is the id of the book that is passed via the params object.

Now, try refreshing your browser and you should get the following screen because we don't have any book in our library.

No Book Message
Creating View File for new Method
Till now, we don't have any book in our library. We have to create few books in the system. So, let us design a view corresponding to the new method defined in the book_controller.rb.

Create a file called new.html.erb using your favorite text editor and save it to app/views/book. Add the following code to the new.html.erb file.

<h1>Add new book</h1>

<%= form_tag :action => 'create' do %>
<p><label for = "book_title">Title</label>:

<%= text_field 'books', 'title' %></p>
<p><label for = "book_price">Price</label>:

<%= text_field 'books', 'price' %></p>
<p><label for = "book_subject_id">Subject</label>:

<%= collection_select(:books, :subject_id, @subjects, :id, :name, prompt: true) %></p>
<p><label for = "book_description">Description</label><br/>

<%= text_area 'books', 'description' %></p>
<%= submit_tag "Create" %>

<% end -%>
<%= link_to 'Back', {:action => 'list'} %>
Here form_tag method interprets the Ruby code into a regular HTML <form> tag using all the information supplied to it. This tag, for example, outputs the following HTML −

<form action = "/book/create" method = "post">
Next method is text_field that outputs an <input> text field. The parameters for text_field are object and field name. In this case, the object is book and the name is title.

Rails method called collection_select, creates an HTML select menu built from an array, such as the @books one. There are five parameters, which are as follows −

:book − The object you are manipulating. In this case, it's a book object.

:subject_id − The field that is populated when the book is saved.

@books − The array you are working with.

:id − The value that is stored in the database. In terms of HTML, this is the <option> tag's value parameter.

:name − The output that the user sees in the pull-down menu. This is the value between the <option> tags.

The next used is submit_tag, which outputs an <input> button that submits the form. Finally, there is the end method that simply translates into </form>.

Go to your browser and visit http://localhost:3000/book/new. This will give you the following screen.

New Book
Enter some data in this form and then click the Create button. Here i have added the following details into the fields −

Title: Advance Physics
Price: 390
Subject: Physics
Description: This is test to create new book
When you click the Create button, it will call the create method, which does not need any view because this method is using either list or new methods to view the results. So, when you click the Create button, the data should submit successfully and redirect you to the list page, in which you now have a single item listed as follows −

Create Book
If you click the link, you should see another Template is missing error, since you haven't created the template file for show method yet.

Creating View File for show Method
This method will display the complete detail about any book available in the library. Create a show.html.erb file under app/views/book and populate it with the following code −

<h1><%= @book.title %></h1>

<p>
   <strong>Price: </strong> $<%= @book.price %><br />
   <strong>Subject :</strong> <%= @book.subject.name %><br />
   <strong>Created Date:</strong> <%= @book.created_at %><br />
</p>

<p><%= @book.description %></p>

<hr />

<%= link_to 'Back', {:action => 'list'} %>
This is the first time you have taken the full advantage of associations, which enable you to easily pull data from related objects.

The format used is @variable.relatedObject.column. In this instance, you can pull the subject's name value through the @book variable using the belongs_to associations. If click on any listed record then it will show you the following screen.

Show Book
Creating View File for edit Method
Create a new file called edit.html.erb and save it in app/views/book. Populate it with the following code −

<h1>Edit Book Detail</h1>

<%= form_for @book, :url =>{:action => "update", :id =>@book} do |f| %>

<p>Title: <%= f.text_field 'title' %></p>
<p>Price: <%= f.text_field  'price' %></p>
<p>Subject: <%= f.collection_select :subject_id, Subject.all, :id, :name %></p>
<p>Description<br/>

<%= f.text_area 'description' %></p>
<%= f.submit "Save changes" %>
<% end %>

<%= link_to 'Back', {:action => 'list' } %>
This code is very similar to the new method except action to be updated instead of creating and defining an id.

In this scenario, we used form_for tag for the form action. It will perform better than form_tag. Why because it will create interaction with the Model easily. Therefore it is better to use form_for tag whenever you need interaction between the model and the form fields.

At this point, we need some modification in the list method's view file. Go to the <li></li> element and modify it to look like the following −

<li>
   <%= link_to c.title, {:action => "show", :id => c.id} -%>
   <b> <%= link_to 'Edit', {:action => "edit",
   :id => c.id} %></b>
</li>
Now, try to browse books using the http://localhost:3000/book/list. It will give you the listing of all the books along with Edit option. When you click the Edit option, then you will have next screen as follows −

Edit Book
Now, you edit this information and then click the Save Changes button. This will result in a call to update method available in the controller file and it will update all the changed attribute. Notice that the update method does not need any view file because it's using either show or edit methods to show its results.

Creating View File for delete Method
Removing information from a database using Ruby on Rails is almost too easy. You do not need to write any view code for the delete method because this method is using list method to display the result. So, let's just modify list.html.erb again and add a delete link.

Go to the <li></li> element and modify it to look like the following −

<li>
   <%= link_to c.title, {:action => 'show', :id => c.id} -%>
   <b> <%= link_to 'Edit', {:action => 'edit', :id => c.id} %></b>
   <b> <%= link_to "Delete", {:action => 'delete', :id => c.id},
      :confirm => "Are you sure you want to delete this item?" %></b>
</li>
The :confirm parameter presents a JavaScript confirmation box asking if you really want to perform the action. If the user clicks OK, the action proceeds, and the item is deleted.

Now, try browsing books using http://localhost:3000/book/list. It will give you listing of all the books along with Edit and Delete options as follows −

Delete Book
Now using the Delete option, you can delete any listed record.

Creating View File for show_subjects Method
Create a new file, show_subjects.html.erb, in the app/views/book directory and add the following code to it −

<h1><%= @subject.name -%></h1>

<ul>
   <% @subject.books.each do |c| %>
   <li><%= link_to c.title, :action => "show", :id => c.id -%></li>
   <% end %>
</ul>
You are taking advantage of associations by iterating through a single subject's many books listings.

Now modify the Subject: line of show.html.erb so that the subject listing shows a link.

<strong>Subject: </strong> <%= link_to @book.subject.name,
:action => "show_subjects", :id => @book.subject.id %><br />
This will output a list of subject on the index page, so that users can access them directly.

Modify list.html.erb to add the following to the top of the file −

<ul id = "subjects">
   <% Subject.find(:all).each do |c| %>
   <li><%= link_to c.name, :action => "show_subjects", :id => c.id %></li>
   <% end %>
</ul>
Now try browsing books using http://localhost:3000/book/list. It will display all subjects with links so that you can browse all the books related to that subject.

List Subjects
What is Next?
Hope now you are feeling comfortable with all the operations of Rails.

The next chapter explains how to use Layouts to put your data in a better way. We will show you how to use CSS in your Rails applications.
