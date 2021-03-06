[![Import](https://cdn.infobeamer.com/s/img/import.png)](https://info-beamer.com/use?url=https://github.com/info-beamer/package-32c3-screens.git)

# 32c3 package (running on all the screens)

This is the code that ran on a single RPI2 during the [32c3](https://events.ccc.de/congress/2015/wiki/Static:Main_Page)
conference. I updated code and added images/videos while the visualization was running numerous times during the conference
without restarting anything. I wrote code on my own machine and committed it to a local git repository which I
then pushed to the [info-beamer hosted server](https://info-beamer.com/doc/building-packages#packageasagitrepositoryoninfobeamercom). 
That way info-beamer takes care of the rest and pushes all new content automatically to all configured devices and restarts
all services if required.

## Installation/Running

So there are three ways to use this repository:

 * You can fork it and create a new hosted service package that points to your new repository. Everytime you commit you then
 have to click the "Check for updates" button in the package page. If you want to do that, check the "Show advanced/expert
 options" in your account page. Then on the packages page click on "Add Package", then "Create from Url" and enter the
 clone url of your repository.

 * You can clone this repository locally and push it directly to the info-beamer hosted service. This is the recommended way
 to run this code because you can directly push your changes and see the result. This is the way the setup was running during
 32c3. To do this, again, check the "Show advanced/expert options" in your account page. Then click "Add Package" on the
 packages page and select "Create git repository". Follow the instructions on the package page. When done, you should be able
 to just use `git push info-beamer master` after committing changes.

 * You can run the complete visualization without using the hosted service by just cloning it to your PI and then running
 the info-beamer pi program. Since the package uses the configuration feature of info-beamer hosted you have to create some
 `config.json` files manually that are otherwise automatically created. Consult the `config.json.example` files for
 that. You also have to manually start all associated python services. Look out for the `service` files in the various
 subdirectories.

To add new images, just create new JPEG files prefixed with either `img_` or `ads_`. Adding videos requires you to
edit the `playlist.json` file. New content for the ticker can be added by editing `scroll.txt`.

## Notes

 * During the conference I edited some of the `module_*` lua code and pushed updates to the PI. Code in `node.lua`
 monitors all lua files prefixed with `module_` and reloads them every time they change.

 * During the conference I had a development PI connected to the PI 7" screen to test my changes before pushing them to
 "production". You can just setup multiple repositories on info-beamer hosted so you can just do
 `git push info-beamer-test master`.

 * This code doesn't use any child nodes for performance reasons. It's only using a single top level node. To make it more
 modular I wrote a small module that makes it easier to split code into logical parts. Have a look at `node.lua` for
 that.
