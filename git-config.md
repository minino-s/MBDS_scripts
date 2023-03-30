# Using git config to determine non-default behavior 

Git uses the tool **git config** to determine and change non-default behaviour.
**git config** sets configuration variables control all aspects of how Git looks and operates.
Three configuration files in different places store configuration variables on different levels.
Git checks these files one after the other to find these variables.

- The first file git checks: `/etc/gitconfig`\
This contains settings that are applied to every user on the system + all their repositories\
**system-wide**  
    
 - next file Git checks: `~/.gitconfig` or `~/.config/git/config`\
     is specific to each user\
     affects all repositories the user works with on the system\
     **global**
- last file git checks: configuration file in the Git directory of currently used repo: `.git/config`\
    values are specific to that single repository\
    This is default if not specified by user\
    **local** 


- **Each level** (system, global, local) **overwrites** values of previous level
- The user can pass options to git config (--system, --global, --local), so git reads and writes to each file specifically.
- In general it makes sense to pass most variables globally, and use local level for project-specific options.


## What to set up with git config

* As first step, set user name and email.\
     `git config --global user.name "John Doe"`\
     `git config --global user.email johndoe@example.com`
* Specify default **editor of choice** (e.g. for commit messages) with `core.editor`\
    By default, Git uses the editor set by shell environment variables. 
* Create your own **template** for commit-messages using `commit.template`
* Specify the tool to **output pages** given with commands as log and diff, using `core.pager`\
     `less` by default
* Save your **signing key** for annotated tags using `user.signingkey`
* Change the default branch name to e.g. main with `init.defaultBranch main`
* For Git to not only point out but also **correct a typo**, use `help.autocorrect`

* `color.ui` lets the user choose whether they want **colored output** or not\
     set this either to false or true (default)
    
* custom **merge resolution** and **diff tools**\
     `merge.tool` to tell Git what strategy to use, \
     `mergetool.<tool>.cmd` to specify how to run the command, \
     `mergetool.<tool>.trustExitCode` to tell Git if the exit code of that program indicates a successful merge resolution or not, and \
    `diff.external` to tell Git what command to run for diffs.\
    These four commmands can be skipped by adding a few lines to to `~/.gitconfig`
* **Formatting and whitespaces** are often an isue when sharing code, especially with different operating systems\
     Git has configuration options to help with this.
    
## Inspect configuration settings

* check all current settings
* Pass `--list` and `--show-origin` to git config to **find all settings** and **their origins**
    
## Server Configuration 


* There are less configuration options available for the server side than user side.

    ### Application examples

* Making sure that every object received during a push still **matches its SHA-1 checksum** and points to valid objects is not done by default\
    Set `receive.fsckObjects true` to force Git to check this\
    Is computationally expensive though!

* **force git to refuse force pushes**:\
The user can force push with a -f flag if git denies their push\
Set `receive.denyNonFastForwards true` to prevent this\
Can also be done via server-side receive hooks

* Possible workaround the denyNonFastForwards policy:\
deleting the branch and pushing with a new reference\
To prevent users from doing this, set `receive.denyDeletes true` to avoid this\
**Deletion of branches or Tags is then denied for every user**

## Git ignore: Not every file needs to be version-controlled
    
* It makes sense to **omit version control for non-essential files**:\
     maybe they can be produced from other files (intermediate and result files) that are being version controlled.\
 Some editors produce duplicates of files, which do not make sense to commit.
    
* With the git config commmand `core.excludesfile` **patterns to be ignored** can be specified\
 Files matching patterns will not be shown as untracked or suggested for staging

* Usage:\
 create a .gitignore_global file, which can be filled with patterns to ignore or\
set up .gitignore_global to ignore all files, and include only particular file types\
pass `core.excludesfiles /path/to/file/.gitignore_global` to git config --global


## Git Alias 
    
* Aliases in Git are **custom shortcuts** that define commands that expand to longer or combined commands
* Git provides its own alias system through the use of the git config command and the Git configuration files
* Git aliases are **stored in Git configuration files** in \[alias\] sections
* use the git config command to configure aliases
* Reasons for using Aliases in Git:
    * Aliases enable more **efficient workflows**
    * practical for frequently used commands


### Aliases in practice
* Creating the aliases will not modify the source commands
* There is no direct git alias command
* Creation of Git Aliases
    * direct editing of Git config files or usage of git config tool
* possible popular aliases:
    * `alias.co checkout` 
    * `alias.br branch` 
    * `alias.ci commit` 
    * `alias.st status`
    * reference other aliases within alias
        * `alias.amend ci --amend`
    * common Git pattern is to remove recently added files from the staging area
        * `alias.unstage 'reset HEAD --'`
 
# Sources
https://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration

https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup

https://www.atlassian.com/git/tutorials/setting-up-a-repository/git-config

https://www.atlassian.com/git/tutorials/git-alias

https://gist.github.com/tdd/470582