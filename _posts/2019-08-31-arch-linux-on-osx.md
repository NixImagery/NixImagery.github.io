---
layout: post
title: Arch Linux on OSX
date: 2019-08-31 17:00
# description: 
img: archlinux-logo.png
# fig-caption: 
# fig-attrib: 
published: true
tags:
- OSX
- VM
- Linux
- Arch
# permalink:
---
I've wanted to take a look at Arch Linux for a while now, and when a student got me to connect her inherited Arch laptop to the University Wi-Fi network last week, I was reminded that this lightweight distribution is attractive to the increasingly paranoid control freak that I am becoming. Having toyed with the idea of spending money on an XPS or some other super-cool hacker machine, and having been defeated by prudence, here's how I got it running as a first-time-out instance on my University MacBook Air[^Mac].

## The Host
Like I said, I really can't justify a separate development machine, especially as I have use of a decent spec laptop. The [Arch download page](https://www.archlinux.org/download/) includes a number of different ways of acquiring the distro, including using [Vagrant](https://app.vagrantup.com/archlinux/boxes/archlinux) with VirtualBox, which I had intended to plug an Arch ISO disk into. 

## The Virtual Machine
I downloaded and installed [Vagrant](https://www.vagrantup.com/) and gave it a spin with the example Ubuntu 12.04 LTS. Installation, running and logging in to the instance takes three commands...

```bash
$ vagrant init hashicorp/precise64
$ vagrant up
$ vagrant ssh
```

## Arch
Firing up Arch itself could be done the same way, but the Vagrant site hints that once Vagrant is installed on your dev machine, all you need is a Vagrantfile with the right info in it. Here's the MWE[^MWE] I started with. It uses ruby syntax, and was simply a new directory containing a single file called ```Vagrantfile```:

```ruby
Vagrant.configure("2") do |config|
  config.vm.box = "archlinux/archlinux"
end
```

This is a super quick and easy way to get Arch up and running. Now, you just type the command:

```bash
$ vagrant up
```

This will download and install a fresh instance of Arch and fire it up, ready for you to ```ssh``` into.

[^Mac]: MacBook Air specs: 13-inch, Early 2015, 2.2 GHz Intel Core i7, 8GB DDR.
[^MWE]: Minimum working example.