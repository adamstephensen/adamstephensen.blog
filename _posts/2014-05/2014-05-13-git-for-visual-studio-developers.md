---
title: Git for Visual Studio Developers–Get your .gitignore right and save yourself needless merges
permalink: 2014/05/13/update-your-gitignore/
layout: post
tags:
  - .NET
comments: true
---

<p>One of the most common issues I am finding with teams moving from Team Foundation Version Control to TFS-Git is that they are including files in their repositories that they shouldn’t. The most common offenders are .suo user settings files, Nuget packages and Azure publish settings.   Luckily, the solution is straightforward.   </p> <p>1. Ensure you have no pending changes. </p> <p>2. Close the solution </p> <p>3. Go into Team Explorer and click Settings <a href="./images/image6.png"><img title="image" style="background-image:none;padding-top:0;padding-left:0;display:inline;padding-right:0;border-width:0;" border="0" alt="image" src="./images/image6.png" width="452" height="279"></a>   </p> <p> </p> <p>4. In the Settings tab select Git Settings <a href="./images/image7.png"><img title="image" style="background-image:none;padding-top:0;padding-left:0;display:inline;padding-right:0;border-width:0;" border="0" alt="image" src="./images/image7.png" width="458" height="392"></a>   </p> <p> </p> <p>5. Open the .gitignore file from GitHub that is specific to Visual Studio projects and copy the contents to the clip board. <a title="https://raw.githubusercontent.com/github/gitignore/master/VisualStudio.gitignore" href="https://raw.githubusercontent.com/github/gitignore/master/VisualStudio.gitignore">https://raw.githubusercontent.com/github/gitignore/master/VisualStudio.gitignore</a> <a href="./images/image12.png"><img title="image" style="background-image:none;padding-top:0;padding-left:0;display:inline;padding-right:0;border-width:0;" border="0" alt="image" src="./images/image12.png" width="462" height="262"></a> <br>Figure: the .gitignore includes a list of all of the files that you want to avoid committing to your repository  </p> <p> </p> <p> 4. In Settings | Repository Settings, click the Edit link next to ‘/,gitIgnore’ <a href="./images/image8.png"><img title="image" style="background-image:none;padding-top:0;padding-left:0;display:inline;padding-right:0;border-width:0;" border="0" alt="image" src="./images/image8.png" width="461" height="398"></a>   </p> <p> </p> <p> </p> <p>6. Paste the contents of the .gitIngore from GitHub into the .gitignore file and Save it. <a href="./images/image15.png"><img title="image" style="background-image:none;padding-top:0;padding-left:0;display:inline;padding-right:0;border-width:0;" border="0" alt="image" src="./images/image15.png" width="462" height="315"></a>   </p> <p> </p> <p>7, In Team Explorer, navigate to the Changes window. Enter a comment and click Commit. <a href="./images/image9.png"><img title="image" style="background-image:none;padding-top:0;padding-left:0;display:inline;padding-right:0;border-width:0;" border="0" alt="image" src="./images/image9.png" width="473" height="413"></a>   </p> <p> </p> <p>8. Click the Sync link to take you to Unsynched Commits <a href="./images/image10.png"><img title="image" style="background-image:none;padding-top:0;padding-left:0;display:inline;padding-right:0;border-width:0;" border="0" alt="image" src="./images/image10.png" width="473" height="415"></a>   </p> <p> </p> <p>9. Click the Sync button to push your updated .gitIgnore <a href="./images/image11.png"><img title="image" style="background-image:none;padding-top:0;padding-left:0;display:inline;padding-right:0;border-width:0;" border="0" alt="image" src="./images/image11.png" width="480" height="290"></a>   </p> <p> </p> <p>10. If you have included files in your repository that you wish to exclude from the repository but not delete from your local working directory refer to </p> <p><a href="http://adamstephensen.com/git-essentials#Remove-files-from-your-repository" target="_blank">Remove files from your repository (so that they aren't tracked), but leave them in the working directory</a> </p> <p>on my page for </p> <p><a href="http://adamstephensen.com/git-essentials/" target="_blank">Git: Essential Commands for Visual Studio Developers</a></p>
