<HTML>
<HEAD>
  <!-- Created with AOLpress/2.0 -->
  <!-- AP: Created on: 10-Feb-2016 -->
  <!-- AP: Last modified: 17-Feb-2016 -->
  <TITLE>GIT Version Control Software</TITLE>
  <LINK REL="home" HREF="http://www.ecomorder.com/techref/app">
</HEAD>
<BODY>
<H1>
  <A NAME="GIT" HREF="https://git-scm.com/">GIT^</A><A TITLE="JMN-EFP-786"
      NAME="42190.6908796296">
  </A><A HREF="http://techref.massmind.org/techref/method/versioncontrol.htm">Version
  Control</A> Software
</H1>
<P>
GIT is a free and open source distributed version control system designed
to handle everything from small to very large projects with speed and efficiency.
It is complex and somewhat picky about who it appears friendly to. For a
web interface, and shared hub see:<BR>
<A HREF="https://github.com">https://github.com</A>
<P>
<I>Note: the following was written with
<A HREF="https://git-for-windows.github.io/">msysgit</A> on Windows, but
it should apply to all versions and operating systems</I>.
<P>
With GIT, you can make a <B>local copy</B> of a <B>remote repository</B>
(or repo) with the command: <BR>
<B><TT>git clone <I>URL</I></TT> </B><BR>
This copies in ALL the changes to the files, not just the current version.
<P>
We can see a simple list of the <B>past changes</B> to a repo with the command:
<BR>
<B><TT>git log</TT> </B><BR>
issued inside the repositories main folder. The list includes unique <B>commit
ID's</B> along with the data, author and comment about each entry.
<!-- 42190.6908796296 EOR -->
<BLOCKQUOTE>
  Neat trick: Add this to .getconfig<BR>
  <TT>[alias]<BR>
  lg = log --graph --abbrev-commit --decorate --date=relative
  --format=format:'%C(bold cyan)%h%C(reset) - %C(bold green)(%ar)%C(reset)
  %C(white)%s%C(reset) %C(dim white)- %an%C(reset)%C(bold yellow)%d%C(reset)'
  --all</TT>
  <P>
  (the line starting lg= is a single line and should not be wrapped as it is
  shown here) <TT>git lg</TT> will produce a nice graph of git branches.
</BLOCKQUOTE>
<P>
To view the <B>differences</B> between two commit ID's use the command: <BR>
<B><TT>git diff <I>commitID</I> <I>commitID</I></TT> </B><BR>
This will list each file that has changed, and the differences between the
files in diff -c format. <BR>
<TT><B>git diff</B></TT> by itself shows the difference between the working
files and the staging area (files which have been added, but not yet
committed)<BR>
<TT><B>git diff --staged</B></TT> shows the difference between the staging
area and the head commit.<BR>
<B><TT>git show <I>commitID</I> </TT></B>shows the difference between a commitID
and it's immediate "parent"... the commit just before it.
<P>
To <B>go back</B> to a prior version or <B>branch</B>, use <BR>
<TT><B>git checkout <I>commitID</I></B></TT><BR>
commitID can be "master" to <B>return to the head</B>.
<P>
We can quickly see the <B>status</B> of the repo, including which files are
not committed, by running<BR>
<TT><B>git status</B></TT><BR>
This will list the current branch, the current commit, and which files are
not being tracked or have been changed.
<P>
To turn an <B>exiting folder</B> into a git repo:<BR>
<TT><B>git init</B></TT><BR>
git creates a hidden metadata folder to store information about the changes
made to a file. This must be separate from the file itself, since only the
currently checked out version of the file data will be in the file.
<P>
Note that files in the folder are NOT automatically committed to the repo,
nor will they be included in a commit. You have to <B>stage</B> files to
be<B> tracked</B>, and <I>then</I> <B>commit</B> them. Staged files are going
to be version tracked. Keeping them separate from other files provides a
way to focus tracking on only those files which need it.<BR>
<B>Add files</B> to the repo with <BR>
<B><TT>git add</TT> <I>filename</I></B><BR>
you can <B>remove files</B> from tracking with <BR>
<TT><B>git reset <I>filename</I></B></TT>
<P>
And then to commit those changes into the new repo (it doesn't automatically
do that when you init) with an optional message.<BR>
<B><TT>git commit</TT> <I>[</I> -m "<I>message</I>" <I>]</I></B><BR>
(by convention, the message should be a command. E.g. "Add stuff" instead
of "Added stuff" or "Adding stuff"). If you fail to include the message on
the command line, git will open an editor window with a default message and
expect you to edit that. By default, the editor used is vi. vi is not known
for making friends. Move cursor with arrows, press the i key to insert text,
press Esc to stop inserting. Type :wq to save and quit. If something goes
wrong, type :q to quite without saving. That is the : or colon key followed
by q.
<P>
Because it is important to ensure that <B>each individual commit is a logical
grouping of changes</B>, it is sometimes useful to remove one or more files
from tracking via the reset command before a commit, then re-add those files
and make a second commit.
<P>
<B>Branches</B> allow you to make completely separate versions, as opposed
to revisions, of your files which are tracked separately over time and which
you can switch between. It is always good to keep a known working branch,
<B>Master is the default branch</B>, and then experiment with a named branch
off the Master "trunk". Branches can also be used to <B>allow multiple people
to work at the same time</B> on the same code by creating a branch for each
person. Commits are only added to the branch you currently have checked out.
You can merge branches (usually back to the master) if the experiment works
out. <BR>
<TT><B>git branch</B></TT><BR>
lists the current branches with a star next to the currently checked out
branch.<BR>
<TT><B>git branch <I>branchName</I></B></TT><BR>
makes a new branch but does not check it out.<BR>
<TT><B>git checkout <I>branchName</I></B></TT><BR>
checks out a branch. New commits will be added to this branch.
<P>
Note that <B>git log shows commits along the branch that is currently checked
out</B>. So there may be other commitID's which are not listed if they are
on another branch. Having a diagram that shows all the branches would be
really nice...
<P>
Because branches are basically just names for commitID's, we can view the
<B>differences</B> between two branches with the command: <BR>
<B><TT>git diff <I>branchName branchName</I></TT></B>
<P>
If you check out a commitID which is not at the end, or HEAD, of a branch,
and then commit new changes from that revision, you will be in <B>"detached
HEAD"</B> state. You are following a new, unnamed, path which is sprouting
off from one of the named branches. The commits you make will not show up
in logs after checking out a branch head, and will not be merged back into
the Master if those branches are merged. To make this twig a new branch,
use:<BR>
<TT><B>git checkout -b <I>branchName</I></B></TT><BR>
which both makes a new branch and then checks it out.
<P>
<B>To <A NAME="merge">merge</A> </B>branches back together, differences must
be resolved. That can be difficult, but git can figure out most issues by
itself by looking through the prior versions on each branch to see what was
added or removed.
<P>
To start a merge, checkout the branch were you want to continue development
from in the future. Normally, this is the Master branch. Then issue the
command:<BR>
<TT><B>git merge <I>branchName [branchName ...]</I></B></TT><BR>
Note that you can specify as many other branches as you like, potentially
merging them all back into the current branch.
<P>
If there is a conflict which can not be resolved automatically, git will
report which files are in conflict and ask you to fix it. Note that the merge
operation has still been started. To abort the merge, use:<BR>
<TT><B>git merge --abort</B></TT><BR>
then you can use diff to view the files in conflict, resolve the conflict,
add and commit those new file versions and try the merge again. Once possible
source of conflict is line ending differences between operating systems.
See:
<A HREF="https://help.github.com/articles/dealing-with-line-endings/#platform-all">https://help.github.com/articles/dealing-with-line-endings/#platform-all</A>
<P>
To continue the merge, and work with git to resolve the conflicts, don't
abort the merge, but instead edit the files git called out in the error message.
You will find that git has edited those files to include tags marking areas
of conflict:
<UL>
  <LI>
    <TT>&lt;&lt;&lt;&lt;&lt;&lt;&lt; HEAD</TT> marks the start of a conflict.
    The code after this mark is your current code
  <LI>
    <TT>||||||| merged common ancestor.</TT> Starts the code which was in the
    prior versions of the file, before anyone changed anything.
  <LI>
    <TT>&gt;&gt;&gt;&gt;&gt;&gt;&gt; <I>branchID</I></TT> marks the code in that
    branch
</UL>
<P>
Edit the file to combine the code, retaining all the features you want. Work
with others if you aren't sure what their changes accomplish. Be sure to
remove the lines git added to mark the conflict. When you are finished, use
<TT><BR>
git status</TT> <BR>
to verify the new file shows "<TT>both modified</TT>" (meaning it was changed
in both branches) and then use <TT><BR>
git add <I>filename</I></TT> <BR>
to mark the new version to be committed. Finish by using <TT><BR>
git commit</TT> <BR>
to complete the merge. The message git auto-generates will show what branches
were merged and which files had conflicts.
<P>
After a merge, all the commits in the merged branches will show in the log
in chronological order. As a result, the diff between commitID's may not
show only the changes made by the parent commit. Use:<BR>
<B><TT>git show <I>commitID</I> </TT></B><BR>
to display the changes from that ID's parent.
<P>
After a merge, if the branch name that was merged into the current branch
is not wanted, it can be deleted with :<BR>
<TT><B>git branch -d <I>branchName</I></B></TT>
<H2>
  Working With Remote Repository Servers, e.g.
  <A HREF="../method/github.htm">GitHub</A>
</H2>
<P>
<A HREF="https://github.com/">GitHub.com</A> is a web-based Git repository
hosting service. It offers all of the distributed revision control and source
code management (SCM) functionality of a standard remote Git repo server
allowing multiple users to collaborate on a project through local Git repos.
It provides access control and several collaboration features such as bug
tracking, feature requests, task management, and wikis for every project.
<P>
You can make a <B>local copy</B> of a <B>remote repository</B> (or
<I>repo</I>) on github with the command: <BR>
<B><TT>git clone
https://github.com/<I>ProfileName/repoName</I>.git</TT></B>
<P>
To update the local from the remote, use:<BR>
<TT><B>git pull origin master </B></TT><BR>
assuming the name of the remote is origin (which it is by default) and the
name of the local branch is master (which it is by default). See below for
more.
<P>
To make a <B>remote copy</B> of a <B>local repo, </B>
<UL>
  <LI>
    first create the repo at the remote system. For example, in
    <A HREF="../method/github.htm">GitHub</A>, click the "+" in the upper right
    corner (after logging in) and select New repo, enter a unique name (github
    will check) and decide what license you want and if you want to start with
    a README.md file. Once the repo is created, get the HTTPS link to it.
  <LI>
    then init or cd into a local repo, and add a link between the local and the
    remote repo with:<BR>
    <TT><B>git remote add <I>remoteName</I> <I>URL</I></B></TT><BR>
    where <I>remoteName </I>is any name you would like to give this remote but
    by convention is most often <TT>origin</TT>, and <I>URL </I>is the HTTPS
    URL. Each remote is given a name so that you can have several. You can check
    the remotes that are associated with a local repo, including name and
    URL,&nbsp;with the verbose version of get remote:<BR>
    <TT><B>git remote -v</B></TT>
  <LI>
    load the data from the local repo to the remote by doing the first
    <I>push:</I><BR>
    <TT><B>git push <I>remoteName branchName</I></B></TT><BR>
    you should be asked for your username and password. To avoid entering your
    username each time, you can add a section to the config file:<BR>
    <TT>[credential "https://example.com"]<BR>
    &nbsp;username = <I>username</I></TT><BR>
    To avoid entering both username and password, you can setup credentials.
    For more
    see:&nbsp;<A HREF="http://stackoverflow.com/questions/5343068/is-there-a-way-to-skip-password-typing-when-using-https-github">General</A>,
    <A HREF="https://stackoverflow.com/questions/11693074/git-credential-cache-is-not-a-git-command">msysgit
    windows</A>,
    <A HREF="https://discussions.udacity.com/t/github-authentication-error/152121">troubleshooting
    msysgit windows</A>
</UL>
<H3>
  Collaboration
</H3>
<P>
<B>Conflicts must be resolved manually</B>: There is no system for automatically
sycronizing repos because too many conflicts require human review to resolve.
Googles collaborative documents avoid this problem (for the most part) by
re-syncronizing so quickly and constantly that conflicts don't have a chance
to develop... but that causes conflicts between programmers making incompatible
changes in the code all at the same time, and it moves a lot of data around,
increasing overhead.
<P>
<B>Fork at the Remote Repo:</B> Even if you are going to clone a remote repo
to work on it locally, when you are collaborating or want to extend or change
code written by someone else, it's best to "Fork" that code on the remote
so that there is a record of the source, and the possibility for the original
author to pull your changes back into the main project. See:
<A HREF="../method/github.htm#Fork">GitHub:Fork</A> for detailed instructions.
<P>
<B>Locals may be out of sync with Remotes.</B> If changes are made by you
in the local repo, and different, but non-conflicting&nbsp;changes are made
by someone else to the remote repo, then there is no problem, just use the
pull command to merge them back into your local repo:<BR>
<TT><B>git pull <I>remoteName branchName</I></B></TT>
<P>
<B>Resolve Conflicts</B>: If there is a conflict, you will have to resolve
it in several steps.
<OL>
  <LI>
    It's always safe to "fetch" the remote repo by it's remote name (usually
    origin), which will updated a local branch called
    <I>remoteName/branchName</I>, or most often origin/master. <BR>
    <TT><B>git fetch <I>remoteName </I></B></TT><BR>
    This remote branch still different, and in conflict, with your local master
    branch. And any repo with a remote has this seperate branch but it's normally
    hidden. You can see it with <TT><BR>
    <B>git branch -a</B></TT><BR>
    It turns out that a <TT>git fetch</TT> is exactly what a <TT>git pull</TT>
    does, but then it automatically starts a merge. And, in fact, we could just
    use <TT>git pull origin master</TT> instead of <TT>git fetch</TT>, but then
    we would be forced into a merge. It's nice to know what's going on before
    we have to resolve it. Also, doing a fetch is a nice way to check if other
    developers have pushed changes.
  <LI>
    Next, you need to use the same <A HREF="#merge">conflict resolution steps
    listed above to merge </A>the remote branch with your local branch. We can
    check<TT><BR>
    <B>git status</B></TT><BR>
    to see where we are, and we can use
  <LI>
    <TT><B>git diff master origin/master</B></TT><BR>
    to see the differences in the conflicting files. Once we feel confident that
    we can resolve the conflicts, we can use
  <LI>
    <TT><B>git checkout master</B></TT><BR>
    to make sure we are on the master branch, then
  <LI>
    <TT><B>git merge master origin/master</B></TT><BR>
    which will edit the conflicting files to show the issues, and list them.
    After we edit the file to consolidate the changes and remove the
    &lt;&lt;&lt; === &gt;&gt;&gt; tags we can use <TT></TT>
  <LI>
    <TT><B>git status</B></TT><BR>
    to verify the new files show "<TT>both modified</TT>" then
  <LI>
    <TT><B>git add <I>filename</I></B></TT> <BR>
    to mark the new version to be committed. Finish by using <TT></TT>
  <LI>
    <TT><B>git commit</B></TT> <BR>
    to complete the merge.
</OL>
</BODY></HTML>
