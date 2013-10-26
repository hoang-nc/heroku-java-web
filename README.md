Heroku buildpack: Java web
=========================

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpack) for Java web apps.

It uses OpenJDK 1.7 and [Webapp Runner](https://github.com/jsimone/webapp-runner) to deploy Java web.

It not compile/build you code on server so you have to build in your pc, this buildpack focus to Netbean's users for easy deploy their Java web projects.


Usage
-----
Build your project by "Run - Build Project (F11)" in Netbean IDE, after build successful there are 2 folder in your project: <b>build</b> and <b>dist</b>

		HELLOJSP
		├───build
		│   ├───empty
		│   ├───generated-sources
		│   │   └───ap-source-output
		│   └───web
		│       ├───META-INF
		│       └───WEB-INF
		│           └───classes
		├───dist
		├───nbproject
		│   └───private
		├───src
		│   ├───conf
		│   └───java
		└───web
			├───META-INF
			└───WEB-INF

You have to keep <b>build</b> folder for deploying, with <b>dist</b> folder you should add to [git ignore](https://help.github.com/articles/ignoring-files) for saving deploy time.

Create new app with argument: --buildpack https://github.com/nchoang/heroku-java-web or override old buildpack (below).

Using git push you app to server, all done!

Example usage:

    $ ls
    build  build.xml  dist  nbproject  src  web

    $ heroku create --stack cedar --buildpack https://github.com/nchoang/heroku-java-web

    $ git push heroku master
    -----> Fetching custom git buildpack... done
    -----> Java web app detected
    -----> Installing OpenJDK 1.7... done
    -----> Creating boot.sh... done
    -----> Creating Procfile... done
    -----> Discovering process types
           Procfile declares types -> web
    
    -----> Compiled slug size: 67.9MB
    -----> Launching... done, v7
           http://*.herokuapp.com deployed to Heroku
           
Override old buildpack
----------------------

    $ heroku config:set JAVA_HOME=/app/.jdk
    $ heroku config:set JAVA_OPTS=-Xmx1024m -Xss512m -XX:+UseCompressedOops
    $ heroku config:set PATH=/app/.jdk/bin:/usr/local/bin:/usr/bin:/bin
    $ heroku config:set WEBAPP_RUNNER_OPTS=--session-store memcache
    $ heroku config:set BUILDPACK_URL=https://github.com/nchoang/heroku-java-web


Hacking
-------

To use this buildpack, fork it on Github.  Push up changes to your fork, then create a test app with `--buildpack <your-github-url>` and push to it.


License
-------

Licensed under the MIT License. See LICENSE file.
