# grunt-contrib-pdomap

## Install

You need [nodejs & npm installed](https://nodejs.org/en/download/package-manager/). If you php project is not yet configured with npm run `npm init` into the project root.


- [install grunt](http://gruntjs.com/installing-grunt) : `npm install -g grunt-cli && npm install grunt --save-dev`
- [install grunt watch](https://github.com/gruntjs/grunt-contrib-watch) : `npm install grunt-contrib-watch --save-dev`
- [install grunt pdoMap](https://github.com/ichiriac/grunt-contrib-pdomap) : `npm install grunt-contrib-pdomap --save-dev`

## Quick-start configuration snipet

In order to run grunt you need a `gruntfile.js` at the root of your project. Take this snippet and paste it into this file, and configure according :

```js
module.exports = function(grunt) {
  grunt.initConfig({
    pkg: grunt.file.readJSON('package.json'),
    pdomap: {
      options: {
        // THE LOCAL CONNECTION (http://php.net/manual/fr/pdo.construct.php)
        dsn: 'mysql:host=127.0.0.1,dbname=tests',
        user: 'root',
        pwd: '',
        init: [
          // JUST A SAMPLE
          "SET NAMES 'UTF8'"
        ],
        // AFTER SCANNING AND GENERATING FILES, REFRESH DATABASE STRUCTURE
        sync: true,
        // VERBOSE MODE (in order to know what was done)
        verbose: true,

      },
      build: {
        // that you put your models into the src/models folder
        path: 'src/models',
        core: {
          // where to create the storage file
          path: 'src/Storage.php',
          // how to name the storage class
          class: 'YourNamespace/Storage'
        }
      }
    },
    watch: {
      // say where model files are located
      files: ['src/models/*.php'],
      // says to run build > alias of pdoMap:build
      tasks: ['build']
    }
  });

  // Load the plugins
  grunt.loadNpmTasks('grunt-contrib-watch');
  grunt.loadNpmTasks('grunt-contrib-pdomap');

  // Default task(s).
  grunt.registerTask('default', ['watch']);
  grunt.registerTask('build', ['pdomap:build']);

};
```

Now you are able to run it from the cli :

- `grunt` : run this and start developping. At each file change, it will trigger the build system

- `grunt build` : It will build once all model classes and sync the database

