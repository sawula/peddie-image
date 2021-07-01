# Adding libraries simply
This explains how to add a new library to your 2i2c JupyterHub environment.  Its target audience is someone who is essentially new to Github.  If you have developed with Github or think that this should all be done on the command line, the other instructions may suit you better.

There are special cases which may require a slightly different procedure.  In the interest of simplicity, this focuses on the core case.

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

2. **Test the changes.** On the next screen, a 'launch binder' button will appear under 'github-actions' to the left of the words 'Test this PR on Binder'.  A Binder page will open with a black 'Build logs' window.  This may run for several minutes (eg, 5 minutes). If it completes without an error message, the build will be verified.  Before completing, the 'Build logs' window will say 'Pushing image' several times. Be patient. If successful,  'Launching server...' will appear and eventually a Jupyter (but not JupyterHub) tab will open. 

3. **Create pull request to update `environment.yml`.**  If you need to, return to the repo and click on 'Pull requests' near the top of the window.  You should be able to click on this pull request.  If the build was successful, you will see in green 'All checks have passed' and 'This branch has no conflicts with the base branch'.  Currently, under the latter you will see in small type the message 'Only those with write access to this repository can merge pull requests.'  You will have to wait for one of the 2i2c maintainer (admin) to merge this pull request.  Eventually, the plan is for a 'merge pull request' button to appear at the bottom of the page for you to press yourself.

4. **Get new container tag.** Go to the repo.  At the top, click on 'Actions'.  On the actions list, click on the 'Merge pull request...' for the change you just created.  Click on 'Build'. Click on 'update Jupyter dependencies with repo2docker'.  At the bottom of that breakout, you will see the words 'Successfully pushed...'  The tag you want appears at the end of that line after the colon. It's 12 characters long. Copy it.

5. **Point your JupyterHub to the new tag.** Open up your 2i2c JupyterHub. Click on 'Control Panel', then 'Services', then 'configurator'.  Replace the old 12-character tag with the new one.  Then shut down your JupyterHub server and restart it.  You should be good to go!
