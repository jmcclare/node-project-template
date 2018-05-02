# Node.js Project Template #

A template for a Node.js website project.

Site-specific commands are in the `bin` directory. Run the following to make
them available:

    . ./bin/set-env

Your Node.js app should go in the `app` directory. If you are using one of the
commands to setup the Node site template, it will create this for you.
Otherwise, create the `app` directory and fill it in yourself.


## Initialization ##

You should edit `config/versions` to set `node_version` to the specific node
release you will use for this project. It will fetch the latest Node version by
default.

To install Node.js with npm, run the following:

    ./bin/initialize-node

Note that the site creation commands below run `initialize-node` for you.

To install Node.js with npm and Koa and create a starting Koa 2 site with our
template, run the following:

    ./bin/create-koa-site

To install Node.js with npm and Express and create a starting Express site with
our template, run the following:

    ./bin/create-express-site


## Running the Site ##

To add this site's installation of `node` to your path, run the following:

    . ./bin/set-env

For any of the auto‐created sites, you can run the site in development mode with:

```bash
cd app
npm start
```

See the README and the `package.json` in the `app` directory for details on
other app commands and how to run it in production mode.

Production mode details may also be setup by your server config. If this is on
the server, look for a `server-info.txt` for details on how to configure or
manually control the site process.


## Static Files ##

Node can serve static files on it’s own. It usually serves everything in the
`app/public` directory. We also usually have NGinx setup to serve static files.
If you place (or symlink) static files in the `public` directory, NGinx will
serve them itself instead of passing the request off to the Node process.

This gives slightly better performance, and it allows us to configure static
file serving with NGinx, which can be better than Node.

For development mode, Node will be serving the static files, which means they
must also be in `app/public`. We find it best to keep all files in `app/public`
and symlink the files and directories we want NGinx to serve into `public`.
It’s simpler to keep the app specific code and static files all in `app` so
that you can deploy the Node app in a different site directory.
