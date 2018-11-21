

Ruby on Rails - AJAX
Advertisements
 Previous Page Next Page  
Ajax stands for Asynchronous JavaScript and XML. Ajax is not a single technology; it is a suite of several technologies. Ajax incorporates the following −

XHTML for the markup of web pages
CSS for the styling
Dynamic display and interaction using the DOM
Data manipulation and interchange using XML
Data retrieval using XMLHttpRequest
JavaScript as the glue that meshes all this together
Ajax enables you to retrieve data for a web page without having to refresh the contents of the entire page. In the basic web architecture, the user clicks a link or submits a form. The form is submitted to the server, which then sends back a response. The response is then displayed for the user on a new page.

When you interact with an Ajax-powered web page, it loads an Ajax engine in the background. The engine is written in JavaScript and its responsibility is to both communicate with the web server and display the results to the user. When you submit data using an Ajax-powered form, the server returns an HTML fragment that contains the server's response and displays only the data that is new or changed as opposed to refreshing the entire page.

For a complete detail on AJAX you can go through our AJAX Tutorial

How Rails Implements Ajax
Rails has a simple, consistent model for how it implements Ajax operations. Once the browser has rendered and displayed the initial web page, different user actions cause it to display a new web page (like any traditional web application) or trigger an Ajax operation −

Some trigger fires − This trigger could be the user clicking on a button or link, the user making changes to the data on a form or in a field, or just a periodic trigger (based on a timer).

The web client calls the server − A JavaScript method, XMLHttpRequest, sends data associated with the trigger to an action handler on the server. The data might be the ID of a checkbox, the text in an entry field, or a whole form.

The server does processing − The server-side action handler ( Rails controller action )-- does something with the data and returns an HTML fragment to the web client.

The client receives the response − The client-side JavaScript, which Rails creates automatically, receives the HTML fragment and uses it to update a specified part of the current page's HTML, often the content of a <div> tag.

These steps are the simplest way to use Ajax in a Rails application, but with a little extra work, you can have the server return any kind of data in response to an Ajax request, and you can create custom JavaScript in the browser to perform more involved interactions.

AJAX Example
This example works based on scaffold, Destroy concept works based on ajax.

In this example, we will provide, list, show and create operations on ponies table. If you did not understand the scaffold technology then we would suggest you to go through the previous chapters first and then continue with AJAX on Rails.

Creating An Application
Let us start with the creation of an application It will be done as follows −

rails new ponies
The above command creates an application, now we need to call the app directory using with cd command. It will enter in to an application directory then we need to call a scaffold command. It will be done as follows −

rails generate scaffold Pony name:string profession:string
Above command generates the scaffold with name and profession column. We need to migrate the data base as follows command

rake db:migrate
Now Run the Rails application as follows command

rails s
Now open the web browser and call a url as http://localhost:3000/ponies/new, The output will be as follows

Ajax
Creating an Ajax
Now open app/views/ponies/index.html.erb with suitable text editors. Update your destroy line with :remote => true, :class => 'delete_pony'.At finally, it looks like as follows.

Ajax
Create a file, destroy.js.erb, put it next to your other .erb files (under app/views/ponies). It should look like this −

Ajax
Now enter the code as shown below in destroy.js.erb

$('.delete_pony').bind('ajax:success', function() {
   $(this).closest('tr').fadeOut();
});
Now Open your controller file which is placed at app/controllers/ponies_controller.rb and add the following code in destroy method as shown below −

# DELETE /ponies/1
# DELETE /ponies/1.json
def destroy
   @pony = Pony.find(params[:id])
   @pony.destroy
   
   respond_to do |format|
      format.html { redirect_to ponies_url }
      format.json { head :no_content }
      format.js   { render :layout => false }
   end
   
end
At finally controller page is as shown image.

Ajax
Now run an application, Output called from http://localhost:3000/ponies/new, it will looks like as following image

Ajax
Press on create pony button, it will generate the result as follows

Ajax
Now click on back button, it will show all pony created information as shown image

Ajax
Till now, we are working on scaffold, now click on destroy button, it will call a pop-up as shown below image, the pop-up works based on Ajax.

Ajax
If Click on ok button, it will delete the record from pony. Here I have clicked ok button. Final output will be as follows −
