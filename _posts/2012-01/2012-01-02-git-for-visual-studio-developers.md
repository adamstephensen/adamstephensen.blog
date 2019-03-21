---
title: Git - Essential Commands for Visual Studio Developers
permalink: /git-essentials/
layout: post
tags:
  - Git
  - Visual Studio
bigimg:
  - /assets/images/angular-superpower-photo-1.jpg
comments: true
---

# {{ page.title }}

Unfortunately, I see a lot of devs who would like to learn git, but get stuck trying to get to Git Level 1.

This post is the list of the essential commands that I believe you know to get started.

 
<h2>Getting Help</h2>
The git help is really good once you have an understanding of what's going on.
<pre>git help                 : return list of all the commands</pre>
<pre>git help <command name>  : to return the options for a specific command</pre>
<pre>git help add             : to display help specific for the add command</pre>
<h2>The Basics</h2>
Visual Studio  does a great job of the basics. All of the commands in this section are handled very nicely in the Visual Studio interface. But..... it will go wrong, and when it does you are going to need to go to the command line. I'd strongly suggest that you spend at least a week or two doing the basics on the command line, as it will help you with your understanding of git, so that when things to get more complicated, you can deal with them.
<h4>Create a new repository</h4>
<pre>git init</pre>
<h4>Add a file to the repository</h4>
Once you add a file to the folder, you need to tell git that you want git to track it.
<pre>git add <pathspec>          : Adds all the files in the specified path</pre>
<pre>git add *.cs                : To add all c# files</pre>
Tip: to add all files in the working tree that have been added or changed, but are not excluded by the .gitignore file.
<pre>git add .</pre>
Note: <pathspec> is used to indicate a file path. Wildcards can be used. e.g. *.cs and also leading directory names. e.g. content/*.jpg.
<h4>Status, Commit, Push, Pull</h4>
Just the basics will get you a long way here. Check the references below for great articles explaining in more details.
<pre style="padding-left:30px;">git status

git commit -m "Merged suo conflict from staging"   : Commit to the local repository 

git pull                       : Pull the pending commits from the server 
git pull origin staging        : Same as the above, but specifies the server and branch to pull from

git push                       : Push the current repository
git push origin staging        : Some devs like to specify the target repository as well. Here it is 'staging' on 'origin'
git config --global credential.helper cache   : Get git to remember your username and password
</pre>
<h4><strong>Merge from staging to master</strong></h4>
First you must be on the branch that you want to merge to git checkout master :The checkout command select the branch to work on Merge the staging branch into the master branch
<pre style="padding-left:30px;">git merge staging           :Specify the branch to pull the changes from</pre>
<h2>Commands You Wish Visual Studio Had</h2>
<h4>Discard your local changes. (Equivalent of Visual Studio, Source Control, Undo - but this one will always work*)</h4>
Are you in Visual Studio, trying to undo all your changes, but getting an error. This is the answer.

This command will

- point the current branch back to point HEAD (your last commit).

- update the files in the staging to match those from HEAD.
<pre style="padding-left:30px;">git reset --hard HEAD</pre>
 
<h4 id="Remove-files-from-your-repository">Remove files from your repository (so that they aren't tracked), but leave them in the working directory.</h4>
There are files in your solution that you don't want git to track.

To stop git from tracking these files you should

- tell git not to track them in the future by adding an exclusion in your .gitignore file TO

You dont' want to include your user settings files in your repository because it is individual to each user.

If someone has committed it to your repository, you want to remove it from the repository so that it is no longer tracked by git, but still leave the files in the working directory.
<pre style="padding-left:30px;">git rm *.suo --cache
</pre>
The same applies to your Azure publish profiles. Remove the azure publish setting files from the index, but leave them in the working folder
<pre style="padding-left:30px;"> git rm *.pubxml --cache

<a title="Update your .gitignore" href="http://adamstephensen.com/2014/05/13/update-your-gitignore/">Check out my post on updating your .gitignore file</a></pre>
<h2>More to come...</h2>
Keep checking back as I'll add more as they come up and I think they are helpful.

 
<h2><strong>Great References</strong></h2>
<a title="Learn Git In 15 Minutes" href="https://try.github.io/levels/1/challenges/1" target="_blank">Learn Git in 15 Minutes</a>

<a title="Try Git from CodeSchool" href="https://www.codeschool.com/courses/try-git" target="_blank">Try Git from CodeSchool</a>

<a title="Github for Beginners: Don't get scared, get started" href="http://readwrite.com/2013/09/30/understanding-github-a-journey-for-beginners-part-1" target="_blank">Github for Beginners: Don't get scared get started.</a>

<a title="Git Reference" href="http://gitref.org/" target="_blank">Git Reference</a>

<a href="https://www.kernel.org/pub/software/scm/git/docs/everyday.html" target="_blank">Everyday Git with 20 commands or so</a>

 
<h1></h1>