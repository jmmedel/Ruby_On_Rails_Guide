

Ruby on Rails - Active Records
Advertisements
 Previous Page Next Page  
Rails Active Record is the Object/Relational Mapping (ORM) layer supplied with Rails. It closely follows the standard ORM model, which is as follows −

tables map to classes,
rows map to objects and
columns map to object attributes.
Rails Active Records provide an interface and binding between the tables in a relational database and the Ruby program code that manipulates database records. Ruby method names are automatically generated from the field names of database tables.

Each Active Record object has CRUD (Create, Read, Update, and Delete) methods for database access. This strategy allows simple designs and straight forward mappings between database tables and application objects.

Translating a Domain Model into SQL
Translating a domain model into SQL is generally straight forward, as long as you remember that you have to write Rails-friendly SQL. In practical terms, you have to follow certain rules −

Each entity (such as book) gets a table in the database named after it, but in the plural (books).

Each such entity-matching table has a field called id, which contains a unique integer for each record inserted into the table.

Given entity x and entity y, if entity y belongs to entity x, then table y has a field called x_id.

The bulk of the fields in any table store the values for that entity's simple properties (anything that's a number or a string).

Creating Active Record Files (Models)
To create the Active Record files for our entities for library application, introduced in the previous chapter, issue the following command from the top level of the application directory.

library\> rails script/generate model Book
library\> rails script/generate model Subject
Above rails generate model book commands generates the auto code as below −

Book Generate
You're telling the generator to create models called Book and Subject to store instances of books and subjects. Notice that you are capitalizing Book and Subject and using the singular form. This is a Rails paradigm that you should follow each time you create a model.

When you use the generate tool, Rails creates the actual model file that holds all the methods unique to the model and the business rules you define, a unit test file for performing test-driven development, a sample data file (called fixtures) to use with the unit tests, and a Rails migration that makes creating database tables and columns easy.

Apart from creating many other files and directories, this will create files named book.rb and subject.rb containing a skeleton definition in the app/models directory.

Content available in book.rb −

class Book < ActiveRecord::Base
end
Content available in subject.rb −

class Subject < ActiveRecord::Base
end
Creating Associations between Models
When you have more than one model in your rails application, you would need to create connection between those models. You can do this via associations. Active Record supports three types of associations −

one-to-one − A one-to-one relationship exists when one item has exactly one of another item. For example, a person has exactly one birthday or a dog has exactly one owner.

one-to-many − A one-to-many relationship exists when a single object can be a member of many other objects. For instance, one subject can have many books.

many-to-many − A many-to-many relationship exists when the first object is related to one or more of a second object, and the second object is related to one or many of the first object.

You indicate these associations by adding declarations to your models: has_one, has_many, belongs_to, and has_and_belongs_to_many.

Now, you need to tell Rails what relationships you want to establish within the library data system. To do so, modify book.rb and subject.rb to look like this −

class Book < ActiveRecord::Base
   belongs_to :subject
end
We have used a singular subject in the above example, because one Book can belong to a single Subject.

class Subject < ActiveRecord::Base
   has_many :books
end
We have used plural books here, because one subject can have multiple books.

Implementing Validations on Models
The implementation of validations is done in a Rails model. The data you are entering into the database is defined in the actual Rails model, so it only makes sense to define what valid data entails in the same location.

The validations are −

The value of title field should not be NULL.
The value of price field should be numeric.
Open book.rb in the app\model subdiractory and put the following validations −

class Book < ActiveRecord::Base
   belongs_to :subject
   validates_presence_of :title
   validates_numericality_of :price, :message=>"Error Message"
end
validates_presence_of − protects "NOT NULL" fields against missing user input.

validates_numericality_of − prevents the user, entering non numeric data.

Besides the validations mentioned above, there are other common validations. Check Rails Quick Guide.

What is Next?
In the next chapter, we will learn Rails Migration, which allows you to use Ruby to define changes to your database schema, making it possible to use a version control system to keep things synchronized with the actual code.
