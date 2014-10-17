# grunt-filerev-replace

> Replace references to grunt-filerev files.

## Getting Started
This plugin requires Grunt `~0.4.2`

If you haven't used [Grunt](http://gruntjs.com/) before, be sure to check out the [Getting Started](http://gruntjs.com/getting-started) guide, as it explains how to create a [Gruntfile](http://gruntjs.com/sample-gruntfile) as well as install and use Grunt plugins. Once you're familiar with that process, you may install this plugin with this command:

```shell
npm install grunt-filerev-replace --save-dev
```

Once the plugin has been installed, it may be enabled inside your Gruntfile with this line of JavaScript:

```js
grunt.loadNpmTasks('grunt-filerev-replace');
```

## The "filerev_replace" task

### Overview
In your project's Gruntfile, add a section named `filerev_replace` to the data object passed into `grunt.initConfig()`. See the test files for a working example.

```js
grunt.initConfig({
  // Filerev all images
  filerev: {
    images: { src: 'tmp/assets/images/**/*' }
  },

  // Replace references to the images in the compiled js and css files, and the html views
  filerev_replace: {
    options: {
      assets_root: 'tmp/assets/'
    },
    compiled_assets: {
      src: 'tmp/assets/compiled/*.{css,js}'
    },
    views: {
      options: {
        views_root: 'tmp/views/'
      },
      src: 'tmp/views/**/*.html'
    }
  }
});
```

### Addendum
Lightly tested fix included in this fork allowed the following configuration of a Yeoman generated project I've extended to work across subfolders. This need arose from a project directory structure that was not flat while using Firebase hosting for an Angularfire project. Upon deployment cached views were causing a problem. The original only worked for me on files contained in the views_root. The commented out line was prepending the src path in its comparisons. I've been able to use this configuration to build a functioning deploy, but more testing is required.

```js
grunt.initConfig({
  // Filerev all images
    filerev: {
        dist: {
            src: [
              '<%= yeoman.dist %>/states/**/*.html', 
              '<%= yeoman.dist %>/scripts/{,*/}*.js',
              '<%= yeoman.dist %>/styles/{,*/}*.css',
              '<%= yeoman.dist %>/images/{,*/}*.{png,jpg,jpeg,gif,webp,svg}',
              '<%= yeoman.dist %>/styles/fonts/*'
            ]
        }
    },
    filerev_replace: {
        options: {
        	assets_root: '<%= yeoman.dist %>'
        },
        dist: { 
        	options: {
        		views_root: '<%= yeoman.dist %>'
        	},
        	src: '<%= yeoman.dist %>/{,**/}*.{html,css,js}'
        }
    }
});
```

### Options

#### options.assets_root
Type: `String`
Required

The root path from where assets are served by the web application.

#### options.views_root
Type: `String`
Default value: assets_root

The root path from where views are served by the web application.

## Contributing
In lieu of a formal styleguide, take care to maintain the existing coding style. Add unit tests for any new or changed functionality. Lint and test your code using [Grunt](http://gruntjs.com/).

## Release History
_(Nothing yet)_
