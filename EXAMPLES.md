# Examples

### First, let's look at a setup where `config-grunt-task` loads all the tasks in you `tasks` folder.

```
module.exports = function(grunt) {
  "use strict";

  require("load-grunt-tasks")(grunt);
  var pkg = require("./package.json");

  // Load up your tasks in the `tasks` folder.
  var taskConfig = require("config-grunt-task")(grunt, "./tasks");

  // Naively set `pkg`. But please feel free to use your merging module of choice
  taskConfig.pkg = pkg;

  // Now just call your grunt initialization step.
  grunt.initConfig(taskConfig);

  grunt.registerTask("build", ["eslint:all"]);
  grunt.registerTask("test", ["connect:test", "mocha:test"]);
};
```

### Second, let's look at a setup where `config-grunt-task` loads specific tasks. Some people like more control over their stuff! I am certainly not judging you. :)

```
module.exports = function(grunt) {
  "use strict";

  require("load-grunt-tasks")(grunt);
  var pkg = require("./package.json");

  // Get your task configurator
  var taskConfig = require("./config-grunt-task");

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
