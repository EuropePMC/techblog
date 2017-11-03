---
layout: post
title:  "Remote debug Ruby on Rails running in a Docker container using RubyMine"
date:   2017-11-03
categories: rails
---

[RubyMine](https://www.jetbrains.com/ruby/) brings a sophisticated [debugger](https://www.jetbrains.com/ruby/features/ruby_debugger.html) with a graphical UI for Ruby, JS, and CoffeeScript. You can set breakpoints and run your code step by step with all the information at your fingertips, without having to modify your code as [Pry](https://github.com/pry/pry).

This article is written about how one can use RubyMine to remote debug a Ruby on Rails application that even runs inside a Docker container.

# Versions of software in our environment

 - RubyMine 2017.2.4 (Build #RM-172.4155.44, built on September 26, 2017)
 - Ruby inside docker (ruby 2.4.2p198 (2017-09-14 revision 59899) [x86_64-linux])
 - Ruby SDK and Gems used by RubyMine (ruby-2.4.2-p198)

Note: for Ruby SDK used by RubyMine, we are just using a local Ruby interpreter /usr/bin/ruby, not a remote one. (See below)

![Ruby SDK and Gems settings 1][sdk1]

![Ruby SDK and Gems settings 2][sdk2]

# Below are the detailed steps as a demo

## 1. Start the docker container

    docker run --name rails-demo -p 1234:1234 -p 3080:3000 -it ruby bash

## 2. Steps inside the docker container

Be sure you have the following gems in your Gemfile, and better to comment out gem pry-byebug if it's there, to avoid possible interference.

    # gem 'pry-byebug'
    gem 'debase', '0.2.2.beta10'
    gem 'ruby-debug-ide'

Update the dependencies of your application if necessary

    bundle install

Start your rails server

    /home/hello_rails# rdebug-ide --host 0.0.0.0 --port 1234 --dispatcher-port 26162 -- bin/rails s

# 3. Remote debug from RubyMine
Now start RubyMine, Run -> Debug... -> Edit Configurations...

Click plus sign '+' to add new configuration, and choose Ruby remote debug.

![RubyMine Debuger Settings][debugger]

Fill the form as shown above and click the Debug button. Now you'll see in the docker container the Rails server gets started:

    /home/hello_rails# rdebug-ide --host 0.0.0.0 --port 1234 --dispatcher-port 26162 -- bin/rails s
    Fast Debugger (ruby-debug-ide 0.6.0, debase 0.2.2.beta10, file filtering is supported) listens on 0.0.0.0:1234
    => Booting Puma
    => Rails 5.1.4 application starting in development 
    => Run `rails server -h` for more startup options
    Puma starting in single mode...
    * Version 3.10.0 (ruby 2.4.2-p198), codename: Russell's Teapot
    * Min threads: 5, max threads: 5
    * Environment: development
    * Listening on tcp://0.0.0.0:3000
    Use Ctrl-C to stop

Now, you can set breakpoints in RubyMine, and start remote debugging it :-)

Go to browser with URL: http://localhost:3080/say/hi (Note port 3080 is mapped from 3000, see above the command of starting the docker container)

The breakpoint is hit as shown below, where you can inspect variables, etc.

![RubyMine breakpoints][breakpoints]

One more caveat worth mentioning is that you need to be sure the web server puma starts in single mode. For me the cluster mode does not work for remote debugging, where you'll have errors like "terminating timed out worker". For development, single mode should be good enough.

# References:

 1. [JetBrains RubyMine remote debugging](https://www.jetbrains.com/help/ruby/remote-debugging.html)
 2. [Running the Rails debugger in a Docker container using RubyMine](http://bzzt.io/posts/running-the-rails-debugger-in-a-docker-container-using-rubymine)

  [sdk1]: {{ site.baseurl }}/images/posts/rubymine-remote-debug-rails-in-docker/sdk1.png
  [sdk2]: {{ site.baseurl }}/images/posts/rubymine-remote-debug-rails-in-docker/sdk2.png
  [debugger]: {{ site.baseurl }}/images/posts/rubymine-remote-debug-rails-in-docker/debugger-settings.png
  [breakpoints]: {{ site.baseurl }}/images/posts/rubymine-remote-debug-rails-in-docker/breakpoints.png
