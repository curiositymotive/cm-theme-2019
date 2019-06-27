# CM-theme (2019)
Ghost theme for Curiosity Motive (2019 edition)

> Note: This README information is still in process. This is the original Casper theme, (sort of) forked from the [Casper repo](https://github.com/TryGhost/Casper). See their README for expanded theme info and links to the Ghost theme API for more information.


## Dependencies

- [Docker](https://docs.docker.com/install/) and [Docker Compose](https://docs.docker.com/compose/install/)
- [Node](https://nodejs.org/)
- [Yarn](https://yarnpkg.com/)
- [Gulp](https://gulpjs.com)

## Setup

Docker is awesome. In this setup, we'll be using it to load up our site and get it running. It's pretty simple, provided that you have the dependencies installed already and have Docker running locally.

On a mac, you can just install Node, Yarn and Gulp with [Homebrew](https://brew.sh) to get up and running fairly quickly. (`brew install node yarn gulp`)

This should be everything that you'll need to run Ghost locally for development (other than the Ghost content, see below)

1. Clone this repo to your machine
2. Change to the .local dir - `cd .local`
3. Start the Ghost instance with Docker Compose - `docker-compose up -d` (you can just run `docker-compose up` without the `-d` flag if you want to see the Ghost CLI output)
4. Head over to [localhost:2368](http://localhost:2368/) in your browser, you should see that Ghost is up and running now

### Ghost setup

1. Proceed to [localhost:2368/ghost/](http://localhost:2368/ghost/) to setup your Ghost install locally.
2. Run through the steps for setup, including setting up the local administrative user.
3. You can skip sending out invites on next screen, as email relays aren't setup yet.
4. In the Admin, go ahead and navigate to the [Staff](http://localhost:2368/ghost/#/staff) section and click on the Admin user. In the gear icon on the top right, choose `Delete User` and remove the user and all of their posts. (This will remove the initial demo content fromt the site)
5. Under the `Labs` link on the left there's a section for data import. You want to export the data from the current live CM site on it's respective `Labs` section and save to your computer.
6. Import the data you saved from the CM site.
7. Match up the backend settings from the live CM site to your local instance if they differ at all. ([General](http://localhost:2368/ghost/#/settings/general), [Design](http://localhost:2368/ghost/#/settings/design) and [Labs](http://localhost:2368/ghost/#/settings/labs) sections)

### Theme setup

1. If you want to have all images from the live site, pull down the folder from the CM server at `/srv/www/curiositymotive.com/public/images/` and put in your Ghost folder at `~/YOURPATH/cm-theme-2019/.local/images/`
2. Make sure you're in the .local dir in the theme repo - `cd ~/YOURPATH/cm-theme-2019/.local/`
3. Restart the instance with Docker Compose - `docker-compose down && docker-compose up -d`
4. Go back to [localhost:2368/](http://localhost:2368/) and your newly loaded images should be ready to go.

> Note: Any changes that you make to the local images folder will NOT be mirrored on the live site. Be sure to also make your edits there as well (to avoid the import/export dance over and over).

#### Updating images from the live site

If you have already downloaded the images at some point and just want to update from the live site, you can use rsync to quickly update your local files:

```
rsync -azP user@curiositymotive.com:/srv/www/curiositymotive.com/public/images ~/YOURPATH/cm-theme-2019/.local/
```

## Theme Development

Theme styles are compiled using Gulp/PostCSS to polyfill future CSS spec. From the theme's root directory (`cd ~/YOURPATH/cm-theme-2019/`), run:

```bash
$ yarn install
$ yarn dev
```

Now you can edit `/assets/css/` files, which will be compiled to `/assets/built/` automatically.

The `zip` Gulp task packages the theme files into `dist/cm-theme-2019.zip`, which you can then upload to your site.

```bash
$ yarn zip
```

> Note: If you are running Ghost in the foreground with `docker-compose up`, rather in detatched mode, you'll have to open up a new terminal window and navigate to the theme dir in order to run the `yarn` commands above. Also, we likely won't be uploading the zipped theme files to the site directly. See below for deployment information of your completed/updated theme.

## Deploying

Deployment is done by doing a `git pull origin master` in the `cm-theme-2019` directory on the server itself (`/srv/www/curiositymotive.com/public/themes/cm-theme-2019/`). Any git push of template files will require a restart of Ghost. Post up in the Slack channel if you need it restarted for some reason.

----

_Updated 06.24.19_
