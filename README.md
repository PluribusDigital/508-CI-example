# Example of 508 Scans in CI Process

This repo implements accessibility scans via [pa11y](https://github.com/pa11y/pa11y) in a CI pipeline, failing a build for errors.

## Why

Accessibility should be a concern for any development team. STSI supports federal government clients, which are bound to comply with [Section 508 of the Rehabilitation Act](https://www.section508.gov/). This demo shows one way to automate some accessibility/compliance checks and incorporate that into a CI process.

## This Implementation and Alternatives

This repo has the following major components:

 * A Sample Application, which is described below the line, and borrowed from [*Ruby on Rails Tutorial: Learn Web Development with Rails*](http://www.railstutorial.org/) by [Michael Hartl](http://www.michaelhartl.com/). The sample app accounts for everything except for the two folders below.
 * The `508scan/` directory includes the package.json file that defines the dependencies and the command to run the scan.
 * The `.circleci/` directory includes the configuration for the hosted CI environment.

The app has 508 compliance issues, thus should fail the build. You can see the failure on [CircleCI](https://circleci.com/gh/STSILABS/508-CI-example/6). 

### Running the Scan Locally

From the `508scan` directory, run `yarn install` and then `yarn scan508`. (Yarn is a pre-req, and NPM is an alternative to that.)

### Shortcomings

This demo uses a crude command `rails s & sleep 10 && pa11y http://localhost:3000/signup` to run the scan. It starts up the rails server, then runs pa11y against one hard-coded URL. This works for the demo or a smoke test, but has limitations:
 * We'd have to add more hard-coded URLs to test more pages
 * We can't script things like logging in, or other actions that would render "deeper" content
 * It is specific to Ruby on Rails

## Alternatives

Pa11y can run against URLs (as above), but can also run against files, or a directory of files. We can use a robust full-stack testing framework (protractor, cucumber, etc.) to perform full-stack/functional/acceptance testing, and use those tools to save the rendered pages at different points. Those could be saved into a `508scan/static_files` directory. Then, instead of pointing pa11y to a URL, we can point it to that directory.

-----

# Ruby on Rails Tutorial sample application

This is the reference implementation of the sample application for the 4th edition of [*Ruby on Rails Tutorial: Learn Web Development with Rails*](http://www.railstutorial.org/) by [Michael Hartl](http://www.michaelhartl.com/).

## License

All source code in the [Ruby on Rails Tutorial](http://railstutorial.org/) is available jointly under the MIT License and the Beerware License. See [LICENSE.md](LICENSE.md) for details.

## Getting started

To get started with the app, clone the repo and then install the needed gems:

```
$ cd ~/tmp
$ git clone https://bitbucket.org/railstutorial/sample_app_4th_ed.git sample_app
$ cd sample_app
$ bundle install --without production
```

Next, migrate the database:

```
$ rails db:migrate
```

Finally, run the test suite to verify that everything is working correctly:

```
$ rails test
```

If the test suite passes, you'll be ready to run the app in a local server:

```
$ rails server
```

On Cloud9, this command should be

```
$ rails server -b $IP -p $PORT
```

instead.

To check out the code for a particular chapter, use

```
$ git checkout chapter-branch-name
```

where you can find the branch name using

```
$ git branch -a
```

A branch called `remotes/orgin/foo-bar` can be checked out using `git checkout foo-bar`.

For more information, see the
[*Ruby on Rails Tutorial* book](http://www.railstutorial.org/book).
