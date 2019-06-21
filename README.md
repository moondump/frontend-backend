# One Repo With Two Directories
This repo demonstrates how to configure a single git repo that has two top-level
directories that can be deployed to two different places.

The `backend` directory contains a rails app. The frontend directory can
contain a static site or React app or whatever.

```
backend/
frontend/
Procfile
Gemfile
Gemfile.lock
```

Alongside the two directories there are three files, `Procfile`, `Gemfile`, and
`Gemfile.lock`.

Heroku depends on the `Gemfile` files being in the top level directory to
automatically detect that it's a Ruby applicatiton and build it all correctly.
Putting the gemfiles there is definietly weird! It's only to trick Heroku.

Manually take time to copy both the `Gemfile` files in order for Heroku to
detect and install things correctly. You should still use the two `Gemfile`
files inside the `backend` directory for your actual rails server on your own
machine. If you make changes there make sure you copy the changes back up top
so when Heroku reads them it installs the correct things.

The `Procfile` is a tiny configuration file that tells Heroku how to start
running the web server. In this case we tell it to specicially `cd` into
the backend directory, and then run `rails s`.

**Procfile**
```
web: cd backend && bundle exec rails s
```

