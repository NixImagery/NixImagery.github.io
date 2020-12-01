---
layout: post
title: Github/Jekyll site update via Rake
# date: 2019-11-26 20:10
# description: 
img: Ilford-Delta-3200-20201127_20085880.jpg
fig-caption: Yester Castle
fig-attrib: Nick Hood
published: true
tags:
- Jekyll
- Git
- Rake
# permalink:
---
I wanted a quick way to provide useful comments on commits made in development of a Jekyll site which is deployed on GitHub. This method offers a couple of rake tasks to first quickly build the site locally, placing the output into the `docs` folder; then to commit and push the changes to GitHub once you're happy. All of this code goes in the `Rakefile`.

### Build

```ruby
require 'rubygems'
require 'rake'
require 'rdoc'
require 'date'
require 'yaml'
require 'tmpdir'
require 'jekyll'

desc "Generate blog files"
task :generate do
  Jekyll::Site.new(Jekyll.configuration({
    "source"      => ".",
    "destination" => "docs"
  })).process
end
```
You can build and test your site in your development machine (I'm using a Mac) using a python http server to render the static site thus:

```sh
$ rake generate
Configuration file: /your/path/to/GitHub/projectname/_config.yml
$ cd docs/
$ python3 -m http.server
```
### Deploy
You should place an empty `.nojekyll` file in the root of your project to tell GitHub not to bother rebuilding the site. You're just deploying static files to the `docs` folder. Once you're ready to deploy, you can publish via rake. The rest of the `Rakefile` looks like this:

```ruby
# Usage:
# $ rake
# $ rake generate
# $ rake publish
# $ rake publish["Your comment here"]

desc "Generate and publish blog to master/docs"
task :publish, [:var] => [:generate] do |task, args|
  args.with_defaults(var: 'Commit via Rake')
Dir.mktmpdir do |tmp|
    system "mv docs/* #{tmp}"
    system "git checkout -B master"
    system "rm -rf docs/*"
    system "mv #{tmp}/* docs"
    system "git add ."
    system "git commit -a -m #{args.var.inspect}"
    system "git push origin master --force"
    system "git checkout master"
    system "echo Finished."
  end
end

task :default => :publish
```
For example, you might publish using this command from the project folder:

```sh
$ rake publish["Example updates"]
(in /your/path/to/GitHub/projectname/)
Configuration file: /your/path/to/GitHub/projectname/_config.yml
D	docs/yyyy/mm/dd/some-files.html
....
Reset branch 'master'
Your branch is up to date with 'origin/master'.
[master abcdefg] Example updates
 n files changed, p insertions(+), q deletions(-)
Enumerating objects: r, done.
Counting objects: 100% (nn/nn), done.
Delta compression using up to x threads
Compressing objects: 100% (mm/mm), done.
Writing objects: 100% (mm/mm), 1234 bytes | 123.00 KiB/s, done.
Total mm (delta nn), reused 0 (delta 0)
remote: Resolving deltas: 100% (nn/nn), completed with nn local objects.
To https://github.com/YourGHName/projectname.git
   0aa7f2g..abcdefg  master -> master
Already on 'master'
Your branch is up to date with 'origin/master'.
Finished.
```
Notice a call to publish will also generate the site for you. If you're in a hurry, just issue `rake` to get the default *Commit via Rake* commit message.