---
layout: post
title: Global Search for Moodle on Centos
date: 2017-09-06 15:54:42.000000000 +01:00
# description: 
img: Screen-Shot-2017-09-06-at-16.11.59.png
# fig-caption: 
# fig-attrib: 
published: true
tags:
- CentOS
- Solr
- Moodle
- PHP
# permalink: "/blog/2017/09/06/global-search-for-moodle-on-centos/"
---
My students are using a Moodle VLE to access resources and teaching materials and it became evident that some kind of global search function would help them find things quickly, especially later in the programme when they come to write their assignments.

I'm running Moodle on a CentOS 7.3 virtual private server with Plesk Onyx. The server hosts several other sites running WordPress, bespoke PHP and some other bits and pieces including the usual mail services. Some of the containers require the OS-standard PHP5.4 but a recent upgrade to Moodle 3.3 required me to switch the container to PHP 7.0.

Installing Global Search was a little tricky because of the multiple PHP versions running on the server, but I eventually figured it out to these key steps:

## Install the Solr Server
```sh
$ cd /opt
$ wget http://apache.mirrors.nublue.co.uk/lucene/solr/6.6.0/solr-6.6.0.tgz
$ tar zxvf solr-6.6.0.tgz
$ cp solr-6.6.0/bin/install_solr_service.sh .
$ rm -rf solr-6.6.0
$ ./install_solr_service.sh solr-6.6.0.tgz
$ chkconfig solr on
$ su - solr -c "/opt/solr/bin/solr create_core -c moodle"
```
You should be able to visit `http://your-domain.tld:8983` to verify the Solr server is running OK.

## Secure the Solr Server
By default, Solr is open to the world. You might want to secure it by adding this at the end of `/opt/solr/server/etc/webdefault.xml`

<pre class="p1"><span class="s1"><span class="Apple-converted-space">  </span>&lt;security-constraint&gt;</span>
<span class="s1"><span class="Apple-converted-space">   </span>&lt;web-resource-collection&gt;</span>
<span class="s1"><span class="Apple-converted-space">       </span>&lt;web-resource-name&gt;Solr Administration&lt;/web-resource-name&gt;</span>
<span class="s1"><span class="Apple-converted-space">       </span>&lt;url-pattern&gt;/*&lt;/url-pattern&gt;</span>
<span class="s1"><span class="Apple-converted-space">   </span>&lt;/web-resource-collection&gt;</span>
<span class="s1"><span class="Apple-converted-space">   </span>&lt;auth-constraint&gt;</span>
<span class="s1"><span class="Apple-converted-space">       </span>&lt;role-name&gt;solr-admin&lt;/role-name&gt;</span>
<span class="s1"><span class="Apple-converted-space">   </span>&lt;/auth-constraint&gt;</span>
<span class="s1"><span class="Apple-converted-space">  </span>&lt;/security-constraint&gt;</span>

<span class="s1"><span class="Apple-converted-space">  </span>&lt;login-config&gt;</span>
<span class="s1"><span class="Apple-converted-space">   </span>&lt;auth-method&gt;BASIC&lt;/auth-method&gt;</span>
<span class="s1"><span class="Apple-converted-space">   </span>&lt;realm-name&gt;Solr Administration&lt;/realm-name&gt;</span>
<span class="s1"><span class="Apple-converted-space">  </span>&lt;/login-config&gt;</span></pre>

Create a file in the same directory called realm.properties containing your chosen authentication details (matching the role above) in a single line:

`admin: password, solr-admin`

Finally, add this just before the last line in jetty.xml in the same directory:
```xml
<Call name="addBean">
 <Arg>
  <New class="org.eclipse.jetty.security.HashLoginService">
    <Set name="name">Solr Administration</Set>
    <Set name="config">
      <SystemProperty name="jetty.home" default="."/>/etc/realm.properties</Set>
    <Set name="refreshInterval"></Set>
  </New>
 </Arg>
</Call>
```

## Install the PHP Solr Extension
```sh
$ rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
$ rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
$ yum install libxml2-devel pcre-devel libcurl-devel php70w-devel php70w-pear
```

You'll need to build the extension using the right versions of phpize and php-config for your version of PHP, in my case, 7.0:

```sh
$ cd /opt
$ curl -O https://pecl.php.net/get/solr-2.4.0.tgz
$ tar zxvf solr-2.4.0.tgz
$ cd solr-2.4.0/
$ ../plesk/php/7.0/bin/phpize
$ ./configure --with-php-config=/opt/plesk/php/7.0/bin/php-config
$ make
$ make install
$ cp /opt/solr-2.4.0/modules/solr.so /opt/plesk/php/7.0/lib64/php/modules/
$ sudo service httpd restart
```

Visit the Site administration / ▶︎ Plugins / ▶︎ Search / ▶︎ Manage global search page in your Moodle installation to configure, index and enable the Solr Search Engine.

I am impressed with how quickly this has been used and appreciated by the students.
