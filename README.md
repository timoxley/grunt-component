# grunt-component

Super thin wrapper of `grunt` task for `component-build`.
It simply spawn `make build`. That's basically it :)

### Sample gruntfile

**Make sure you have `Makefile` placed at your component root.**

This `watch` task will compile `stylus` and `coffeescript`
build component, then reload the browser.

`grunt.js`

```
module.exports = function(grunt) {

  // Project configuration.
  grunt.initConfig({
    lint: {
      files: ['grunt.js', 'src/coffee/*.coffee', 'template.html', 'src/stylus/*.styl']
    },
    reload: {
        port: 35729,
        liveReload: {},
        proxy: {
            host: 'localhost',
            port: "3000"
        }
    },
    watch:{
        files:'<config:lint.files>',
        tasks:'stylus coffee component reload'
    },
    coffee: {
      compile: {
          options: {
            bare: true
          },
          files: {
            "index.js": "src/coffee/index.coffee"
          }
        }
    },
    stylus: {
      compile: {
        files: {
          'page-turn.css': 'src/stylus/page-turn.styl',
        }
      }
    }
  });

  // Default task.
  grunt.registerTask('default', 'lint qunit');
  grunt.loadNpmTasks('grunt-contrib');
  grunt.loadNpmTasks('grunt-reload');

  grunt.loadNpmTasks('grunt-component');

};
```
