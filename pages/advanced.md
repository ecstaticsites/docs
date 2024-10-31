# 3 - Advanced Publishing

Ecstatic also includes support for sites which require a build step.

This is necessary for fancy static sites, like web app frontends using something like [Webpack](https://webpack.js.org/) or blogs generated from Markdown files using something like [Jekyll](https://jekyllrb.com/).

> If you haven't created a site yet, see [the docs for site creation](./creating.md) instead!

### Prerequisites

Ecstatic supports all website build tools in all programming languages, via [Devbox](https://www.jetify.com/devbox). You'll need to have it and Nix installed in order to continue (Devbox installer will take care of installing Nix as well if you don't already have it).

### Creating an Environment

Then, you'll need to create a Devbox environment in your repository.

This is a one-step process on the command line (do this in the root of your repository):

```sh
$ devbox init
```

And you'll see a new `devbox.json` file in your current directory.

Then, add to this environment any dependencies you need in order to build your project -- it's a good idea to add specific versions of these. For example, if your build tool relies on a Javascript runtime (or is installed via `npm`), you can add that to your Devbox with the following:

```sh
$ devbox add nodejs@20
```

Then, to make sure it worked, you should be able to run:

```sh
$ devbox run npm init
```

And see the the prompts to create a new package.

### Setting up Scripts

Then, you'll need to edit that `devbox.json` file to add a couple of [scripts](https://www.jetify.com/docs/devbox/guides/scripts/).

Ecstatic expects your configuration to define two scripts:

* `install`, which should install dependencies and run any other pre-build steps
* `build`, which should build the actual site and output it to a directory

The content of those scripts depends on the site generator you've chosen to use! To see an example of a compliant `devbox.json`, you can see the [main Ecstatic webapp configuration](https://github.com/ecstaticsites/js/blob/main/devbox.json).

It's no problem to define additional scripts here -- for example, having one called `dev` is often nice for running a local development server.

### Configuring the Site

If your site has a build step, it's likely it renders the site in a child directory, for example `_site`.

In this case, now's the time to tell Ecstatic about it! Go to the site's "settings" page in the [Ecstatic UI](https://app.ecstaticsites.org/#/sites), and in the "Index Path" field, enter where Ecstatic can find your site's `index.html` after the site has been built, for example the following:

```
/_site/index.html
```

### Git Push

Finally, you should commit the above changes and push to Ecstatic:

```sh
# below assumes "main" is your default branch
$ git push ecstatic main
```

If it all went according to plan, you should see a line like this in the output:

```
remote: File devbox.json found, attempting to build site...
```

And you'll see logs from Ecstatic running `devbox run install` and `devbox run build` before it attempts to upload your site to the CDN. Magic!
