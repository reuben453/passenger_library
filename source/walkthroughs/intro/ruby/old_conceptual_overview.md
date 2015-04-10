---
title: Understanding Phusion Passenger
section: intro
---
# Understanding Phusion Passenger

You've heard that Phusion Passenger is an "application server", but what is that exactly? Why do you need Passenger to run your Ruby application, and how does it compare to other software?

Well, Ruby web applications typically are not directly able to listen on the Internet. They need a piece of software that provides Internet HTTP transaction handling. That piece of software is the application server.

The Ruby ecosystem has multiple application servers, all with different features. Passenger is a popular server, and other popular servers include Unicorn and Puma. Because the Ruby community has embraced a standard interface called [Rack](http://rack.github.io/), it is very easy to migrate from one application server to another.

## Versus other software

### Vs Unicorn and Puma

Unicorn and Puma are application servers, just like Passenger. If you already use Puma and Unicorn, then switching to Passenger is almost effortless. The inverse is also true, so there is no vendor lock-in.

Passenger is much easier to use than Unicorn and Puma, and is also much more ambitious and provides [a lot more features](../../../guides/). Unicorn and Puma are very minimalist compared to Passenger, and only provide HTTP transaction handling as well as limited amounts of problem management. In contrast, Passenger automates many of the tasks that you have to do manually when using Unicorn and Puma, has more advanced process management and resource management, supports direct Nginx and Apache integration, has more security features, etc.

### Vs "rails server"

"rails server" isn't an application server by itself. It's just a thin wrapper that launches your Rails app in an application server.

### Vs Nginx and Apache

Nginx and Apache are web servers. They provide HTTP transaction handling and serve static files. However, they are not Ruby application servers and cannot run Ruby applications. That is why Nginx and Apache are used in combination with an application server (Passenger, Unicorn, Puma).

### Vs Capistrano

Capistrano is an application release automation tool. When releasing a new version of your web application, there are actions that need to be performed, such as uploading your application code to your servers, running a command to install your gem bundle, restarting processes, etc. Capistrano allows you to automate these actions.

Capistrano is not a server that provides HTTP transaction handling, so it does not replace application servers or web servers. Instead, you are supposed to use Capistrano in combination with them. For example, Capistrano scripts typically contain instructions to restart the application server after a new application version has been released.

## What Passenger doesn't do

Passenger follows the Unix philosophy of doing a small number of things, but doing them well. So there are a number of things that are (currently) outside Passenger's scope. Passenger may or may not take care of some of these some time in the future.

 * **Setting up a server with an operating system**<br>
   Passenger assumes that you already have a server with an working operating system on it. Passenger is not a hosting service. It is software that is to be installed on a server.<br>
   However, the Passenger Library contains excellent [documentation on setting up a server](../../deploy/ruby/).
 * **Installing Ruby**<br>
   To run Ruby apps on Passenger, you must already have Ruby installed. Passenger doesn't do that for you. Passenger doesn't care how you install Ruby though; you sometimes just need to tell Passenger where Ruby is.<br>
   Having said that, the Passenger Library contains excellent [documentation on installing Ruby during a production deployment](../../deploy/ruby/).
 * **Transferring the application code and files to the server**<br>
   Passenger does not transfer the application code and files to the server for you. To do this, you should use something like Capistrano. Passenger assumes that the application code and files are already on the server, and does not care which tool you use to make that so.<br>
   The Passenger Library contains [documentation on automating releases using Capistrano](../../../guides/capistrano.html).
 * **Installing application dependencies**<br>
   Passenger does not install your application's dependencies for you. That job belongs to Capistrano and Bundler.
 * **Managing the database**<br>
   If your application requires a database, then Passenger does not install that database for you, nor does it sets up database accounts and tables for you. They must already be set up by the time you deploy your application to Passenger.
 * **Managing auxiliary daemons and services**<br>
   If your application requires additional daemons and services, e.g. Memcached or Redis, then Passenger does not manage those. They must already be running.

## Next step

Now that you've seen Passenger in action and understand what it is, it's time to get acquainted with the basic features.

A key feature in Phusion Passenger is [process management](process_management.html). This allows Phusion Passenger to keep your application stable and to maximize performance.

<a href="process_management.html" class="btn btn-primary btn-lg">Continue &raquo;</a>

<a href=".">&laquo; Back to table of contents</a>