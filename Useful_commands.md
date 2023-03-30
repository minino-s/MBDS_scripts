Useful commands to create branches:

-   git branch \# List branches in repository
-   git branch &lt;branch name&gt; \# create a new branch
-   git checkout &lt;branch name&gt; \# Start working on the Branch
-   git log --all --decorate --oneline --graph \# Graphical scheme of
    branching tree

Useful commands to merge branches:

-   git diff &lt;target branch&gt;..
    \# show the changes that will be merged into the current branch
-   git merge &lt;source branch&gt; \# merge the current branch with the
    branch where the changes have been performed.
-   git merge --abort \# stop merging process and don't merge anything
-   git merge --no-ff &lt;source branch&gt; \# gives the opportunity of
    a commit message, even though a fast forward merge was done
-   git log --merge \# produces a list of commits that conflict with
    each other

Useful commands to rebase branches:

-   git rebase &lt;target branch&gt; \# rebases the current branch
    (source branch) to the tip of the target branch
-   git rebase -i &lt;target branch&gt; \# gives the opportunity to
    clean up commit history before rebasing
-   git push --force \# this will force git to push the altered main
    branch and overwrites the remote main branch

Workflow to combine merge and rebase command by generating a temporary
branch:

-   git checkout &lt;temporary branch&gt;
-   git checkout -b &lt;temporary branch&gt;
-   git rebase -i &lt;main&gt; \# Clean up the commit history in an
    interactive session
-   git checkout &lt;main&gt;
-   git merge &lt;temporary branch&gt;

Useful commands to delete branches:

-   git branch --merged \# show which branches are merged together
-   git branch -d &lt;branch name&gt; \# delete a branch, but only if it
    was merged to another branch already
-   git branch -D &lt;branch name&gt; \# deletes a branch, no matter if
    the work was merged already

Other useful commands:

-   git branch -m &lt;branch&gt; \# rename a branch
-   git branch -r \# list remote branches
-   git checkout -b &lt;existing branch&gt; \#will create and checkout a
    new branch from an existing branch
