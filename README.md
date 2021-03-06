Analytics
=========
BSkyB wrapper for Adobe Sitecat analytics JS.

## Code structure
- lib/omniture.js
  The original omniture js library. This file shouldn't need to be modified
  often.

- lib/tracking.js
  The bskyb api wrapper around the omniture js file. New functionality should
  be added here.

- views/
  Documentation for using the API

- app.rb
  A basic Sinatra server for displaying the documentation, and running the tests

- test/
  the functional tests for the API

- circle.yml
  Configuration for the CI server

- config.ru
  Configuration for running the Sinatra server

## Prerequisites for running the documentation and tests

- RVM
- Ruby (version 1.9.3 or later)

## Setup
1. Clone the repository from Github onto your local machine
2. Create a gemset (not required)
  - rvm --rvmrc --create default@<gemset name>
3. In the root of the project, run the following:
  - bundle
  - rackup
4. You should be able to see the documentation site in your browser on http://localhost:4567

## Running the tests
Tests are found in the test directory. At present only functional
tests are run. These tests use minitest and capybara.

To run the test suite, simply type `rake functional` in your terminal

You can add additional files within the functional directory and these will be
picked up by the rake task.

The tests within the functional directory will be run on the CI server
automatically upon pushing to Github

## Deployment
In order to release a new version of the library, the versionfile must be
incremented following the rules below: 

### Versioning
This library should follow the [Semantic versioning
specification](http://semver.org/). In short, that means the following:

Version: X.Y.Z

- API changes that are **not backwards compatible**, and break existing
  calls using the API must increment the X value.

- API changes that introduce **new backwards compatible changes**, or **change the
  internals**, but not the interface, of existing methods will increment the
  Y value.

- **Patches or bug fixes** that are backwards compatible should increment the
  Z value.


Upon commiting and pushing your code to Github, the CI server will run through
the functional tests and - if there are no errors - a new version of the library
will be deployed to the CDN using the version number specified in the
versionfile.
