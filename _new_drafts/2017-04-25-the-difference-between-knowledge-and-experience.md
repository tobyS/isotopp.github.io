---
layout: post
status: publish
published: true
title: The difference between knowledge and experience
author: isotopp
author_login: kris
author_email: kristian.koehntopp@gmail.com
wordpress_id: 1562
wordpress_url: http://blog.koehntopp.info/?p=1562
date: '2017-04-25 15:14:34 +0200'
date_gmt: '2017-04-25 14:14:34 +0200'
categories:
- MySQL
tags: []
---
<p>[![](http://blog.koehntopp.info/wp-content/uploads/2017/04/Bildschirmfoto-2017-04-25-um-16.13.30.png)](https://twitter.com/kurorori/status/856860139038662659)[Tweet](https://twitter.com/kurorori/status/856860139038662659)&nbsp;via [Turbo&nbsp;Sandzwerg](https://twitter.com/Sandzwerg/status/856865559346073604) I have a&nbsp;personal story that goes very well with this tweet:<!--more--> Many years ago, I was doing database scalability at a company I have been working for. A new DBA needed to reload the a&nbsp;central MySQL master server in order for some config changes to /etc/my.cnf to go life. Back then it could happen that when you "service mysql stop" something, it could go fast or it could take rather long. You would not know beforehand. Starting and stopping the server kindly would create an outage of unpredictable length, and consequently loss of money, because the company would not have an incoming while this server reloaded. It was 2 in the afternoon, and the server was in good shape - I checked, and the redo log was at less than 400 MB in size. Also, critically, innodb\_flush\_log\_at\_trx\_commit was set at the proper value, the default 1. That is,&nbsp;commits would go properly to disk, to the redo log, on each commit. I knew from personal experience that this would be safe, and fast: a kill -9 on the mysql pid would terminate the server, the server would go into recovery and this particular hardware would recover 400 MB of redo log in less than 20 seconds. I had in fact at one time&nbsp;written a script that did restore a server from backup, start up recovery and replication, kill the server, and backup the server again, in a loop, for a week, in order to test and provoke a certain bug. The new DBA knew all I did knew, but from a book. He had not tested this personally the way I did. He knew the server was important, and to him kill -9'ing this server at 2pm in the afternoon was a high risk operation. So we agreed to reload the server the next morning at 6am. We met in a chat, and in a "screen -x" shared session. I typed the kill command, and in a second screen a "tail -F" on the error log of the server, then asked him to hit return. He could not. He physically was unable to hit the return key. He intellectally knew that it was safe and should recover in no time. He knew the operation should be safe. He could not bring himself to do this. So I did. Of course the server went through recovery, and came back in 12 seconds. We lost a minimal amount of business, far less then an orderly shutdown of the server would have cost. The admin saw, and learned. He knew before, but now he experienced personally that his knowledge is true, and trustworthy. He did not just know he was safe, he felt safe. In the following months he became an excellent and courageous DBA and did whatever was operationally necessary. The lesson here is that there is a huge difference between knowing things, _knowledge in the head_, and having experienced things personally, _knowledge&nbsp;in the heart_, and having done things so often that you do not even have to think about what goes which way when you act, _knowing things inutitively in the stomach_. These are knowledge, experience and intuition. Experience and Intuition cannot be taught in a book. They can only be gathered from practice, repetition and survived failure.</p>