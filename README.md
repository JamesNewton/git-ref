<HTML>
<HEAD>
  <!-- Created with AOLpress/2.0 -->
  <!-- AP: Created on: 10-Feb-2016 -->
  <!-- AP: Last modified: 13-Feb-2016 -->
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
and it's immidiate "parent"... the commit just before it.
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
Note that files in the folder are NOT automatically commited to the repo,
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
the command line, git will open an editor window with a default messge and
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
<B>Branches</B> allow you ot make completely seperate versions, as ooposed
to revisions, of your files which are tracked seperately over time and which
you can switch between. It is always good to keep a known working branch,
<B>Master is the default branch</B>, and then experiment with a named branch
off the Master "trunk". Branches can also be used to <B>allow mulitple people
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
<B>To merge </B>branches back together, differences must be resolved. That
can be difficult, but git can figure out most issues by itself by looking
through the prior versions on each branch to see what was added or removed.
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
To continue the merge, and work with git to resove the conflicts, don't abort
the merge, but instead edit the files git called out in the error message.
You will find that git has edited those files to include tags marking areas
of confilict:
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
<TT>git status</TT> to verify the new file shows "<TT>both modified</TT>"
(meaning it was changed in both branches) and then use <TT>git add
<I>filename</I></TT> to mark the new version to be committed. Finish by using
<TT>git commit</TT> to complete the merge. The message git autogenerates
will show what branches were merged and which files had conficts.
<P>
After a merge, all the commits in the merged branches will show in the log
in cronological order. As a result, the diff between commitID's may not show
only the changes made by the parent commit. Use:<BR>
<B><TT>git show <I>commitID</I> </TT></B><BR>
to display the changes from that ID's parent.
<P>
After a merge, if the branch name that was merged into the current branch
is not wanted, it can be deleted with :<BR>
<TT><B>git branch -d <I>branchName</I></B></TT>
<H2>
  WORKING WITH GITHUB / Remote Repository Servers
</H2>
<P>
<A HREF="https://github.com/">GitHub.com</A> is a web-based Git repository
hosting service. It offers all of the distributed revision control and source
code management (SCM) functionality of Git as well as adding its own features.
Unlike Git, which is strictly a command-line tool, GitHub provides a Web-based
graphical interface and desktop as well as mobile integration. It also provides
access control and several collaboration features such as bug tracking, feature
requests, task management, and wikis for every project
<P>
You can make a <B>local copy</B> of a <B>remote repository</B> (or
<I>repo</I>) on github with the command: <BR>
<B><TT>git clone
https://github.com/<I>ProfileName/repoName</I>.git</TT></B>
<P>
To make a <B>remote copy</B> of a <B>local repo, </B>
<UL>
  <LI>
    first create the repo at the remote system. For example, in github, click
    the "+" in the upper right corner (after logging in) and select New repo,
    enter a unique name (github will check) and decide what license you want
    and if you want to start with a README.md file. Once the repo is created,
    get the HTTPS link to it.
  <LI>
    then init or cd into a local repo, and add a link between the local and the
    remote repo with:<BR>
    <TT><B>git remote add <I>remoteName</I> <I>URL</I></B></TT><BR>
    where <I>remoteName </I>any name you would like to give this remote, and
    <I>URL </I>is the HTTPS URL. You can check the remotes that are associated
    with a local repo, including name and URL,&nbsp;with <BR>
    <TT><B>git remote -v</B></TT>
  <LI>
    load the data from the local repo to the remote by doing the first
    <I>push:</I><BR>
    <TT><B>git push <I>remoteName branchName</I></B></TT>
</UL>
</BODY></HTML>
