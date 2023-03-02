# Scaffold-LookOut

Using Scaffold:

1) Commands

$ bundle install
$ npm install --prefix client

2) Generators

$ rails g scaffold lowercase_snake_formatted_name attr_default_string attr_of_type:datatype model_that_has_many_of_these:belongs_to --no-test-framework

Lowercase snake is is the only format that will turn test_model into TestModel, TestModels, has_many :test_models, etc in all the right places.
Pay attention to using belongs_to relationships in this generator as it will create the foreign key tables. We won’t need to use has_many in this line ever because of the nature of where foreign keys live.
If you make a mistake . . .

$ rails d scaffold lowercase_snake_formatted_name attr_default_string attr_of_type:datatype model_that_has_many_of_these:belongs_to --no-test-framework

// the difference is a "d" for destroy instead of "g" for generate //

3) Fill out model relationships
belongs_to will be created automatically
has_many will be created like so . . .

has_many :signups, dependent: :destroy
has_many :campers, through: :signups
** This is a good time to consider dependent: :destroy if applicable. **
    
4) Fill out model validations
Here are some common ones . . .

validates :name, presence: true
validates :age, :inclusion => 8..18
validates :email, :uniqueness: true

5) Seed

$ rails db:migrate db:seed

6) routes.rb 
** rails g scafffold will generate full CRUD for you under
resources :model_name

to limit / cut down unnecessary routes 

resources :models, only: [:index, :show, :create]
or
resources :models, except: [:update, :destroy]

** putting the CRUD method you want to dislay inside [], any method not mentioned will be exluded from routes
