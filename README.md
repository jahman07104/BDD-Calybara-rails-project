# README

This is the repo of the BDD Calybara course

This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

* Ruby version

* System dependencies

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...
************************************************
Git for version controll 
check status (git status)
add the files and new changes to track (git add -A)
commit the changes/disgard the changes as well (git commit -M "changes")
Save/Push your code to online repositories   - Github  (git push)
************************************************

RSPEC and Capybara
-write out the scenario in a test file
-First step - feature will fail
-build the features one by one till the test passes

*************************************************
Process for creating articles feature test and feature
-Install the RSpec and Capybara gems  

    ** Best practice is to clone a branch***
- Create a branch to do the developement work
- write the feature test
- Build the feature to make the test pass one by one
- Once the feature test passes with no errors - merge Branch with the master

expectations: 

- Visit root page
- click on new article
- fill in title
- fill in body
- create article

expectation:

- Article has been created
- articles patn

******************************************************
lecture notes

Text lecture - install RSpec and Capybara
Install RSpec and Capybara

In the Gemfile add the needed gems in their specific groups as follows:

group :development, :test do 
gem 'rspec-rails', '3.1.0'
end

group :test do
gem 'capybara', '2.7.1'
end

Then run:
bundle install

Now run the rspec install generator:
rails generate rspec:install

Generate a stub for RSpec:
bundle binstubs rspec-core

Make a git commit and push to Github:
git add -A
git commit -m "Setup RSpec and Capybara"
git push


************************************************************
Text lecture - create article feature test
Create Article Feature Test -

Create a topic branch:
git checkout -b article-feature-success

Create a folder called features under spec directory:
mkdir spec/features

In that folder create a new file called creating_article_spec.rb: 
Open that file and add the following:

****require "rails_helper" ***** must always be included as it sets up Capybara-Rails integration in spec/rails_helper.rb:
require 'capybara/rspec' is also needed to set up Capybara-RSpec integration in spec/spec_helper.rbc
***
RSpec.feature "Creating Articles" do 
scenario "A user creates a new article" do
visit "/"
click_link "New Article"
fill_in "Title", with: "Creating a blog" 
fill_in "Body", with: "Lorem Ipsum" 
click_button "Create Article"

expect(page).to have_content("Article has been created")
expect(page.current_path).to eq(articles_path) 
end
end

Now save the file type this to run the spec (or you can just type rspec to run all specs):
rspec spec/features/creating_article_spec.rb

You get a routing error that suggests to create a root path
Update the routes.rb file in the config folder like below:
root to: "articles#index"

Now save and run rspec spec/features/creating_article_spec.rb
again.
You get an error that says: Uninitialized constant ArticlesController. This suggests to create the Articles Controller

Generate an articles controller with an index action by issuing the following command:
rails g controller articles index

Remove the get 'articles/index' line from the routes.rb file

Save￼ and run rspec again. 
The next error message suggests to add the "New Article" link 