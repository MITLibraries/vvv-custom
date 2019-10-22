This should allow you to get a rudimentary copy of the MIT Libraries' WordPress network running under your VVV box.

## Prerequisites

You will need the following:

- [Vagrant](https://www.vagrantup.com/)

## Defining the network

1. Clone https://github.com/Varying-Vagrant-Vagrants/VVV
**Do not run `vagrant up` yet**

2. Copy `vvv-custom.yml` from this repository into the VVV folder (as a sibling to `vvv-config.yml`)

3. `Vagrant up`
Note any errors you encounter. **Please note:** this step can take quite a bit of time.

You will now have a running WordPress network visible at http://mitlib-public.test (using a stock theme's homepage)
You should also see the VVV dashboard at http://vvv.test/, which will list any other sites that have been defined.

## Installing local projects

The majority of our WordPress development work is focused on building themes and plugins, each of which have their own repositories. Because contributions are managed via git, they cannot be provisioned via `vvv-custom.yml`.

Please follow the steps below for any such project to which you want to contribute.

4. Install and build the parent theme
   - Clone git@github.com:MITLibraries/MITlibraries-parent.git into `$vagrantroot/www/mitlib-public/public_html/wp-content/themes/libraries` (note the directory name must be `libraries`)
   - `npm install` to install the build tooling
   - `grunt` to run the build

5. Log into WordPress at http://mitlib-public.test/wp-admin/ with the username `admin` and `password`

6. Network-enable the parent theme at http://mitlib-public.test/wp-admin/network/themes.php

7. Activate the parent theme to at http://mitlib-public.test/wp-admin/themes.php

8. The theme should now be installed and ready to serve content. The front page will be broken for a bit longer, unfortunately, but the following URLs should work:
   - http://mitlib-public.test/blog/2013/03/15/tiled-gallery/
   - http://mitlib-public.test/about/

Further content can be found from the WP admin dashboard at http://mitlib-public.test/wp-admin/edit.php?post_type=page

### Local themes

Our list of locally-maintained themes can be found at https://github.com/search?q=topic%3Awordpress-theme+org%3AMITLibraries+fork%3Atrue. They should be installed under `$vagrantroot/www/mitlib-public/public_html/wp-content/themes/`.

### Local plugins

Our list of locally-maintained plugins can be found at https://github.com/search?q=topic%3Awordpress-plugin+org%3AMITLibraries+fork%3Atrue. They should be installed under `$vagrantroot/www/mitlib-public/public_html/wp-content/plugins/`. Plugins can typically skip the NPM / Grunt portions of step 4 above.

## Future work

This workflow is obviously painful. I'm working on making it suck less. The general roadmap includes:

- Making the themes directory-agnositc
- Making the themes auto-build (or not need a build step)
- Building the entire network via Composer
- Installing locally-built themes and plugins via the site template
- Recovering a handful of plugins that are no longer listed in the WordPress directory (see the "missing_plugins" section in `vvv-custom.yml`)

If you encounter something that feels needlessly painful, please bring it up to the EngX group for consideration.
