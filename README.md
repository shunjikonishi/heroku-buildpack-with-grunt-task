Heroku buildpack: Run grunt task in build process
============================================

Supported Grunt versions: 0.3 and 0.4.
See the Grunt [migration guide](https://github.com/gruntjs/grunt/wiki/Upgrading-from-0.3-to-0.4) if you are upgrading from 0.3.

This is a fork of [heroku-buildpack-nodejs-grunt](https://github.com/mbuchetics/heroku-buildpack-nodejs-grunt).
Using this buildpack you do not need to commit the results of your Grunt tasks (e.g. minification and concatination of files), keeping your repository clean.

After all the default Node.js and npm build tasks have finished, the buildpack checks if a Gruntfile (`Gruntfile.js`, `Gruntfile.coffee`or `grunt.js`) exists and executes the `heroku` task by running `grunt heroku`. For details about grunt and how to define tasks, check out the [offical documentation](http://gruntjs.com/getting-started). You must add grunt to the npm dependencies in your `package.json` file.
If no Gruntfile exists, this buildpack does nothing.

The purpose of this buildpack is only running grunt task in build process.  
So this buildpack doesn't include node modules in slug.

You must use [heroku-buildpack-multi](https://github.com/ddollar/heroku-buildpack-multi) to combine it with a real buildpack.

Usage
-----
To use this buildpack, you should prepare .buildpacks file that contains this buildpack url and your real buildpack url.  

    $ ls
    .buildpacks
    package.json
    Gruntfile.js
    ...
    
    $ cat .buildpacks
    https://github.com/shunjikonishi/heroku-buildpack-with-grunt-task
    https://github.com/heroku/heroku-buildpack-scala

    $ heroku create --buildpack https://github.com/ddollar/heroku-buildpack-multi

    $ git push heroku master
    ...

You can verify your grunt task result by following command.

    $ heroku run bash

