# User environment for peddie JupyterHub

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/2i2c-org/peddie-image/HEAD?urlpath=lab)

This repository specifies the user environment for the [peddie hub](https://peddie.pilot.2i2c.cloud/)
run by [2i2c](https://2i2c.org/).

## Making a change

1. Make a pull request to this repository with your environment changes (edits to
   `environment.yml`, `postBuild`, etc). A bot will post a link to `mybinder.org` that
   can be used to test your new changes! Use it, and make sure things work the way
   you would like. If not, amend the PR until it seems right.

2. Merge the PR. This will kick off a [GitHub Action](https://github.com/2i2c-org/peddie-image/actions)
   to build and push the container image. We use [quay.io](https://quay.io) instead of
   DockerHub, but that shouldn't matter to you. Wait for this action to finish.

3. Go to the [list of image tags](https://quay.io/repository/2i2c/peddie-image?tab=tags), and find
   the tag of the last push. This is *not* the `latest` tag but is usually under it. Use this
   to construct your image name - `quay.io/2i2c/peddie-image:<tag>`.

4. Open the [Configurator](https://peddie.pilot.2i2c.cloud/services/configurator/) for the peddie
   hub (you need to be logged in as an admin). You can also access it from the hub control panel,
   under *Services* in the top bar. Make a note of the current image name there, and
   put the image tag you constructed in the last step into the `User docker
   image` text box, and click `Submit`. This is alpha level software, so there
   is no 'has it saved' indicator yet :) You can find more information about the Configurator
   [here](https://pilot.2i2c.org/en/latest/admin/howto/configurator.html)

5. Test the new image by starting a new user server! If you already had one running, you need to
   stop and start it again to test.

6. If you find new issues, you can revert back to the previous image by entering the old image name,
   back in the JupyterHub Configurator. This will be streamlined in the future.
   
   # Adding libraries (less technical version)
This explains how to add a new library to your 2i2c JupyterHub environment.  Its target audience is someone who is essentially new to Github.  If you have developed with Github or think that this should all be done on the command line, the instructions above may suit you better.

There are special cases which may require slightly different procedures.  In the interest of simplicity, this focuses on the core case.

## Prerequisite
You need a Github account.  You can create one [here](https://github.com/join).

## Overview
The basic steps described informally:
1. Using the online Github editor, add the new library to a copy of the `environment.yml` file.
2. Using Binder, test the new version of `environment.yml` in a new container with the other old files.
3. Create a pull request to update (merge) `environment.yml` in the repo.
4. Create a new container built from the updated version of the repo. The new container will have a tag.
5. Using this tag, point your JupyterHub to the new container.

## In more detail
1. **Edit `environment.yml` file.** From repo's file listing, open `environment.yml` by clicking on it.  Next click on the pencil icon at upper left to edit.  Add the name of the new library to the list under 'dependencies:'. Follow the formatting of the list, including indentation and hyphen. At this point, you have only edited a copy of the `environment.yml` file.  Scroll down to 'Propose changes'.  Add brief and extended descriptions of your changes.  Click on the green 'Propose changes' button. You will then be taken to a new screen with a green 'Create pull request' button.  Press it. And on the next screen, press the next 'Create pull request' button.

2. **Test the changes.** On the next screen, a 'launch binder' button will appear under 'github-actions' to the left of the words 'Test this PR on Binder'.  Click on it. A Binder page will open with a black 'Build logs' window.  This may run for several minutes (eg, 5 minutes). If it completes without an error message, the build will be verified.  Before completing, the 'Build logs' window will say 'Pushing image' several times. Be patient. If successful,  'Launching server...' will appear and eventually a Jupyter (but not JupyterHub) tab will open. 

3. **Create pull request to update `environment.yml`.**  If you need to, return to the repo and click on 'Pull requests' near the top of the window.  You should be able to click on this pull request.  If the build was successful, you will see in green 'All checks have passed' and 'This branch has no conflicts with the base branch'.  Currently, under the latter you will see in small type the message 'Only those with write access to this repository can merge pull requests.'  You will have to wait for one of the 2i2c maintainer (admin) to merge this pull request.  Eventually, the plan is for a 'merge pull request' button to appear at the bottom of the page for you to press yourself.

4. **Get new container tag.** Go to the repo.  At the top, click on 'Actions'.  On the actions list, click on the 'Merge pull request...' for the change you just created.  Click on 'Build'. Click on 'update Jupyter dependencies with repo2docker'.  At the bottom of that breakout, you will see the words 'Successfully pushed...'  The tag you want appears at the end of that line after the colon. It's 12 characters long. Copy it.

5. **Point your JupyterHub to the new tag.** Open up your 2i2c JupyterHub. Click on 'Control Panel', then 'Services', then 'configurator'.  Replace the old 12-character tag with the new one.  Then shut down your JupyterHub server and restart it.  You should be good to go!  
   
