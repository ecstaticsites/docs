# 2 - Basic Publishing

In the basic case, it's easy to publish a site using plain old HTML, CSS, and Javascript files.

> If you haven't created a site yet, see [the docs for site creation](./creating.md) instead!

### Prerequisites

To begin, you'll want to make sure you have the program `git` installed on your computer. Depending on your operating system, you may have this installed already -- most Linux and MacOS systems come with it. If you need to install it, you can download a copy on the [official Git website](https://git-scm.com/downloads).

In addition, you'll also need the ID of the site you want to update. This can be found on the Ecstatic web app, in the "Settings" page for the site in question (check the sidebar).

### Add a Git Remote

From there, all you need is a Git repository with Ecstatic added as a remote.

You might already be using Git to version-control your website, in which case, great! If not, it's a great idea to start doing so (even disregarding Ecstatic). To get started, go ahead and read a simple "getting started with Git" guide like [this one](https://www.garyrobinson.net/2014/10/git-in-two-minutes-for-a-solo-developer.html) to get a repository set up.

Then, run the following command to add Ecstatic as a "remote" of your Git repository:

```sh
# replace "bala-dori-nuge" below with your site ID
git remote add ecstatic https://git.ecstaticsites.org/bala-dori-nuge
```

And you're all set! This adds Ecstatic as a "push target" of your Git repository, so it'll be easy to publish updates to your site in the same way as you handle your version control.

### Git Push

After the above one-time step, all you need to do to publish an update is push, like this:

```sh
# below assumes "main" is your default branch
git push ecstatic main
```

The first time you try this, it will ask for credentials -- you should enter the same email and password you use for the Ecstatic web app.

Then, you'll see your files packaged up and uploaded to Ecstatic, and lines printed in your terminal (the ones which have `remote:` at the front) will show the progress of those files being uploaded to the CDN which serves your site.

At that point, you can visit your site's URL in a browser to see your changes live on the web! You may need to do a hard-refresh to see what you expect.
