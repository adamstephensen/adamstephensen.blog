# Adam's Blog

This project drives [my personal blog](https://adamstephensen.com) using the [Jekyll blog engine](https://jekyllrb.com/) with all the content hosted as markdown on [Github](https://github.com/adamstephensen/adamstephensen.blog).

I am happy for others to fork my master branch and use it to power their own blogs.
Disclaimer: for most people using a hosted solution that doesn't require management is preferrable as per [Troy Hunt's great post on the issue](https://www.troyhunt.com/its-a-new-blog/). I have previously run my blog on WordPress for years without any issue.

My reasons for this project are 
- I wanted to have my content as markdown in GitHub 
- I like having some 'real' projects to maintain
- I wanted to be able to easily edit content offline
- I wanted a project to use for Azure demos around topics like DevOps, containers and Azure FrontDoor

## Structure
There are two main branches to the project

- master: The core website that contains everything you need to run the blog is on the ```master``` branch.
- adamstephensen.com - All my content is in the ```adamstephensen.com``` branch.

You can also check out both websites

- [Core website](https://adamstephensen-blog-core.azurewebsites.net/)
- [Core website - staging](https://adamstephensen-blog-core-staging.azurewebsites.net/)
- [adamstephensen.com - staging](https://adamstephensen-blog-dev.azurewebsites.net/)
- [adamstephensen.com](https://adamstephensen.com)

## Resources
- I got the idea for this method from the [old version of the Azure Docs](https://github.com/Azure/azure.github.io) which used Jekyll. I created this project from scratch because the old docs used very outdated versions of dependencies like Jekyll and bootstrap but I have taken the page templates and a few scripts from this repo so big thanks to the team who put it together !!! 