# Git Maintenance

## Course Goals

* List the items that should be included in a README
* Identify what makes a good commit message
* Explain when to merge vs rebase
* Perform an interactive rebase to clean up your git history
* List three things you can accomplish with git commit --amend
* Describe the process of creating and submitting a pull request

## Summary

Git is a tool that new developers tend to overlook. Being able to show off good git practices can signal to future employers that you are organized and pay attention to details. Git maintenance is one of many soft skills that a good developer should possess.

## README

A README is typically the first place that software seekers will look when deciding which open source tools to use in their projects. New developers on a project will look to the README as the first piece of documentation to find all of the information that they need to get started working on the codebase. It is a window into the application. Therefore, understanding how to effectively write a README is important knowledge that every developer should have.

The main components of a README include:

* The name of the application
* Description of what the application does
* Requirements needed to run the application
* How to install and use/run the application
* How to run the tests (if it is developer facing)

Additionally, these options should be considered where appropriate:

* License information
* Images of the user interfaces if appropriate
* A CI badge indicating the build status (will show green if the tests pass)
* Author attributions
* Ways that one can contribute to the project
* Future planned work

### README Examples

#### [HTTPie](https://github.com/httpie/httpie#readme)
![HTTPie README]('./assets/httpie_readme.png')
#### [Release It!](https://github.com/release-it/release-it#readme)
![Release It! README]('./assets/release_it_readme.png')
#### [Sinatra](https://github.com/sinatra/sinatra)
![Sinatra README]('./assets/sinatra_readme.png')
#### [Sourcerer](https://github.com/sourcerer-io/sourcerer-app#readme)
![Sourcerer README]('./assets/sourcerer_readme.png')


## Commit Messages

Your commit messages should be meaningful and focused. It should be obvious for a person reading your commit history what was changed and when. Here are some guidelines:

### Be concise

If you fixed a typo, you don’t need to say what specifically was fixed; if anyone wants that level of detail, they will look at the code from the commit.

Stick to character limits (50 characters for the body, 72 for the description if you must include one).

### Use conventional mood

Note what the commit accomplished in present tense imperative mood:

  *This fixes a typo…* 🚫

  *Fixes a typo…* 🚫

  *Fixing a typo…* 🚫

  *Fixed a typo…* 🚫

  *Fix a typo* ✅


### Follow style conventions

Capitalize the commit, don’t include abbreviations unless they are obvious, don’t include a period at the end

### Tag the commit

If you are working with user stories that are sequenced, prepend your commit with that sequence number.

*Note: WIP commits are completely fine if that is part of your workflow. We will talk about how to edit your commit history to only include meaningful commit messages through interactive rebasing in the next section.*

## Git History

An organized git history with expressive commit messages serve as another method of documentation for the codebase.

### Git Rebase

Whether you are working with a group or working independently, rebase is a great tool to help you keep your commit history clean and orderly.

### Rebase vs merge

When you are working with multiple branches, whether multiple branches of your own, or you are working in a group, you have two options for incorporating code into your working branch.

**Merge** takes all of the changes from the other branch and merges them into your working branch. A merge commit is added as the most recent commit in your git history. Any commits you have made on your working branch will be woven into your working branch’s commit history based on their timestamp.

![Git Merge](https://wac-cdn.atlassian.com/dam/jcr:c6db91c1-1343-4d45-8c93-bdba910b9506/02%20Branch-1%20kopiera.png?cdnVersion=960)

**Rebase** takes all of the changes from the other branch and adds them at the bottom of your working branch, so all of your commits from your current branch are shown at the top of your git history. Rebasing essentially creates a new starting point for your branch.

![Git Rebase](https://wac-cdn.atlassian.com/dam/jcr:4e576671-1b7f-43db-afb5-cf8db8df8e4a/01%20What%20is%20git%20rebase.svg?cdnVersion=960)

Behind the scenes, all of your commits on your current working branch are actually recommitted, which is what makes them appear in the order they do in the commit history, despite the timestamps

### When to merge vs rebase:

* **Merge** when you are merging changes from a feature branch into your main branch after a PR review

* **Merge** when you pull down code from a branch on Github that has changed into your same branch locally that has not changed (this is done behind the scenes when you perform a git pull)

* **Rebase** when you are on a working branch and want to incorporate the most recent changes from main into your working branch

* **Rebase** when your team all knows how to properly rebase and everyone on the team is using rebase as their merging strategy

### Rebasing Changes From Main Into Your Feature Branch

Working in a team setting and pulling new changes from main into your working feature branch is one of the most common use cases for rebasing. Here are the steps we would use to accomplish this:

```bash
// from your feature branch, you are ready to submit a PR
git add .
git commit -m "A good commit message"
git push origin some-feature-branch // just to be safe, push to your fork on GH
git checkout main

// on main branch
git pull upstream main
git checkout some-feature-branch

// back on feature branch
git rebase develop // at this point, your feature and local main should both have
                   // the latest changes in main
git push origin some-feature-branch

// Open a PR in Github
// PR is merged
```

### Interactive Rebase

An interactive rebase is a way to edit your commit history on a working branch. You would want to use this if you have many low-quality commit messages and you want to clean up the git history.

Interactive rebasing provides several options, but we will be focusing on squash and fixup. These two options are similar, except squash allows you to amend the commit messages.

Let’s say you have the following commits on your working branch:

```bash
$ git log
commit a3b1297d89d04473f8ee226b3e56c78027de3783 (HEAD -> abc-2576-inforce-reissue-face-term-update)
Author: Nicole Jones <nicole@example.com>
Date:   Thu Dec 15 17:05:00 2022 +0000

    ABC-2576 Save face/term increase for later

commit f6afd15274db32426f2bf94e845f3ad8f3a9c2af
Author: Nicole Jones <nicole@8thlight.com>
Date:   Thu Dec 15 14:43:41 2022 +0000

    fix a linter error

commit 2131f0c31cb6585ae5e22307ddd3722b5b68243c
Author: Nicole Jones <nicole@example.com>
Date:   Tue Nov 8 21:05:34 2022 +0000

    ABC-2576 Create API endpoint for inforce_face_term_update

commit bbdd28571bb9f3625eeaf4a5560fc553ce8cee02 (upstream/develop, develop)
Merge: 1cd41cca 31d84378
Author: Patrick Smith <patrick@example.com>
Date:   Fri Dec 9 16:20:40 2022 -0600

    Merge branch 'retry-add-cash-to-rt' into 'develop'

    ABC-2541 Fix problem saving SOAP fault messages in acord_103_response

    See merge request vericity-platform/nbx!1693
```

You can include the four commits in your rebase using either of these commands:

`git rebase -i HEAD~4 (select the last 4 commits)`


`git rebase -i bbdd28571bb9f3625eeaf4a5560fc553ce8cee02 (select commits beginning from this SHA)`

The above command will open up the interactive rebase menu:

```bash
pick 31d84378 ABC-2541 Fix problem saving SOAP fault messages in acord_103_response
pick 2131f0c3 ABC-2576 Create API endpoint for inforce_face_term_update
pick f6afd152 fix a linter error
pick a3b1297d ABC-2576 Save face/term increase for later

# Rebase 1cd41cca..a3b1297d onto 1cd41cca (4 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup [-C | -c] <commit> = like "squash" but keep only the previous
#                    commit's log message, unless -C is used, in which case
#                    keep only this commit's message; -c is same as -C but
#                    opens the editor
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <label> = label current HEAD with a name
# t, reset <label> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
# .       create a merge commit using the original merge commit's
# .       message (or the oneline, if no original merge commit was
# .       specified); use -c <commit> to reword the commit message
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
```

All of the commits are set to **pick**, meaning if you exited at this point, nothing would happen.

By changing the “picks”, you can perform an action on a commit. Let’s say we want to combine this commit into the one above (note that the order is opposite of how it was displayed with git log).

```bash
pick 2131f0c3 fix a linter error
```

We don’t want to keep this commit in the middle of other meaningful commit messages, so we can either change “pick” to “squash” or “fixup” to merge it into the commit that is shown above it. You would then save the edit (:wq if you are using vim). If you check your git history, that commit would be gone, but the changes would be part of the commit that you squashed it into.

The difference between squash and fixup is that with squash, you can keep both commit messages (they are combined into one), or you can edit the messages. Fixup just deleted the message for the commit you are getting rid of.

## Amending a commit

One last commonly used tool is the amending your last commit. If you want to change your last commit message and you don’t have any changes staged, you can use this command:

```bash
git commit -amend
```

If you do have changes staged, that command would allow you to edit the commit message while also including the changes in that commit.

Finally, if you have staged changes you want to add to the previous commit and you do not want to edit the commit message, you can use this command:

```bash
git commit -amend --no-edit
```

## Pull Requests

A pull request is your opportunity to solicit feedback on the code you have written. Generally when you are working on a dev team, other members of your team will be reviewing your code, but that is not always the case. Even if your code is being reviewed by other members of your team, it is still prudent to include as much context as possible in your pull requests so that the reviewer(s) can more easily assess the code.

The pull request feedback cycle for first timers is usually longer than developers anticipate, because first pull requests almost always require a lot of feedback. There are some measures that you can take to reduce this feedback cycle.

### Length

Pull requests should be small. Small PRs mean faster turnaround time, less chance of a merge conflict, and less back and forth between the reviewer and submitter. When you are working on a project that involves production code, having smaller merge requests means that more code gets promoted to a production environment, more quickly.

### Title

PR titles should include the relevant ticket number and title, ie: *TODO-001 Display a list of tasks*. If tickets are small, or if the tickets tasks are effectively broken down, then the PRs should reflect that structure.

### Branch name

The branch name should model the ticket name ie: *todo-001-display-a-list-of-tasks*.

### PR description

The description should include (where appropriate) the acceptance criteria for the ticket that it is addressing. If there is a UI change, screen shots should also be included.

### Commits

* Should be prepended by the ticket number ie: *TODO-001 Display a single task*, *TODO-001 Display multiple tasks*
* Should be in the imperative mood (**Fix a typo**, and not *Fixes a typo*, *Fixing a typo*, *Fixed a typo*)
* Should be concise
* Should follow convention
  * First word should be capitalized
  * Use plain English–don’t include uncommon abbreviations
  * Don’t add a period at the end
  * Squash unnecessary commits

### Test coverage

All pull requests should include tests for the features that were added. All tests must be passing. You **never** should commit and push up broken code for a PR, because if it gets merged, that broken code will infect the main branch of your repository.

## Exercises

* Practice rebasing to update git commit history
* Practice rebasing changes from your main branch into a feature branch

## Resources

* [Make a Readme (template)](https://www.makeareadme.com/)
* [Pro Git](https://git-scm.com/book/en/v2)
* [Version Control (video/article)](https://missing.csail.mit.edu/2020/version-control/)
* [How to Write a Git Commit Message](https://cbea.ms/git-commit/#seven-rules)
* [Git Maintenance](https://git-scm.com/docs/git-maintenance)
* [Squashing Commit Messages](https://www.internalpointers.com/post/squash-commits-into-one-git)
* [Merging vs. Rebasing](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)
* [Git Interactive Rebase, Squash, Amend and Other Ways of Rewriting History](https://thoughtbot.com/blog/git-interactive-rebase-squash-amend-rewriting-history)
