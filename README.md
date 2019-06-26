# CM-theme (2019)
Ghost theme for Curiosity Motive (2019 edition)

> Note: This is the previous README information. All information below is likely not to work currently, and will be updated eventually. (as of 06.24.19)

### Dependencies

Please make sure your dependencies match the following.

- Node: `>4.2`
- Gulp `>3.9`

### Setup

In this setup, `gulp` will install everything that you need to run Ghost locally for development (other than the Ghost content)

1. Run `npm install` to ensure the required dependencies are installed.
2. Run `gulp` and you'll have a new Ghost site generated for you and displayed in your browser.
3. Your default browser will open up [localhost:3000](http://localhost:3000/) automatically.


#### Ghost setup

1. Proceed to [localhost:3000/ghost/setup/](http://localhost:3000/ghost/setup/) to setup your Ghost install locally.
2. Run through the steps for setup, including setting up the local administrative user.
3. You can skip sending out invites on next screen, as email relays aren't setup yet.
4. Once you're in the administration, under the `Labs` link on the left there's a section for data import. You want to export the data from the current live CM site on it's respective `Labs` section and save to your computer.
5. Import the data you saved from CM.
6. Match up the backend settings from the live CM site to your local instance if they differ at all. ([General](http://localhost:3000/ghost/settings/general/), [Navigation](http://localhost:3000/ghost/settings/navigation/) and [Labs](http://localhost:3000/ghost/settings/labs/) sections)
7. Quit `gulp`

#### Theme setup

1. If you want to have all images from the live site, pull down the folder from the CM server at `/srv/users/serverpilot/apps/curiositymotive/public/content/images/2017/` and put in your Ghost folder at `~/YOURPATH/cm-theme/node_modules/ghost/content/images/2017/`.
2. Grab the `symlink.js` file from [this gist](https://gist.github.com/ff4500/665c2c8124081b46f6fe984ba4be49a3).
3. In a text editor, open up the `symlink.js` file you downloaded and place into `~/YOURPATH/cm-theme/gulp/tasks/`. Change the `.src('/YOURPATH/WHATEVER/')` path for the theme and images folders to match your local environment.
4. Run `gulp init` to automatically setup your local symbolic links.
5. Run `gulp` to start the project again
6. In your browser, navigate to [localhost:3000/ghost/settings/general/](http://localhost:3000/ghost/settings/general/) and scroll down to the 	`Themes` section at the bottom of the page.
7. Click to activate the `CM-Theme - 1.X.X` and hit save on the top right.
8. Go back to [localhost:3000/](http://localhost:3000/) and your site should be ready to go.

Note: You probably want to remove the example post entitled **Welcome to Ghost** at your convenience.

### Deploying

Deployment is done by doing a `git pull origin master` in the `cm-theme` directory on the server itself. Any git push of template files will require a restart of Ghost. Post up in the Slack channel if you need it restarted for some reason.
