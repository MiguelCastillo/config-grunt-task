# config-grunt-tasks
> Grunt task configuration loader that helps organize your `Gruntfile.js` tasks configuration.

The idea is to modularize your task settings. I personally like to create a folder called `tasks`, which contains all the different configurations for each grunt task in separate JavaScript files. But `config-grunt-tasks` is flexible enough to let you customize how you slice your pie.

This module goes really well with [load-grunt-tasks](https://github.com/sindresorhus/load-grunt-tasks).

This [article by Thomas Boyt](http://www.thomasboyt.com/2013/09/01/maintainable-grunt.html) is good literature on the topic.


## Using it...

First things first, you need to install this module.

```
npm install --save-dev config-grunt-tasks
```

Then you can `require`it in your `Gruntfile.js` to load your tasks configuration files.


## Conventions

`config-grunt-tasks` uses conventions for mapping task configurations to file names. That is to say that your `eslint` taks will require a file called `eslint.js` in your `tasks` directory. This `eslint.js` will export the JSON structure, or a function that is called to get the JSON structure that contains all the corresponding `eslint` settings.  If `eslint.js` exports a function, then that function will be called with the current instance of Grunt as the first argument. Please feel free to checkout [bit-bundler](https://github.com/MiguelCastillo/bit-bundler/tree/master/tasks) for a sample setup.


## Examples

#### First,
let's look at a setup where `config-grunt-tasks` loads all the tasks in you `tasks` folder.

``` javascript
module.exports = function(grunt) {
  "use strict";

  require("load-grunt-tasks")(grunt);
  var pkg = require("./package.json");

  // Load up your tasks in the `tasks` folder.
  var taskConfig = require("config-grunt-tasks")(grunt, "./tasks");

  // Naively set `pkg`. But please feel free to use your merging module of choice
  taskConfig.pkg = pkg;

  // Now just call your grunt initialization step.
  grunt.initConfig(taskConfig);

  grunt.registerTask("build", ["eslint:all"]);
  grunt.registerTask("test", ["connect:test", "mocha:test"]);
};
```

#### Second,
let's look at a setup where `config-grunt-tasks` loads specific tasks. Some people like more control over their stuff! I am certainly not judging you. :)

``` javascript
module.exports = function(grunt) {
  "use strict";

  require("load-grunt-tasks")(grunt);
  var pkg = require("./package.json");

  // Get your task configurator
  var taskConfig = require("config-grunt-tasks");

  // Load each task configuration individually
  grunt.initConfig({
    pkg: pkg,
    connect: taskConfig(grunt, "./tasks/connect.js").connect,
    mocha: taskConfig(grunt, "./tasks/mocha.js").mocha,
    watch: taskConfig(grunt, "./tasks/watch.js").watch,
    eslint: taskConfig(grunt, "./tasks/eslint.js").eslint,
    concurrent: taskConfig(grunt, "./tasks/concurrent.js").concurrent,
    uglify: taskConfig(grunt, "./tasks/uglify.js").uglify,
    release: taskConfig(grunt, "./tasks/release.js").release
  });

  grunt.registerTask("build", ["eslint:all"]);
  grunt.registerTask("test", ["connect:test", "mocha:test"]);
};
```


## License

Licensed under MIT
