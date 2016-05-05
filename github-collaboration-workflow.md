# <img src="https://cloud.githubusercontent.com/assets/7833470/10899314/63829980-8188-11e5-8cdd-4ded5bcb6e36.png" height="60"> GitHub Collaboration Workflow

GitHub is a powerful tool for version control and collaborating on code. There are two main scenarios for collaborating on coding projects:

1. You **fork** another developer's project and make pull requests from *your remote fork* to the *project's remote*.
2. Another developer makes you a **collaborator** on a project they own, giving you the ability to clone the project and make pull requests directly from the project's *remote branches* to the project's *remote master*. (Note that as a collaborator on a project, you also have the ability to push directly to the master branch, which you should NEVER do.

![github-collab-diagram](https://cloud.githubusercontent.com/assets/7833470/12072895/69abd404-b0b1-11e5-8d8c-4ff54c13b0a0.png)

## Collaborator Scenario

Imagine you, Jessica, and Sam want to build an app together. Jessica bootstraps a Rails project, pushes it to GitHub, and adds the other two group members as <a href="https://help.github.com/articles/adding-collaborators-to-a-personal-repository" target="_blank">collaborators</a>. The group delegates tasks and sets to work.

Your first task is to add user authentication. At the same time, Jessica is doing API integration and Sam is writing tests.

1. You clone the project Jessica pushed up to GitHub after she makes you a collaborator. This creates a local repository with a `remote` called `origin`, which is the original repo Jessica created and technically belongs to Jessica. From within your local repository, you can check the URLs of all remote repos it's connected to.

  ```zsh
  ➜  git remote -v
  ```

2. Before you start implementing user authentication, make a new branch called `auth`. Feature branches help organize work on a project and ensure that only production-ready code lives on the `master` branch.

  ```zsh
  ➜  git checkout -b auth
  ```

  *Now you build the entire auth feature with sign up, log in, log out, etc. The following steps outline how to get your new code up to the main group project.*

3. Make sure to commit all your changes on your `auth` branch. Switch back to your local `master` branch, then pull from `origin/master` to bring your local `master` branch up to date.

  ```zsh
  ➜  git checkout master
  ➜  git pull origin master
  ```

4. Now switch back to your local `auth` branch and merge your local `master` branch into it. This will give you a chance to resolve all conflicts with the most up-to-date master version before making a pull request. Watch git's output in the Terminal to see if any files have merge conflicts.

  ```zsh
  ➜  git checkout auth
  ➜  git merge master
  ```

  **VERY IMPORTANT:** IF you have a merge conflict, you should grab one of your team members to help determine how to safely merge the code, then follow the instructions for [resolving merge conflicts locally](#resolving-merge-conflicts-locally).

5. Once you've resolved any conflicts, add and commit your changes locally, and push your feature branch to the remote repo.

  ```
  ➜  git add .
  ➜  git commit -m "fix conflicts; merged with master"
  ➜  git push origin auth
  ```

6. In your browser, head to the original remote repo's GitHub page. GitHub will detect that you just pushed a new branch and give you a prompt to make a pull request for that branch. Go for it!

  ![pull-request](https://cloud.githubusercontent.com/assets/7833470/12072813/76841710-b0aa-11e5-9644-4f840081c986.png)

  This will notify all the collaborators that you just made a pull request, and it's waiting to be merged. The next step is for someone else on the team to review your code and suggest any changes needed before merging it in. Your team will agree on the workflow for this as part of the planning process.

7. If there are no other pull requests in the queue, one of your team members can merge your pull request cleanly with the most up-to-date `master`. But if your team merges other pull requests before yours, those pull requests might create merge conflicts with yours.

  In that case, GitHub will show that merge conflicts exist and must be resolved locally. You'll want to repeat steps 3-5 to resolve the conflicts locally. Remember it's not up to the project "owner" to fix all the merge conflicts. (How could they do that? They didn't write your code!) Each branch owner is responsible to get a clean pull request queued up. 
  
8. Once the feature branch has been moved into the `master` branch, you can delete the feature branch on GitHub. If you really need to, you can restore the deleted branch. It's up to the team member to delete the branch locally if desired.   

## Resolving Merge Conflicts Locally
1. First, and most importantly: Don't panic! Communication between team members will help you avoid them, but merge conflicts will inevitably happen. They're not the end of the world! Follow the rest of these steps to resolve conflicts. 

1. When merging your local `master` branch into a local feature branch, the Terminal will let you know if there are conflicts, and if so, which files have conflicts.

  ![conflict-terminal](https://cloud.githubusercontent.com/assets/7833470/12072814/7a636df4-b0aa-11e5-98b0-0e31b37dc41d.png)

2. Open your project in your text editor, and open the file(s) with conflicts. You can see the conflict here on lines 27-33:

  ![conflict-sublime](https://cloud.githubusercontent.com/assets/7833470/12072816/813bd576-b0aa-11e5-9b22-b6b41302f9fa.png)

3. You AND one of your group members should decide together which version of the code to keep and which to delete. Remember to always delete the "merge junk" (`<<<<<<< HEAD`, `=======`, and `>>>>>>> master` lines) to prevent syntax errors.

  ![delete-code](https://cloud.githubusercontent.com/assets/7833470/12072817/842c5cce-b0aa-11e5-9c9a-9eecb678a7ad.png)

4. After deleting the decided-upon code and the merge junk, your file should now have the clean version of the code, ready to be checked into git.

  ![final-code](https://cloud.githubusercontent.com/assets/7833470/12072818/8760301e-b0aa-11e5-8248-9201c1d70153.png)

5. Add and commit your changes that resolved the conflict(s):

  ![resolve-conflict](https://cloud.githubusercontent.com/assets/7833470/12072819/898221a4-b0aa-11e5-84ec-f6a1bedaa6de.png)

  Your feature branch is now ready to be pushed up to GitHub, without conflicts!
  
## Tips for Working in Teams
1. Communicate,communicate, communicate! Before you start coding, it's important for your team to discuss roles, expectations, and timetables. Don't assume that everyone is on the same page or that problems will magically resolve themselves - take the time to plan first, and you'll be glad you did later.

2. As part of your planning process, select a GitHub master. This person will be the owner of the GitHub repository, and will add everyone else in the team as collaborators. 

3. Set guidelines for merging pull requests. How many people should review the pull requests before they're merged? Who will be in charge of merging pull requests? What branch should they be merged into? 

4. Consider making a "develop" or "staging" branch to merge into instead of merging into the master branch. Once your app is complete, then you can merge your development branch into the master branch. 

5. Make very descriptive commit messages! The team members who are reading them should be able to tell at a glance what you were working on.

6. Clearly delineate who's working on what. Things will go much more smoothly if team members work on features that don't overlap. This is especially important if you're not all working in the same spot. It's easy to check in on one another when you're in the same room, but once people spread out it's not uncommon for wires to get crossed! 

7. Don't have multiple team members working on the same feature branch at one time. If you're pair programming with someone, only use one computer to avoid having differing code on the same branch. 

8. When merge conflicts arise, it's not up to the GitHub master to resolve them. It's up to the individual contributor! Follow the steps for [resolving merge conflicts locally](#resolving-merge-conflicts-locally), make sure to delete any merge junk from your code, and then push your cleaned-up branch to GitHub.  
  

## Resources

* <a href="https://help.github.com/articles/adding-collaborators-to-a-personal-repository" target="_blank">Adding collaborators to a personal repository</a>
* <a href="http://nvie.com/posts/a-successful-git-branching-model" target="_blank">A successful Git branching model</a>
* <a href="https://help.github.com/articles/using-pull-requests" target="_blank">Using pull requests</a>

## Git Tutorials

* <a href="https://www.codeschool.com/courses/try-git" target="_blank">Try Git - Code School</a>
* <a href="https://github.com/Gazler/githug" target="_blank">githug</a>
