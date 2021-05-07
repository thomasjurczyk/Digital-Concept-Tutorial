# A practical guide to Git: what you'll probably actually use at work and nothing more
Thomas Jurczyk

This tutorial aims to teach the basics of git in a real-world, working context. I will aim to leave out the features nobody cares about or uses and keep the tutorial to only the practial parts of git.

This tutorial would ideally be aimed at those with a basic understanding of programing who want to learn more about git.

### Branches/Branching
Branching may not seem important now, but when you start working in the corporate world you'll most likely be maintaining large apps instead of building new ones from scratch. This makes it essential that you create a new branch for every change you make, even if it seems fairly minor.

* First, you need to pull in the git project that you want to work with. This is fairly simple, since once you have your computer properly credentialed to connect to your organization's remote git server, pulling in the code should be as simple as following the instructions provided with their repositories.

* It is important to note that, when creating a new branch the easy way that I describe, the branch will be created based on the branch you currently have checked out. This is why you must start by checking out your base branch (usually master or release.) Do this by running the command `git checkout master`. To ensure you have the most up-to-date version of the branch, run `git pull` to pull in all the latest changes.

* It is important that your branches have a universal naming structure. I've found that something like `sprint-title/story-or-ticket-number/breif-issue-description` works well. To checkout a sample branch in a sprint named Arches with story code FT-1684 which asks you to update some API endpoints, your new branch name would be something like `Arches/FT-1684/update-API-endpoints`

* To automatically create a new branch and check it out at the same time, run the command `git checkout -b Arches/FT-1684/update-API-endpoints`

* At this point you're all ready to write your code. Once you are done making your code changes, run this handy command: `git status`. This command will show you all the files you've changed and whether they are being tracked by git. When you create new files they are not tracked by git by default. If you run `git status` and all the files that are not added to git need to be added to the project, you can move on to the next step. If, however, you unintentionally changed some already tracked files or added files you don't want git to track, use the `git checkout -- file-you-didn't-mean-to-change` command to undo changes to tracked files, and preferably delete any untracked files you don't want to commit.

* Now you're ready to commit your changes. To do this, run `git commit -a -m "short message describing the commit`. This adds all untracked files you want to git tracking, and updates the files you wanted to update in your local git repository. To push these changes to your remote git server, run the `git push` command.

### Merging

In a perfect world, merging the branch you checked out to develop a new feature would work flawlessly every time. In the real world however, you often run into merge conflicts, in other words areas in the code where git can't tell whether your changes or the original code should be kept.

* In most remote git programs, there is an option to attempt to automatically merge your branch into master/release when you create a pull request (basically a request to merge your code into master/release that other developers on your team can review.) This option is the simplest way to merge in your branch, and you really hope ti works. If it does, you're done, and the rest of this section is unnecessary.

* If, however, that automatic process fails due to a merge conflict, you will need to manually resolve the conflict yourself. To do this, type the command `git merge master`. Your local git will then attempt to merge the branches and find the same conflicts that prevented automatic merging. In your console window, git will give you a list of files where merge conflicts are located. To resolve these conflicts, you must open each file and find the line or lines that begin with `<<<<<<< HEAD`. The structure is something like:
```
<<<<<<< HEAD
(code from the branch you're trying to merge in to)
=======
(code you wrote that conflicts with the above code)
>>>>>>> branch-youre-working-on-now
```
* To resolve these, select either the code from the branch you're merging into or the code you wrote as correct, and delete the other code along with the lines beginning with <, =, and >.

* Once you've done this for all files where git found conflicts, commit your changes, push your code to the remote server, and try merging your pull request again. This time, it should work.

### Conclusion

I know that some people and some workplaces use some more git features than this, but in my experience these are the real essentials.
