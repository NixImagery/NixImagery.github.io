---
layout: post
title: Upgrading solr server from 6.6.0 to 7.3.1
date: 2018-06-13 17:36:30.000000000 +01:00
# description: 
published: true
img: heron.jpg
fig-caption: Heron
fig-attrib: by Nick
tags: [Solr, Moodle]
permalink: "/blog/2018/06/13/upgrading-solr-server-from-6-6-0-to-7-3-1/"
---
I use Apache's [Solr](http://lucene.apache.org/solr/) to provide a global search facility on Moodle. Now that my courses have ended for the summer, it's time to bite the bullet and upgrade the Solr server software from version 6.6.0 which I installed last year, to the current 7.3.1. This turned out to be more straightforward than I feared, and did not require me to touch the PHP solr module that I had to compile from source when I installed it the first time. Here are the steps:

```bash
$ cd /opt
$ wget http://apache.mirrors.nublue.co.uk/lucene/solr/7.3.1/solr-7.3.1.tgz
$ tar zxvf solr-7.3.1.tgz
$ cp solr-7.3.1/bin/install_solr_service.sh .
$ rm -rf solr-7.3.1
$ ./install_solr_service.sh solr-7.3.1.tgz -f
```

Notice the -f flag which tells the script to upgrade an existing installation. The script stops the currently running instance, extracts the new code and starts the instance. A quick check of the admin interface on port 8983 shows the new code running OK, the cores intact, and the client service on Moodle nominal.

**EDIT:** At present (June 2018) [Solr 7 is not supported on Moodle 35](https://docs.moodle.org/35/en/Global_search#The_Solr_server). The latest version of the Solr server that works with Moodle 35 is 6.6.4: the instructions above will install Solr 7.

If you want global search to work with Moodle 35, replace "7.3.1" with "6.6.4" and fetch the code using wget from the Apache archive at <http://archive.apache.org/dist/lucene/solr/6.6.4/solr-6.6.4.tgz>.
