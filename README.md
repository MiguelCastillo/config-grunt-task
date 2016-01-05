# config-grunt-task
> Grunt task configuration loader that helps organize your `Gruntfile.js` tasks configuration.

The idea is to modularize your task settings. I personally like to create a folder called `tasks`, which contains all the different configurations for each grunt task in separate JavaScript files. But `config-grunt-task` is flexible enough to let you customize how you slice your pie.

This module goes really well with [load-grunt-task](https://github.com/sindresorhus/load-grunt-tasks).

This [article by Thomas Boyt](http://www.thomasboyt.com/2013/09/01/maintainable-grunt.html) is good literature on the topic.

## Using it...

First things first, you need to install this module.

```
npm install --save-dev config-grunt-task
```

Then you can `require`it in your `Gruntfile.js` to load your taks configuration files.

Take a look at this [examples](EXAMPLES.md) to get you up and running.

## License

Licensed under MIT
