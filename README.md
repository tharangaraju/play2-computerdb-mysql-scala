Play framework 2 scala computer-database sample application with mysql
============================

This project is a fork of the openshift-play2-computerdb repo, which took the computer-database sample project, scala version, and modified it to work with a mysql database.

This project was tested on Play 2.1.1, Scala 2.10.0, MySQL, 5.5.29, and Java 1.6_0_45 

How to install and run
----------------------------
* Modify conf/application.conf and specify mysql url, port, database, user, and pass
* If necessary, update your sbt.version in project/build.properties
* Ensure MySQL is running and that the database was created
* From the root directory run 'play -DapplyEvolutions.default=true start'
* On subsequent runs you don't need to applyEvolutions, so 'play start' should work
for production mode, or 'play run' for developer mode.
* Afterwards, the sample should work just like the original play sample except
now changes will persist in between server shutdowns

Demo
----------------------------
View a live demo running at http://dev1.minh.io

(Eventually I'll update this to have it run on Heroku...)


List of changes needed to port computer-database sample app from H2 to mysql
----------------------------

conf/evolutions/default/1.sql

* added engine=innodb, to enable referential integrity
* replaced sequences with autoincrement for id fields
* replaced 'SET REFERENTIAL_INTEGRITY' command with 'SET FOREIGN_KEY_CHECKS'
* replaced timestamp fields with datetime

conf/evolutions/default/2.sql

* splitted the computer data between 2.sql and 3.sql file (avoid bug in evolutions running on mysql)

models/Models.scala

* removed 'nulls last' from Computer.list sql query
* modified Computer.insert to skip id field (because is auto-assigned by mysql)

Licence
----------------------------
This project is distributed under [Apache 2 licence](http://www.apache.org/licenses/LICENSE-2.0.html). 