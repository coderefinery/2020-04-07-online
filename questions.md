

## Questions, answers, and feedback


### The essence of version control

https://coderefinery.github.io/git-intro/01-motivation/#the-essence-of-version-control

**Why can code become a disaster without version control?**

- Code got too complex and I changed and tested things. Lost overview. It got worse when another person joined me.
- You won't know what exact version was used in eg  a manuscript publication
- Sharing with collaborators and coauthors gets harder
- Incompatible libraries across the collaborator's computers, if you can see that in advance it keeps it from breaking
- No control over which author has made changes
- Minor changes and quick saves without proper update to version
- To sync code between platforms/ large data
- Hard to track versions when many people work on same project
- Reproducibility of research
- Possibility of recovering any version at any time
- Keeping track of what is happened in each version is much easier
- Had to rewrite (copy/paste) modules between versions

✍️ **What is your own motivation for learning Git with CodeRefinery?** (5mins)
- I do minor changes all the time in my code and we share a lot of snippets in our research group and by having a good version control set in action we will all be able to backtrack, especially since it counts as documents needed for archiving at the University it becomes even more important in academia. I also want to be more organised myself :)
- I have projects with just a few people, but am also a part of a large software development project, which has a complex structure. How to organize branches is one of the issues (personal branches vs. development, for example)
- I wrote quite a bit of code and I started git for version control, but also to keep track and a mainly as a backup. I write mostly alone. I did not do fancy git stuff.
- I would like to find better ways to keep my research projects organized and clean, keep important components of the projects available later when needed and not lose parts of the research. Learning how to publish it/make it open and usable to others is important, too. Thanks for hosting!
- I need to keep track of changes in my projects
- I get confused between versions. sometimes make mistakes and it is difficult to control the versions. Specially if I need to cherrypick.
- Organising my own scripts, which look like the example a bit; sharing with others; making a version for a manuscript
- Git & version control tools will help coordinate my research group for working on the same codes and share documents in a reproducible way. Also good to keep updated in Git.
- I am working on project with many collaborators
- At the start of my own project and looking for a good system to keep track of my work and ensure it will be reproducible
- Learn how to work in large collaborations with proper techniques for forking, making PRs and patches
- For the better documentation, saving the scripts of my projects.
- I would like to be able to share code with collegues
- To better organise the multiple scripts I am currently working on, and to share usable and clearly explained versions of them with my colleagues.
- I write code for fluid mechanics, typically ~10k lines. It's a miracle it has worked for this long without version control.
- I am already using Git for several years but collaboration with in less than five people and would like to advance in Git.


#### The Event Horizon Telescope imaging

https://coderefinery.github.io/git-intro/01-motivation/#a-real-life-example

- How to turn on annotation display? *from command line: `git blame $filename` or `git annotate $filename` (we will practice this on Wednesday), or "blame" button in file view on github. It's called "blame" for historical reasons, very unfortunate naming.
  - Thanks!
- What extenssion?
  - https://github.com/LuisReinoso/git-history-browser-extension


### Git basics

https://coderefinery.github.io/git-intro/02-basics/

- How can I avoid typing GitHub username and password every time I want to push/pull to/from GitHub?
    - We will discuss this tomorrow when we talk about sharing repositories but you can avoid typing credentials by using ssh keys: (https://help.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh)
- Would you mind please comment on commit messages, how to have multiline commit messages. What to write in a commit message? etc.
    - We will (hopefully) discuss this later but convention is one line which summarizes the commit and then one blank line, then more context. In the text we recommend to emphasize the "why" in the commit message. This is often more important than the "what" since I can see what changed from "git diff" or "git show".
- When to stage / add? Is there a recommendation?
    - Every time the change was improving things to "save" the change for an upcoming commit. One can stage many times before committing. But note that you cannot go back to previous stagings so when in doubt, rather commit often if you want to have the flexibility to go back.
    - I often like to make sure the code at least compiles before commiting. However, if the change is quite big, I sometimes I prefer to commit earlier to make sure I do not loose anything and I can come back if necessary.
    - I think commits should be "small" and group together changes that belong to the same "theme". For example, I would recommend committing some changes in codes separately to changes in documentation, rather than committing every change at once.
- I missed this important part. When is a file about to be tracked? When does this tracking start?
    - You have to `git add` at least once, then automatic.  From this moment on the file is part of the repository and if I delete the file, I can get it back from the repository.
- Configure git: I'm asked to configure username/etc now.
    - It prints out some instructions to follow.
    - https://coderefinery.github.io/installation/git/#configuring-git
    - git config --global user.name "Your Name"
    - git config --global user.email yourname@example.com

- I had to make some changes to instructions.txt. What do I do now?
    - Both `git add instructions.txt` , `git commit -m "Changes to instructions"`
- I am always confused if I have to do both to keep track of the change. Or would be `git add instructions.txt` again sufficient?
  - In our lesson, we always `git add` then `git commit`.
  - If you don't want to, a `git commit` will directly add+commit, but then no chance to review things first.
  - A commit is really a picture of the status of all your code, of all files. So before you take the picture you might want to choose what should be in. So, it is possible to commit only part of your new changes by only staging (adding) some of the files.  When you are doing too many things at once, this can be valuable.

- Would it make sense to do multiple `git add example.txt` before doing one `git commit example.txt` and what would this mean, please? What would it track? All changes?
  - It can make sense to avoid losing your intermediate work and we will discuss it later. But in the end, only the final version is saved permanently.
  - More in detail: you do one first time `git add example.txt`, so the status at that time is staged, then you modify again 'example.txt', and at this point you could either 1) commit, and this would only commit the staged changes (before your second modifications) or stage again before commiting (this would then put on stage also your second modifications)
  - If you `git commit $filename`, it will *add and* commit that filename.  So, to do (1) above, you have to do `git commit`, not `git commit example.txt`
  - Correct, this is exactly it. I have prepared this yesterday, may or may not be helpful: https://github.com/bast/git-staging-with-gophers


- I wanted to stop git from tracking changes to a folder. I thought the command was "git rm *" ; git commit. This ended up deleting all files. One way to get back the files is to git checout an older commit
    - The opposite of `git add <file>` is `git rm --cached <file>` (no longer track it) or `git reset <file>` (revert back to last change).
    - Is this the best way?
        - If it was actually committed before, to undo a previous commit (e.g. your `git rm *`, `git commit`), you can revert it with `git revert`.  This saves the history and we will go through it later.
- How does one stop git from tracking changes in a folder?
    - If they have never been tracked, add the paths to a file named `.gitignore` and Git will ignore them.
    - If they have been tracked, they stay tracked ever if they are in `.gitignore`, `git rm --cached <file>` will do what you want.  Removes file from staging area, leaves it in working directory.  Next commit removes it from tracking
    - All files should be either tracked or ignored. Make sure `git status` does not show any paths that are not either tracked or ignored - this will help your sanity and code quality long-term!


### Staging area

https://coderefinery.github.io/git-intro/

- Advantages/disadvantages of examples 1-5 in staging episode:
    - Example 1: difficult to distentagle the good from the possibly problematic in case you later decide to take some feature out again
    - Example 2: easier to undo something without touching other features.  This is our dream, but takes a lot of work.
    - Example 3: too big commit (and not sure what you commit apart from everything...)
    - Example 4: difficult to undo some feature
    - Example 5: difficult to find in `git log --oneline` what happened

- There was a question about what the difference was between reset and checkout
  - `git reset` can be used to unstage changes
  - `git checkout` will overwrite my working tree with either the staged version or the committed version (if there is no staged version). It can be used to get rid of unstaged changes


### Undoing

- what if one needs to work with a specific version which is not necessay the latest commit? I am asking about branching strategy. I usually face problems with cherry picking.
    - You can create a branch back in time, check out that branch, and do what you want.  We will discuss more tomorrow in the history inspection episode.
    - Make new branch from old hash `a123def`; `git checkout -b branchname a123def`. After you are done, you can go back to `master`.
    - One can also use `git checkout somehash` to switch to a version in the past but the disadvantage is that if you commit to the past branch, it gets lost.  (search "git detached HEAD" for more info.  But it's fine if you only want to have a look and not make any modifications
  - `git cherry-pick` can be useful to "merge" only one commit instead of all commits on the other branch.  But it doesn't take you back in time: it just re-applies a change somewhere else.  So, this probably doesn't do what you need here.

- How to undo only part of a commit
    - Simplest: undo that commit, and make it again. `git reset --mixed HEAD^` which will remove the most recent commit but keep the changes to files. After that you can go back to staging what you want to save.
    - if you prefer to keep the commit and undo part of it with a later commit, I would revert it (this will create a new commit), then `git reset --mixed` the new commit, then partially add/remove as above.


### Branching and merging

https://coderefinery.github.io/git-intro/06-branches/#exercise-branches

- With the `git graph` command you show, I get `git: 'graph' is not a command.` I found `git log --all --decorate --oneline --graph`, but this is a pretty lengthy command to remember/type.
    - We made our own alias for git graph: `git config --global alias.graph "log --all --graph --decorate --oneline"`
    - I wish git would include something this useful by default...
- If there was a change in "master" prior to branching "less-salt", would it show up in the graph between the two other branches?
    - Yes, It'll do roughly what you expect.  It makes the branch from the point you check out right before, including all that previous history.  `git graph` is your friend!
- When a repo is cloned from github: are the branches available only if checked out or are they available on the local repo by default?
    - When we clone we clone also all branches but they are tagged "remote" and can't be modified.  With the `git checkout` commands we have created local branches at the same points as the remote tracking branches. One thing that can be confusing is that both "remote" and "local" branches are on your computer after cloning.  `git branch -a` shows both local and remote, as does `git graph`.  When you push to a remote, it remembers what you pushed and updates the remote tracking branches.  Similar when you `git fetch`.
- Why is less-salt green in the graph after the merge with experiment?
    - This question referred to the vertical symbols connecting the asterisks in the graph.  The colors here have no meaning, they are colored just to help you tell them apart.
- One subtle but useful point: any normal git command will *only* modify the currently checked out branch.  So you merge *other* branch into *current* branch, and other branch is unchanged.
- What if you merged master into a feature branch (`git checkout feature`; `git merge master`)?
    - This is not necessarily a problem: graph gets a bit more confusing but you can figure it out go on. (unless you don't want those master commits in the feature branch)
    - Sometimes people would do this if your feature branch was old and needed an update from master (others might prefer `rebase` but that's beyond our scope now)
    - If you want to undo, the "rewind history" part under undoing from yesterday is how (`git reset --hard $commit_before_problem` but be careful you don't lose something!).
- If you then delete "master", is that a problem? Does Git need a "master" always?
    - The name "master" is just a name and default branch can be something else.  With no branches or no default branch, I guess weird stuff would happen but not a major issue.
- Can I merge a branch and continue working on it? And then merge the changes again and keep going...
    - Yes.  Keep an eye on `git graph` output to keep a grasp on the situation.  You might want to merge master into the branch, too, to keep the branch up to date.  (after you merge, if you checkout the feature branch and merge master, it should be a fast-forward to update the feature branch to current master)


### Sharing repositories online

https://coderefinery.github.io/git-intro/09-remotes/

- How can I push/pull to a branch other than master?
    - you can type `git push origin <branch-name>` or `git pull origin <branch-name>`
- How to set up ssh keys on GitHub?
  - https://help.github.com/en/github/authenticating-to-github/connecting-to-github-with-ssh
  - ssh keys will take a short time to understand the first time you do it, but will save you so much time in the long run.
- If you can have two origins, how do you keep both updated? How do they talk to each other?
    - A repository only talks to its links.  Your local copy could pull from one and push to another to keep them in sync.  `git pull origin` and `git push my_mirror`.  Figuring out the best process for you takes some thought though!  (there's also a `--mirror` option...)
- If I push to a public repository not owned by me, does the owner have to approve it before changes happen?
    - you can only push to repositories that you have write access to, i.e. your own repos, repos belonging to an organization that you belong to, or repos where the owner has explicitly added you.
    - For contributing to repos where you don't know the owner, you can instead make a "fork" (your own copy), push to that, and use a Pull Request to ask the owner to accept your change! This is covered in our [git-collaborative lesson](https://coderefinery.github.io/git-collaborative/), and is really the *git killer feature*.
- I often work on two computers (say, work and personal). What is the best way to keep them synced? Push everything to the repository and pull on the other computer?
    - If the computers can communicate with ssh, on each computer you could pull from the other one.  You could also have one central repo that both pull/push.  It's really up to you.  Central repo is probably simpler to set up, keep track of, and more reliable.
- Must there be only one origin per local git repository?
    - The name `origin` can only be used once, but it's just a name.  You can have multiple remotes that are equal.
- So, git push and pull are set on the origin remote by default, is that how these commands work?
    - Yes, default is origin so most of the time I don't think about it.
    - There are different options for "default remote" for branches, I think.  This isn't something I have investigated much, I'm sure stackoverflow has some thoughts! web search suggestion: "git default upstream".
- How do you remove a repository on Git?
    - For Github: Go to repository → Settings (repository settings, not user settings) → at bottom is a "Delete this repository" option.
    - To remove a remote link from your local repository: `git remote rm $name`
    - To remove a local repository, just remove it like a normal directory.


### History inspection

https://coderefinery.github.io/git-intro/10-archeology/

Group exercise: https://coderefinery.github.io/git-intro/10-archeology/#archaeology-exercise

- "reflog"
    - the git reflog lists *past* commands, all the hashes that have been visited, even if the commits have changed.  So, for example, if you rewrite history and lose something, you can get back to it.
    - side note: When we modify/squash/move commits, Git does not actually modify commits, they are immutable, Git always creates new commits which may displace the old commits. This means that you can recover from most commands (except `git checkout $file`) and always go back.
    - also note that "deleted" commits are not kept forever but may get "garbage collected" after a while (30 days?)

- Could we get the solution to the final question, please?
  - Solution to the "Archaeology exercise" (maybe a page will be created with it):
    2) `git grep -in 'No links matched that expression'`
    3) `git log -S 'No links matched that expression'`
    4) `git show 5bbeb7d`
    5) `git checkout -b inspect 5bbeb7d`
    6) There are various possibilities. In detached HEAD state, you can do `git checkout 5bbeb7d^`, where the `^` signals the previous commit to the reference (here `5bbeb7d`), but then you are no more in a specific branch. You could also proceed similarly to the previous point, with `git checkout -b inspect-previous 5bbeb7d^`, or you could finally decide that the master branch needs to point back to the commit `5bbeb7d^` with `git checkout master; git reset --hard 5bbeb7d^`, but then you will lose all the commits after `5bbeb7d^` unless you carefully settled another branch to point to your last commit (note however that these commits are most of the time not really lost, they will become 'orphan' commits not belonging to any branch, which can be browsed with `git reflog --all`, but then the situation will still be a bit chaotic, so better avoid ending up with orphan commits unless you really don't want them anymore).


### Feedback

#### Day 1

- when using Anaconda prompt `git log` gave no output for one participant, same as other git commands (e.g. diff, branch). tip: mention it in the section for the instalaltion of required software and encourage to use interface that behave more in a "Linux-like fashon", like MobaXterm
    - *Comments: Yes we should add some warnings in the setup and mention that it can happen (and I am not sure it is related to windows; probably more related to conda). My windows installation using conda works perfectly (git log, git diff, etc.) so it seems a bit unpredictible. MobaXterm and other similar alternatives for windows will be added too. (on my day to day work, I never use git bash but rather use MobaXterm).*
- interacting on HackMD was awesome!
- Nice intro to git, the pace was good I think
- Thank you for the lessons. I realise I am not so familiar with Git as others, maybe this is a problem. The speed was fast and with lots of open windows on my side it was a bit tricky to follow. I found the speed of the branching and merging session okay to follow with his type along session. The staging and undoing episode was a bit too fast :-)
- I liked the idea of breakout rooms and the helpers were super and patient. I wish there would be more time to discuss in the group.
- In the breakout rooms it would be good if one student could share his/her screen and the exercise can be done together.
  - Comment: In some rooms we did this. I liked this and the interaction brings questions up!
- Is it possible after the course to ask questions somehow? (answer: one option is to ask questions on coderefinery.zulipchat.com, questions always welcome)
- I will now go through the material again :-)
- it is very nice with the codealong-sessions, it has helped me a lot! also the breakout rooms helps and the make a student share their screen thing.
- it would be very nice if all the course links we are using (from the main website i guess) would be available when the course ends. I don't know if they close with the course but if they do maybe a  log in to the material would be an  opition? (answer: the lesson material will remain online but it will also evolve further, we are considering creating releases which remain frozen in time)
- Neat interface to try out Git and follow along. Thanks for setting this up and working through it. I didn't find the breakout rooms useful. For me, it was much nicer to stay in a single room and follow along (type along) as you went through exercises.
- Using 'git add -p' on git version 2.8 and ubuntu 18 throws error: fatal: git was built without support for git-add--interactive (NO_PERL=1). Any suggestions?  *how did you install git?*
  - On Ubuntu 18 (bionic), the latest version of git is 2.17.1. Can you try to update (https://packages.ubuntu.com/bionic/git)?
  - It's almost certainly not about the git version, but from where it was installed.  Anyway, installing from a different source could help.


#### Day 2

- It was much better than Day 1 since we are kinda leveled to working on more advanced works.
    - thanks!
- Agree with previous , the groups were put toghter in a good way today. All-in -all , nice course!!
    - thanks!  tell others about us, and remember to fill out the feedback in six months.
- The beginning yesterday was a bit slow, but that's really expected given it was the first time this workshop was done online and it's hard to get feedback from the students. Today it was much better. I also liked to have more time in the breakout groups. Much easier to interact and get questions answered. Thanks again!
    - thanks!
- Breakout sessions were helpful!
    - great, we will keep working on them!
- Is there a workshop planned for more advanced git?
  - We will definitely have one but not yet clear when. We are also working on a form where one can sign up to get notified about workshops on topics of their interest.
- My breakout sessions were more helpful today (interactive), but the type-along sessions in the main group were also good. It might be helpful if the breakout rooms are not force-closed, but a notice is sent to return to the main group instead. The questions and quick answers in both the HackMD and rooms were very useful, and Zoom interactions seemed to be pretty smooth.
    - great, thanks!
- Thanks a lot for the workshop! Kind and helpful instructors and excellent documentation!
    - thanks!  tell others about us, and remember to fill out the feedback in six months.
- Today the speed was better. I liked working together in my group sharing the screen, learning from others. Suggestion: Can you show the solution to the excercises on a different page? I would really like to know the solution for the last question of "Archaeology exercise", please. I was wondering what else is taught in the offline-course as it is 3 days long? Many thanks again.
    - Archaeology answer has been put above.
    - Answer about the 3 days course: typically we also talk about software licensing, collaborative git, reproducible research, automated testing, documentation, modular code development, jupyter (we are working on developing online versions of these; https://coderefinery.org/lessons/)
- I think the course was a great pace, it didn't need to be much more in-depth or complicated than it is, and it definitely was practical (the commands for git were taught in a very logical following, not chaotic or anything). I think it could have benefited a bit of how the online management and public sharing, but I understand this is a question for a longer course. In general the exercises were good, though I do not think they needed to be as long (time-wise) as they were.
    - thanks!
