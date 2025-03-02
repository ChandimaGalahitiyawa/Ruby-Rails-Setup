====================================================================
                         rails_setup
====================================================================

A Ruby on Rails application configured with MySQL for database management,
Devise for authentication, Cancancan for authorization, and Bootstrap for
responsive design. This project provides a quick and robust starting point
for developing modern web applications.

====================================================================
                         TABLE OF CONTENTS
====================================================================
1. Overview
2. Features
3. Prerequisites
4. Installation
5. Usage
6. Contributing
7. License

====================================================================
1. OVERVIEW
--------------------------------------------------------------------
rails_setup is a Rails project designed to offer a solid foundation for
web applications with the following integrations:

  - MySQL: Used as the database backend.
  - Devise: Implements secure user authentication (sign-up, sign-in, sign-out).
  - Cancancan: Provides role-based access control and permission management.
  - Bootstrap: Enables responsive front-end styling via CDN.

The configuration sets the Devise sign‑in page as the home page and pre-
configures the application layout to load Bootstrap, allowing for rapid UI
customization.

====================================================================
2. FEATURES
--------------------------------------------------------------------
• User Authentication: Secure registration and login capabilities using Devise.
• User Authorization: Role-based access control managed with Cancancan.
• Responsive Design: Out-of-the-box styling with Bootstrap.
• MySQL Integration: Robust and scalable database management.

====================================================================
3. PREREQUISITES
--------------------------------------------------------------------
Before getting started, ensure you have the following installed on your system:

  - Homebrew           (https://brew.sh/)
  - MySQL              (https://dev.mysql.com/downloads/)
  - Ruby               (https://www.ruby-lang.org/en/downloads/)
  - Rails              (https://rubyonrails.org/)
  - Bundler            (https://bundler.io/)

====================================================================
4. INSTALLATION
--------------------------------------------------------------------
Step 1: Start the MySQL Service
--------------------------------
  Open your terminal and run:
    brew services start mysql

Step 2: Create a New Rails Application with MySQL
--------------------------------------------------
  Run the following commands:
    rails new rails_setup --database=mysql
    cd rails_setup

Step 3: Install Dependencies
----------------------------
  In your project directory, run:
    bundle install

Step 4: Install Cancancan for Authorization
-------------------------------------------
  Run these commands:
    bundle add cancancan
    rails generate cancan:ability

Step 5: Install Devise for Authentication
-----------------------------------------
  Execute:
    bundle add devise
    rails generate devise:install
    rails generate devise User
    rails db:migrate

Step 6: Configure Rails Routes
------------------------------
  Replace the content of "config/routes.rb" with the following:

    Rails.application.routes.draw do
      devise_for :users, path: '', path_names: { sign_in: 'login', sign_out: 'logout', sign_up: 'register' }
      devise_scope :user do
        root to: 'devise/sessions#new'
      end
    end

Step 7: Update the Application Layout to Include Bootstrap
-----------------------------------------------------------
  Replace the content of "app/views/layouts/application.html.erb" with:

    <!DOCTYPE html>
    <html>
      <head>
        <title><%= File.basename(Dir.getwd) %></title>
        <meta name="viewport" content="width=device-width,initial-scale=1">
        <%= csrf_meta_tags %>
        <%= csp_meta_tag %>

        <!-- Bootstrap CSS via CDN -->
        <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet"
              integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH" crossorigin="anonymous">
        <%= stylesheet_link_tag "application", "data-turbo-track": "reload" %>
      </head>
      <body>
        <div class="container">
          <%= yield %>
        </div>

        <!-- Bootstrap JS via CDN -->
        <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"
                integrity="sha384-YvpcrYf0tY3lHB60NNkmXc5s9fDVZLESaAA55NDzOxhy9GkcIdslK1eN7N6jIeHz" crossorigin="anonymous"></script>
        <%= javascript_importmap_tags %>
      </body>
    </html>

Step 8: Generate Devise Views for Customization with Bootstrap
---------------------------------------------------------------
  Run:
    rails generate devise:views

Step 9: Start the Rails Server
------------------------------
  Finally, run:
    rails s

====================================================================
5. USAGE
--------------------------------------------------------------------
After completing the installation steps, start the Rails server and open
your web browser to visit:
  http://localhost:3000

The homepage is set to the Devise sign‑in page, where you can register a new
account or log in if you already have one.

====================================================================
6. CONTRIBUTING
--------------------------------------------------------------------
Contributions to rails_setup are welcome!

If you find a bug or have a feature request, please open an issue or submit
a pull request. For major changes, please discuss your ideas by opening an
issue first.

To contribute:
  1. Fork the repository.
  2. Create a new branch (e.g., git checkout -b feature/YourFeature).
  3. Commit your changes (e.g., git commit -am "Add new feature").
  4. Push your branch (e.g., git push origin feature/YourFeature).
  5. Open a pull request describing your changes.

====================================================================
7. LICENSE
--------------------------------------------------------------------
This project is licensed under the MIT License.
See the LICENSE file for details.

====================================================================
                           END OF README
====================================================================
