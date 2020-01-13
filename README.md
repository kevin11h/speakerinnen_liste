[![Build Status](https://travis-ci.org/rubymonsters/speakerinnen_liste.png)](https://travis-ci.org/rubymonsters/speakerinnen_liste) [![Code Climate](https://codeclimate.com/github/rubymonsters/speakerinnen_liste.png)](https://codeclimate.com/github/rubymonsters/speakerinnen_liste)

# About speakerinnen.org

speakerinnen.org is a searchable web directory designed specifically for women* conference speakers. Women* speakers are encouraged to sign up and provide professional information, including their area of expertise, any previous conferences they've presented at, contact details, etc.

The aim of the app is to provide a way for conference and event organizers to find and contact appropriate women* speakers. (But obviously there are many different contexts in which it can be used...)

**Please note: Sometimes for better readability in long passages of text the term `women` is written without a star but we always mean everyone who defines herself as a woman.**

# Getting Started

**1 Clone the repository:** `git clone git@github.com:rubymonsters/speakerinnen_liste.git` and access the folder: `cd speakerinnen_liste`.

**2 Copy `config/database_example.yml` and rename it to `database.yml` file and make sure it is always set to `.gitignore`:** `cp config/database_example.yml config/database.yml`

**3 Install Docker** If you don't have Docker installed, please download it [here](https://docs.docker.com/install/** for your operating system.

**4 Local setup** (you'll need to repeat this whenever there are new dependencies): `make setup`

## Development workflow

The setup is done using Docker to provide all the dependencies and the environment. To access this enviornment you need to run `make dev` and that gets you a session where you can do all the usual things you do in a Rails app (many of them are mentioned later in this file). Some that you'll need before using the app from the first time:

* `rake db:seed`: Load some initial example profiles.
* `rake elasticsearch:import:all`: Import the loaded profiles into the search index

But in general, any `rake`, `bundle` or `rails` command will work inside that development session.

In addition to `make dev`, which will let you run any development flow command, some shortcuts are defined for the most common tasks. Run `make usage` to get a list. But notably:

* `make up`: Start the app.
* `make test`: Run the tests.

## Admin user

  If you build or test some admin features you have to create an admin user (by default the admin attribute for each user is set to false) except 1 admin user is initially created by the `db/seed.rb` file.

  You also can assign the admin status of a user via the rails console:

  ```ruby
  # Log into the rails console
  $ bundle exec rails c

  # Inside the rails console
  user = Profile.find(<your-profile-id>)
  user.admin = true
  user.save

  # Verify your user admin status
  user.valid?

  # => true
  ```

# Testing

```
# Run all tests of the project
$ bundle exec rspec spec

# If the tests are still failing, run:
$ bundle exec rake db:test:clone

# If tests are still failing, run:
$ rails db:test:prepare

# Run tests excluding elasticsearch specs, so without a running elasticsearch server
$  bundle exec rspec spec --tag '~elasticsearch'
```

# Please use Rubocop

```
# Runs rubocop and corrects all errors it can
$ rubocop -a
```

# Database:
Our database schema looks like that:


![db](https://user-images.githubusercontent.com/1218914/43900439-368fa600-9be5-11e8-8f9c-d209784de1ef.jpg)

# Metrics
For seeing our metrics we use the free community edition of honeyycomb ( https://ui.honeycomb.io/login )
More infos how to use this: https://docs.honeycomb.io/beeline/ruby/

# Logging
We are using papertrail.
`heroku addons:open papertrail --app speakerinnen-liste`

# Report Errors
We are using sentry.
`heroku addons:open sentry --app speakerinnen-liste`

# Deployment
We use Heroku to deploy.

# Contributing

Do you want to contribute?

If you want to contribute, you can get an overview over the open issues on our [Project Management Board](https://github.com/rubymonsters/speakerinnen_liste/projects/1) and via https://github.com/rubymonsters/speakerinnen_liste/issues/216.

We are happy to answer your questions if you consider to help. All the issues have a link to their specification. If you want to work on an issue feel free to assign yourself.

Find further details in: https://github.com/rubymonsters/speakerinnen_liste/blob/master/CONTRIBUTING.md

# ♥ Code of Conduct

Please note that [speakerinnen](https://speakerinnen.org) has a [Contributor Code of Conduct](https://github.com/rubymonsters/speakerinnen_liste/blob/master/code-of-conduct.md) based on the [Contributor Covenant](https://www.contributor-covenant.org). By participating in this project online or at events you agree to abide by its terms.
