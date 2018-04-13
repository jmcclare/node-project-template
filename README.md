# Node.js Site #

This is a site built with Node.js.

Site-specific commands are in the `bin` directory. Run the following to make
them available:

    . ./bin/set_env


## Initialization ##

To install Node.js with npm, run the following:

    ./bin/initialize_node

You should run this again whenever you re-deploy the site on a new server. Make
sure you go through the post-installation below the first time you install.

To install Node.js with npm and Express and create a starting Express site with
our template, run the following:

    ./bin/create_express_site


## Running the Site ##

To add this site's installation of `node` to your path, run the following:

    . ./bin/set_env

For a pure ExpressJS site:

    node app/app.js

Or, if you are building a pure CoffeeScript app:

    coffee app/server.coffee

For commands to run / restart the site in production, see your server
configuration, or `server-info.txt` if it is provided.


## Post-Installation ##

After installing Node with `initialize_node`, you should edit `config/versions`
to set `node_version` to the specific node release you will use for this
project. This way, when you re-deploy to a new server you can run
`initialize_node` again and recompile using the same version of Node.

Run the following after initializing Node to find the version you just
installed:

    . ./bin/set_env
    node --version

You should also nail down the versions of all Node packages you are using for
your site. These are usually specified in `app/package.json`. It's alright to
grab the latest version of everything when you create a new site, but when you
re-deploy a site, you want the same versions your development servers are
using.

For each package listed in `package.json`, run <package-name> --version to see
which version you have. Put this version number in `package.json` instead of
`*` or `latest`.


## Updating jmcclare web-templates ##

See the `README.md` in `lib/jmcclare-web-templates/node-express` for detailed
instructions on updating these files.

Download the [latest `.tar.gz` of
web-templates](https://github.com/jmcclare/web-templates/tarball/master) from
GitHub.


## Static Files ##

Node can serve static files on it's own. It usually serves everything in the
`app/public` directory. We also usually have NGinx setup to serve static files.
If you place (or symlink) static files in the `public` directory, NGinx will
serve them itself instead of passing the request off to the Node process.

This gives slightly better performance, and it allows us to configure static
file serving with NGinx, which can be better than Node.

For development mode, Node will be serving the static files, which means they
must also be in `app/public`. We find it best to keep all files in `app/public`
and symlink the files and directories we want NGinx to serve into `public`.
