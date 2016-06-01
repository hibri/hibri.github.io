---
id: 2013
title: My NodeJS development workflow
date: 2014-12-10T13:43:19+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/?p=2013
permalink: /2014/12/10/my-nodejs-development-workflow/
categories:
  - Uncategorized
---
I&#8217;m building a NodeJS + Angular application and there are a few things I want a smooth dev workflow and improve developer happiness. Yay !!

  1. Run the node server process and restart automatically when I make changes
  2. Concatenate my client side JS code, and merge libraries such as angular, jquery and bootstrap.
  3. I don&#8217;t want to check in concatenated files.
  4. I don&#8217;t want to check in modules or libraries, even for client side scripts
  5. I want to catch typos and style violations.
  6. I want tests to run in the background.

[Grunt](http://gruntjs.com/) is the task runner I&#8217;m using to automate the tasks. Let&#8217;s look at each of these tasks.

Automate the NodeJS server process with [nodemon](https://github.com/remy/nodemon).

<pre style="padding-left: 30px;">npm install --save-dev nodemon</pre>

Now, run

<pre style="padding-left: 30px;">nodemon</pre>

Eventually, you&#8217;ll want to trigger nodemon through grunt. Get the [grunt-nodemon](https://www.npmjs.com/package/grunt-nodemon) plugin. The plugin registration and the Grunt config is below.

<pre style="padding-left: 30px;">grunt.loadNpmTasks('grunt-nodemon');

</pre>

<pre style="padding-left: 30px;">nodemon: {
    dev: {
        script: 'bin/www',
        ignore:  ['node_modules/**','bower_components/**','public/**']
    }
}</pre>

I&#8217;ve configured nodemon to ignore javascript that is not my code, and ignore changes to client side javascript. The path to the node server script is set in the script property. Since I&#8217;ve used express to create an app, this is &#8216;bin/www&#8217;.

Great, now executing **_grunt nodemon_**  will watch for changes and restart the server.

Next, I want to avoid all those pesky typos, misplaced semi-colons and get into the habit of writing good Javascript. I&#8217;ll use [JSHint](http://jshint.com/).

<pre style="padding-left: 30px;">npm install --save-dev grunt-contrib-jshint</pre>

Configure JSHint as below,

<pre style="padding-left: 30px;">grunt.loadNpmTasks('grunt-contrib-jshint');

</pre>

<pre style="padding-left: 30px;">jshint: {
    all: ['Gruntfile.js', 'lib/**/*.js', 'test/**/*.js','public/javascripts/app/**/*.js']
}</pre>

This configures JSHint to run on my tests, client side javascript and server code.

As with nodemon, I want JSHint running in the background and checking my code as I type and save files. This gives me quick feedback. Because JSHint doesn&#8217;t do this, I&#8217;ll introduce another plugin to the Gruntfile.

This is the [grunt watch](https://www.npmjs.com/package/grunt-contrib-watch) plugin, which will watch for changes in my source directory and run other Grunt tasks.

<pre style="padding-left: 30px;">npm install --save-dev grunt-contrib-watch</pre>

Configure grunt-watch as below,

<pre style="padding-left: 30px;">grunt.loadNpmTasks('grunt-contrib-watch');</pre>

<pre style="padding-left: 30px;">watch: {
 scripts: {
 files: ['**/*.js','!node_modules/**','!bower_components/**','!public/javascripts/dist/**'],
 tasks: ['jshint']
 }
}</pre>

This sets up grunt-watch to watch over all of my code. Ignore directories by placing an exclamation mark before the path spec.

Great, now if I execute _**grunt watch**_ on the command line, it will start watching for changes and run jshint when a change is detected. Sweet.

There is a catch though. I want to run nodemon and watch at the same time. I could run both in separate shells, but that would mean switching back and forth.

Let&#8217;s introduce [grunt-concurrent](https://www.npmjs.com/package/grunt-concurrent). This executes grunt tasks concurrently. Now I can run nodemon and watch at the same time.

<pre style="padding-left: 30px;">npm install --save-dev grunt-concurrent</pre>

Configure as below;

<pre style="padding-left: 30px;">grunt.loadNpmTasks('grunt-concurrent');


</pre>

<pre style="padding-left: 30px;">concurrent: {
    dev: {
        tasks: ['nodemon', 'watch'],
        options: {
            logConcurrentOutput: true
        }
    }
}</pre>

The config above, tells grunt-concurrent to run nodemon and watch. Both tasks are grouped logically under a &#8220;dev&#8221; subtask.

If I execute _**grunt concurrent**_ on the command line, I&#8217;ll have my server restarting automatically and JSHint watching my code. To reduce what I need to type even more, I&#8217;ll set up grunt to run this task as default

<pre style="padding-left: 30px;">grunt.registerTask('default', ['concurrent']);</pre>

All I need to do is type &#8220;grunt&#8221; and have it do all the work done for me.

This gives me a  basic framework to add other tasks. Grunt allows me to group tasks. For example, I want to group all of my build time tasks as one. My build time tasks are to run jshint, run tests, merge libraries like angular and concatenate client side javascript.

<pre style="padding-left: 30px;">grunt.registerTask('build', ['jshint','karma','concat','bower_concat']);</pre>

Instead of watch running JSHint only, let&#8217;s change it to run the _**build**_ task.

<pre style="padding-left: 30px;">watch: {
 scripts: {
 files: ['**/*.js','!node_modules/**','!bower_components/**','!public/javascripts/dist/**'],
 tasks: ['build']
 }
}</pre>

Here is the complete Gruntfile <https://gist.github.com/hibri/6ccd0aef805353dc8260>

In addition to the tasks described above, I&#8217;ve also used the plugins listed below

  * grunt-bower-concat : merges all the dependencies installed via bower
  * grunt-contrib-concat : merges all the client side javascript I&#8217;ve written. This includes all my angularjs code.
  * grunt-karma : To run tests
  * grunt-bower-task : To run bower install through grunt.

You&#8217;ll also notice I&#8217;ve got the following task configured.

<pre style="padding-left: 30px;">grunt.registerTask('heroku:production', ['bower:install','concat', 'bower_concat']);</pre>

The deployment to Heroku uses the task. I want the concatenation to run when I push to production, so I don&#8217;t have to check in any build artefacts to source control.

Heroku doesn&#8217;t run Grunt natively during a deploy, but they do support [build packs](https://devcenter.heroku.com/articles/buildpacks). I&#8217;ve configured Heroku to use a nodejs buildpack with grunt support.

See <https://github.com/mbuchetics/heroku-buildpack-nodejs-grunt> for more.

This is the build framework I&#8217;m starting with, and most certainly will grow with the project. A way of sharing ignored files between tasks would be nice. There is some duplication already.

What&#8217;s your workflow ?