


Ruby on Rails - Controller
Advertisements
 Previous Page Next Page  
The Rails controller is the logical center of your application. It coordinates the interaction between the user, the views, and the model. The controller is also a home to a number of important ancillary services.

It is responsible for routing external requests to internal actions. It handles people-friendly URLs extremely well.

It manages caching, which can give applications orders-of-magnitude performance boosts.

It manages helper modules, which extend the capabilities of the view templates without bulking up their code.

It manages sessions, giving users the impression of an ongoing interaction with our applications.

The process for creating a controller is very easy, and it's similar to the process we've already used for creating a model. We will create just one controller here −

library\> rails generate controller Book
Notice that you are capitalizing Book and using the singular form. This is a Rails paradigm that you should follow each time you create a controller.

This command accomplishes several tasks, of which the following are relevant here −

It creates a file called app/controllers/book_controller.rb

If you look at book_controller.rb, you will find it as follows −

class BookController < ApplicationController
end
Controller classes inherit from ApplicationController, which is the other file in the controllers folder: application.rb.

The ApplicationController contains code that can be run in all your controllers and it inherits from Rails ActionController::Base class.

You don't need to worry with the ApplicationController as of yet, so let's just define a few method stubs in book_controller.rb. Based on your requirement, you could define any number of functions in this file.

Modify the file to look like the following and save your changes. Note that it is upto you what name you want to give to these methods, but better to give relevant names.

class BookController < ApplicationController
   def list
   end
   
   def show
   end
   
   def new
   end
   
   def create
   end
   
   def edit
   end
   
   def update
   end
   
   def delete
   end
   
end
Now let us implement all the methods one by one.

Implementing the list Method
The list method gives you a list of all the books in the database. This functionality will be achieved by the following lines of code. Edit the following lines in book_controller.rb file.

def list
   @books = Book.all
end
The @books = Book.all line in the list method tells Rails to search the books table and store each row it finds in the @books instance object.

Implementing the show Method
The show method displays only further details on a single book. This functionality will be achieved by the following lines of code.

def show
   @book = Book.find(params[:id])
end
The show method's @book = Book.find(params[:id]) line tells Rails to find only the book that has the id defined in params[:id].

The params object is a container that enables you to pass values between method calls. For example, when you're on the page called by the list method, you can click a link for a specific book, and it passes the id of that book via the params object so that show can find the specific book.

Implementing the new Method
The new method lets Rails know that you will create a new object. So just add the following code in this method.

def new
   @book = Book.new
   @subjects = Subject.all
end
The above method will be called when you will display a page to the user to take user input. Here second line grabs all the subjects from the database and puts them in an array called @subjects.

Implementing the create Method
Once you take user input using HTML form, it is time to create a record into the database. To achieve this, edit the create method in the book_controller.rb to match the following −

def create
   @book = Book.new(book_params)
	
   if @book.save
      redirect_to :action => 'list'
   else
      @subjects = Subject.all
      render :action => 'new'
   end
   
end

def book_params
   params.require(:books).permit(:title, :price, :subject_id, :description)
end
The first line creates a new instance variable called @book that holds a Book object built from the data, the user submitted. The book_params method is used to collect all the fields from object :books. The data was passed from the new method to create using the params object.

The next line is a conditional statement that redirects the user to the list method if the object saves correctly to the database. If it doesn't save, the user is sent back to the new method. The redirect_to method is similar to performing a meta refresh on a web page: it automatically forwards you to your destination without any user interaction.

Then @subjects = Subject.all is required in case it does not save data successfully and it becomes similar case as with new option.

Implementing the edit Method
The edit method looks nearly identical to the show method. Both methods are used to retrieve a single object based on its id and display it on a page. The only difference is that the show method is not editable.

def edit
   @book = Book.find(params[:id])
   @subjects = Subject.all
end
This method will be called to display data on the screen to be modified by the user. The second line grabs all the subjects from the database and puts them in an array called @subjects.

Implementing the update Method
This method will be called after the edit method, when the user modifies a data and wants to update the changes into the database. The update method is similar to the create method and will be used to update existing books in the database.

def update
   @book = Book.find(params[:id])
	
   if @book.update_attributes(book_param)
      redirect_to :action => 'show', :id => @book
   else
      @subjects = Subject.all
      render :action => 'edit'
   end
   
end

def book_param
   params.require(:book).permit(:title, :price, :subject_id, :description)
end
The update_attributes method is similar to the save method used by create but instead of creating a new row in the database, it overwrites the attributes of the existing row.

Then @subjects = Subject.all line is required in case it does not save the data successfully, then it becomes similar to edit option.

Implementing the delete Method
If you want to delete a record from the database then you will use this method. Implement this method as follows.

def delete
   Book.find(params[:id]).destroy
   redirect_to :action => 'list'
end
The first line finds the classified based on the parameter passed via the params object and then deletes it using the destroy method. The second line redirects the user to the list method using a redirect_to call.

Additional Methods to Display Subjects
Assume you want to give a facility to your users to browse all the books based on a given subject. So, you can create a method inside book_controller.rb to display all the subjects. Assume the method name is show_subjects −

def show_subjects
   @subject = Subject.find(params[:id])
end
Finally your book_controller.rb file will look as follows −

class BooksController < ApplicationController

   def list
      @books = Book.all
   end

   def show
      @book = Book.find(params[:id])
   end
  
   def new
      @book = Book.new
      @subjects = Subject.all
   end

   def book_params
      params.require(:books).permit(:title, :price, :subject_id, :description)
   end

   def create
      @book = Book.new(book_params)

      if @book.save
         redirect_to :action => 'list'
      else
         @subjects = Subject.all
         render :action => 'new'
      end
   end
   
   def edit
      @book = Book.find(params[:id])
      @subjects = Subject.all
   end
   
   def book_param
      params.require(:book).permit(:title, :price, :subject_id, :description)
   end
   
   def update
      @book = Book.find(params[:id])
      
      if @book.update_attributes(book_param)
         redirect_to :action => 'show', :id => @book
      else
         @subjects = Subject.all
         render :action => 'edit'
      end
   end
   
   def delete
      Book.find(params[:id]).destroy
      redirect_to :action => 'list'
   end
   
   def show_subjects
      @subject = Subject.find(params[:id])
   end

end
Now save your controller file.

What is Next?
You have created almost all the methods, which will work on backend. Next we will define routes (URLs) for actions.
