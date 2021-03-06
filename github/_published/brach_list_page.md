<!-- -*-Markdown-*- -->

# Branch Lists

Git's branching model is one of it's best features.  Branches are cheap, fast and extremely flexible.  They're great for developing features, maintaining old releases, or just plain experimentation.

If you spend a lot of time with git, you'll also find that there's a lot of really useful information to be discovered in the way git can compare various branches.  We're using some of this information to generate our new [branch list](http://github.com/merbjedi/mongomapper/branches/master) page (you can get to this page from the 'Branch List' subnav item under Source).

### Check in on your topic branches in one glance

Not only do these new branch list pages show you which branches exist on your remote, but you can see at a glance how they compare to any branch.

[![Example Branch List Page](http://share.kyleneath.com/captures/All_Branches_for_merbjedi_s_mongomapper_-_GitHub-20100226-182612.jpg)](http://github.com/merbjedi/mongomapper/branches/master)

Each branch has what we call a divergence graph. On the left side of the black bar we show how many commits that branch is behind (commits in master not found in the branch).  On the right side, we show how many commits that branch is ahead (commits found in the branch, but not in master).  The colors of the bars indicate how recent the last commit was.

In that one graphic, you get an idea of when the last time each branch was updated with master, how far along that branch is, and if people have been working on it recently.

These graphs also have some implicit rules that can help when merging:

* **No left side bar** - This branch is safe to merge with your base branch and there will not be any conflicts.
* **No right side bar** - This branch has already been merged into your base branch, so it's probably ready to be deleted.
* **Large left and right side bars** - This branch is probably going to be difficult to merge. There's a lot of unique commits in the branch and in your base branch so the likelihood of merge conflicts is much higher.

### Having fun with Rails releases

This view can also be fun to glean some information out of Rails releases.  Rails keeps a branch for each point release.  If we take a look at the branches with 2.2 as the base, we [get a pretty interesting page](http://github.com/rails/rails/branches/2-2-stable)

[![Rails Releases](http://share.kyleneath.com/captures/All_Branches_for_rails_s_rails_-_GitHub-20100226-184625.jpg)](http://github.com/rails/rails/branches/2-2-stable)

Using the divergence graphs, we can see how each of the point releases of Rails compare to the 2.2 release. You can also see that there was almost as many commits from 1.2->2.2 as there has been from 2.2->master (Rails 3 beta).

### Compare View

The last piece of the branch lists page is the compare button on each branch.  This is an *awesome* feature--but I think I'll leave it to Ryan to explain in more detail.