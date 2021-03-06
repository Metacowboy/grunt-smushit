# grunt-smushit [![Build Status](https://secure.travis-ci.org/heldr/grunt-smushit.svg)](http://travis-ci.org/heldr/grunt-smushit)

Grunt plugin to remove unnecessary bytes of PNG and JPG using reSmush.it

> reSmush.it is a FREE alternative to Yahoo Smush.it (deprecated on March 2015). This tool provides a online way to optimize pictures size via a documented webservice.

[Read more about reSmush.it](http://resmush.it/)

Prefer Gulp? [gulp-smushit](https://github.com/heldr/gulp-smushit)

## Getting Started
This plugin requires Grunt `0.4.x`

If you haven't used [Grunt](http://gruntjs.com/) before, be sure to check out the [Getting Started](http://gruntjs.com/getting-started) guide, as it explains how to create a [Gruntfile](http://gruntjs.com/sample-gruntfile) as well as install and use Grunt plugins. Once you're familiar with that process, you may install this plugin with this command:

```shell
npm install grunt-smushit --save-dev
```

Once the plugin has been installed, it may be enabled inside your Gruntfile with this line of JavaScript:

```js
grunt.loadNpmTasks('grunt-smushit');
```

## The "smushit" task

### Overview
In your project's Gruntfile, add a section named `smushit` to the data object passed into `grunt.initConfig()`.

```js
grunt.initConfig({
  smushit: {
    mygroup: {
      src: ['tests/img/**/*.png','tests/img/**/*.jpg'],
      dest: 'tests/img/min'
    }
  }
});
```

### Options

#### options.service
Type: `String`
Default value: `null`
Call another service instead of Yahoo Smushit

#### options.verbose
Type: `boolean`
Default value: `true`
Show image compressing rate log

### Usage Examples

#### Output Folder
Move your files to a target folder (should not be into the same).

```js
grunt.initConfig({
  smushit: {

    // catch all files from a single folder
    group1: {
      src: 'tests/img',
      dest: 'tests/opt_img'
    },

    // filter by filetype
    group2: {
      src: ['tests/img/**/*.png','tests/img/**/*.jpg'],
      dest: 'tests/img/min'
    },

    // set each file
    group3:{
        src: ['tests/img/logo.png','tests/img/whatever.png'],
        dest: 'tests/img/min'
    }

  }
});
```

#### Replace files
Be safe to replace all of your old files with this option.

```js
grunt.initConfig({
  smushit: {

    // a single directory
    group1: {
      src: 'tests/img'
    },

    // filter by filetype
    group2: {
      src: ['tests/img/**/*.png','tests/img/**/*.jpg']
    },

    //replace recursive
    group3: {
      src: ['tests/img/logo.png','tests/img/tellme.jpg']
    }

  }
});
```

#### Work with a nested folder
Recursively walk into folders and smushit files

```js
grunt.initConfig({
  smushit: {

    // catch all files from a nested folder
    group1: {
      src: 'tests/nested/img',
      dest: 'tests/opt_img'
    },

    // filter files in a nested folder by filetype
    group2: {
      src: ['tests/nested/img/**/*.png','tests/nested/img/**/*.jpg'],
      dest: 'tests/opt_img'
    },

    // retrieve files in a nested folder by file name
    group3: {
      src: ['tests/nested/img/**/southpark.png','tests/nested/img/**/southpark.jpg'],
      dest: 'tests/opt_img'
    },
  }
});
```

#### Provide multiple source
Smushit one folder, or many of them

```js
grunt.initConfig({
  smushit: {

    // catch all files from a nested folder
    group1: {
      src: ['tests/img1', 'tests/img2'],
      dest: 'tests/opt_img'
    },

    // filter files in a folder by filetype
    group2: {
      src: ['tests/img1/**/*.png','tests/img2/**/*.jpg'],
      dest: 'tests/opt_img'
    },

    // retrieve files in a folder by file name
    group3: {
      src: ['tests/img1/**/southpark.png','tests/img2/**/southpark.jpg'],
      dest: 'tests/opt_img'
    },
  }
});
```

#### Use of cwd
Provide your base directory

```js
grunt.initConfig({
  smushit: {

    // src folder is 'tests/img' and dest is 'tests/opt_img'
    group1: {
      cwd: 'tests'
      expand: true,
      src: 'img',
      dest: 'tests/opt_img'
    },

    // multiple src folders: src folder is ['tests/img1', 'tests/img2'] and dest is 'tests/img/min'
    group2: {
      cwd: 'tests'
      expand: true,
      src: ['img1/**/*.png','img2/**/*.jpg'],
      dest: 'tests/img/min'
    },
  }
});
```


#### Your own service
There is an option that you can set your own image optimizer service. Its a good alternative if you don't want to wait for smush.it web service latency.

```js
grunt.initConfig({
  smushit: {
    options: {
      service: 'http://myimgopt.com/exec'
    },
    mygroup: {
      src: ['tests/img/**/*.png','tests/img/**/*.jpg'],
      dest: 'tests/img/min'
    }
  }
});
```

## Contributing

```cli
$ git clone git://github.com/heldr/grunt-smushit.git
$ cd grunt-smushit
$ npm install
$ npm test
```
NOTE: Be sure to keep up to date the plugin tests and jshint code quality.

## Release History
  * 2015-09-05   v2.0.0   Use resmush.it due Yahoo Smushit deprecation
  * 2014-05-19   v1.3.0   Pass node-smushit options through grunt file
  * 2014-03-30   v1.2.1   Bugfix. Fixes [issue 29](https://github.com/heldr/grunt-smushit/issues/29)
  * 2014-03-03   v1.2.0   Use cwd only for source files, following the [grunt pattern][grunt-cwd-pattern]
  * 2013-07-15   v1.1.0   Support nested folder structure, support for multiple source folders
  * 2013-07-15   v1.1.0   Enable the use of cwd parameter
  * 2013-06-16   v1.0.0   Rewrite task on top of [grunt-init-gruntplugin][grunt-init-gruntplugin]
  * 2013-05-26   v0.4.2   Add support to different service #16

## Credits
  * [node-smushit][node-smushit]

## License

MIT License
(c) [Helder Santana](http://heldr.com)

[node-smushit]: https://github.com/colorhook/node-smushit
[grunt-init-gruntplugin]: https://github.com/gruntjs/grunt-init-gruntplugin
[grunt-cwd-pattern]: http://gruntjs.com/configuring-tasks#building-the-files-object-dynamically
