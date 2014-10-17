---
layout: post
title: "How to deploy Octopress Blog"
date: 2014-10-17 10:03:30 +0800
comments: true
categories: 
---

Before You Begin
1.Install Git.
2.Install Ruby 1.9.3 or greater rbenv or RVM
If ruby --version doesn't say you're using Ruby at least 1.9.3, revisit your rbenv or RVM installation.

//Setup Octopress
git clone git://github.com/imathis/octopress.git octopress
cd octopress
//install dependencies
gem install bundler
rbenv rehash
bundle install
//Install the default Octopress theme
rake install

Create a new Github repository and name the repository with the format username.github.io, where username is your GitHub user name or organization name.

rake setup_github_pages
rake generate
rake deploy
git add .
git commit -m 'your message'
git push origin source

//Blog Posts
rake new_post["title"]
rake generate
rake deploy

(reke deploy 遇到的问题 如果你发觉老是失败 而且是提示pull 根据以下方法会成功)
Without deleting the repository

Please keep in mind this is not considered best practice, but it may work for you.

The solution is to force a push on the master branch.

Edit the Rakefile and look for this line:

system "git push origin #{deploy_branch}"
Alter the line by adding a plus (+) before the #{deploy_branch} tag:

system "git push origin +#{deploy_branch}"
Run the command

rake deploy
It should succeed.