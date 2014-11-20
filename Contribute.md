This document explains how to contribute changes to RE2. It assumes you have installed RE2 using the [installation instructions](wiki/Install).

## Discuss your design
RE2 welcomes submissions but please let everyone know what you're working on if you want it to become part of the main repository.

Before undertaking to write something new for RE2, send mail to the [mailing list](http://groups.google.com/group/re2-dev) to discuss what you plan to do. This gives everyone a chance to validate the design, helps prevent duplication of effort, and ensures that the idea fits inside the goals for the language and tools. It also guarantees that the design is sound before code is written; the code review tool is not the place for high-level discussions.

In short, send mail before you code.  And don't start the discussion by mailing a change list!

## Testing
Before sending code out for review, run all the tests for the whole tree to make sure the changes don't break other packages or programs:

<pre>
$ cd your_re2_root<br>
$ make test<br>
</pre>

The test output should end with the line ` ALL TESTS PASSED. `
(Make may print an ` rm ` command after that.)

You should also add tests covering the code you are adding.  If this is a bug fix, add a test that checks the bug is really fixed.

## Code review

NOTE: THIS IS ALL OUT OF DATE AND NEEDS TO BE UPDATED. DO NOT DO THIS ANYMORE.

Changes to RE2 must be reviewed before they are submitted, no matter who makes the change. (In exceptional cases, such as fixing a build, the review can follow shortly after submitting.) A Mercurial extension helps manage the code review process. The extension is included in the RE2 source tree but needs to be added to your Mercurial configuration.

### Caveat for Mercurial aficionados
Using Mercurial with the code review extension is not the same as using standard Mercurial.

The RE2 repository is maintained as a single line of reviewed changes; we prefer to avoid the complexity of Mercurial's arbitrary change graph. The code review extension helps here: its ` hg submit ` command automatically checks for and warns about the local repository being out of date compared to the remote one. The ` hg submit ` command also verifies other properties about the RE2 repository. For example, it checks that the author of the code is properly recorded for copyright purposes.

To help ensure changes are only created by ` hg submit `, the code review extension disables the standard ` hg commit ` command.

Mercurial power users: To allow RE2 contributors to take advantage of Mercurial's functionality for local revision control, it might be interesting to explore how the code review extension can be made to work alongside the Mercurial Queues extension.

### Configure the extension

Edit ` your_re2_root/.hg/hgrc ` to add:

<pre>
[extensions]<br>
codereview = /your_re2_root/lib/codereview/codereview.py<br>
[ui]<br>
username = Your Name <you@server.dom><br>
</pre>
Replace ` /your_re2_root ` with the fully rooted path to your re2 checkout's root (where the LICENSE file is).  The Mercurial configuration file format does not allow environment variable substitution. The username information will not be used unless you are a committer (see below), but Mercurial complains if it is missing.

### Log in to the code review site

The code review server uses a Google Account to authenticate. (If you can use the account to sign in at google.com, you can use it to sign in to the code review server. The email address you use on the Code Review site will be recorded in the Mercurial change log and in the CONTRIBUTORS file. You can create a Google Account associated with any address where you receive email.

<pre>
$ cd your_re2_root<br>
$ hg code-login<br>
Email (login for uploading to codereview.appspot.com): rsc@swtch.com<br>
Password for rsc@swtch.com<br>
Saving authentication cookies ...<br>
$<br>
</pre>

If you use two-factor authentication with your Google Account, the password here should be an Application-Specific Password, not your real password.  See https://accounts.google.com/IssuedAuthSubTokens for details.

### Configure your account settings

Edit your code review settings. Grab a nickname. Many people prefer to set the Context option to “Whole file” to see more context when reviewing changes.

Once you have chosen a nickname in the settings page, others can use that nickname as a shorthand for naming reviewers and the CC list. For example, rsc is an alias for ` rsc@golang.org `.

### Make a change
The entire checked-out tree is writable. If you need to edit files, just edit them: Mercurial will figure out which ones changed. You do need to inform Mercurial of added, removed, copied, or renamed files, by running hg add, hg rm, hg cp, or hg mv.

When you are ready to send a change out for review, run

<pre>
$ hg change<br>
</pre>
from any directory in your RE2 repository. Mercurial will open a change description file in your editor. (It uses the editor named by the $EDITOR environment variable, vi by default.) The file will look like:

<pre>
# Change list.<br>
# Lines beginning with # are ignored.<br>
# Multi-line values should be indented.<br>
<br>
Reviewer:<br>
CC:<br>
<br>
Description:<br>
<enter description here><br>
<br>
Files:<br>
re2/simplify.cc<br>
re2/testing/simplify_test.cc<br>
re2/testing/random_test.cc<br>
</pre>
The Reviewer line lists the reviewers assigned to this change, and the CC line lists people to notify about the change. These can be code review nicknames or arbitrary email addresses. Reviewer should typically be ` rsc `.

Replace “` <enter description here> `” with a description of your change. The first line of the change description is conventionally a one-line summary of the change and is used as the subject for code review mail; the rest of the description elaborates.

The Files section lists all the modified files in your client. It is best to keep unrelated changes in different change lists. In this example, we can include just the changes to the simplifier by deleting the line mentioning ` random_test.cc `.

After editing, the template might now read:

<pre>
# Change list.<br>
# Lines beginning with # are ignored.<br>
# Multi-line values should be indented.<br>
<br>
Reviewer: rsc<br>
CC:<br>
<br>
Description:<br>
fix bug in simplifier<br>
<br>
See Bimmler and Shaney, ``Extreme automata,'' J. Applied Math 3(14).<br>
Fixes issue 159.<br>
<br>
Files:<br>
re2/simplify.cc<br>
re2/simplify_test.cc<br>
</pre>
The special sentence “` Fixes #159. `” associates the change with issue 159 in the RE2 issue tracker. When this change is eventually submitted, the issue tracker will automatically mark the issue as fixed.

Save the file and exit the editor.

The code review server assigns your change an issue number and URL, which hg change will print, something like:

<pre>
CL created: http://codereview.appspot.com/99999<br>
</pre>
If you need to re-edit the change description, run hg change 99999.

You can see a list of your pending changes by running ` hg pending ` (` hg p ` for short).

### Synchronize your client
While you were working, others might have submitted changes to the repository. To update your client, run

<pre>
$ hg sync<br>
</pre>
(For Mercurial fans, hg sync runs ` hg pull -u ` but then also synchronizes the local change list state against the new data.)

If files you were editing have changed, Mercurial does its best to merge the remote changes into your local changes. It may leave some files to merge by hand.


### Mail the change for review
To send out a change for review, run ` hg mail ` using the change list number assigned during hg change:

<pre>
$ hg mail 99999<br>
</pre>
You can add to the Reviewer: and CC: lines using the -r or --cc options. In the above example, we could have left the Reviewer and CC lines blank and then run:

<pre>
$ hg mail -r rsc--cc math-nuts@swtch.com 99999<br>
</pre>
to achieve the same effect.

Note that ` -r ` and ` --cc ` cannot be spelled ` --r ` or ` -cc `.

### Reviewing code
Running ` hg mail ` will send an email to you and the reviewers asking them to visit the issue's URL and make coments on the change. When done, the reviewer clicks “Publish and Mail comments” to send comments back.

### Revise and upload
You will probably revise your code in response to the reviewer comments. When you have revised the code and are ready for another round of review, run

<pre>
$ hg mail 99999<br>
</pre>
again to upload the latest copy and send mail asking the reviewers to please take another look (PTAL). You might also visit the code review web page and reply to the comments, letting the reviewer know that you've addressed them or explain why you haven't. When you're done replying, click “Publish and Mail comments” to send the line-by-line replies and any other comments.

The reviewer can comment on the new copy, and the process repeats. The reviewer approves the change by replying with a mail that says LGTM: looks good to me.

Submit the change after the review
After the code has been LGTM'ed, it is time to submit it to the Mercurial repository. If you are a committer, you can run:

<pre>
$ hg submit 99999<br>
</pre>
This checks the change into the repository. The change description will include a link to the code review, and the code review will be updated with a link to the change in the repository.

If your local copy of the repository is out of date, ` hg submit ` will refuse the change:

<pre>
$ hg submit 99999<br>
local repository out of date; must sync before submit<br>
</pre>
If you are not a committer, you cannot submit the change directly. Instead, a committer, usually the reviewer who said LGTM, will run:

<pre>
$ hg clpatch 99999<br>
$ hg submit 99999<br>
</pre>
The clpatch command imports your change 99999 into the committer's local Mercurial client, at which point the committer can check or test the code more. (Anyone can run clpatch to try a change that has been uploaded to the code review server.) The submit command submits the code. You will be listed as the author, but the change message will also indicate who the committer was. Your local client will notice that the change has been submitted when you next run hg sync.

## Copyright

Files in the RE2 repository don't list author names, both to avoid clutter and to avoid having to keep the lists up to date. Instead, your name will appear in the [Mercurial change log](http://code.google.com/p/re2/source/list) and in the [CONTRIBUTORS](http://code.google.com/p/re2/source/browse/CONTRIBUTORS) file and perhaps the [AUTHORS](http://code.google.com/p/re2/source/browse/AUTHORS) file.

The [CONTRIBUTORS](http://code.google.com/p/re2/source/browse/CONTRIBUTORS) file defines who the RE2 contributors—the people—are; the [AUTHORS](http://code.google.com/p/re2/source/browse/AUTHORS) file, which defines who “The RE2 Authors”—the copyright holders—are. The RE2 developers at Google will update these files when submitting your first change. In order for them to do that, you need to have completed one of the contributor license agreements:

  * If you are the copyright holder, you will need to agree to the [individual contributor license agreement](http://code.google.com/legal/individual-cla-v1.0.html), which can be completed online.

  * If your organization is the copyright holder, the organization will need to agree to the [corporate contributor license agreement](http://code.google.com/legal/corporate-cla-v1.0.html).  (If the copyright holder for your code has already completed the agreement in connection with another Google open source project, it does not need to be completed again.)

This rigmarole needs to be done only for your first submission.

Code that you contribute should use the standard copyright header:

<pre>
// Copyright 2010 The RE2 Authors. All rights reserved.<br>
// Use of this source code is governed by a BSD-style<br>
// license that can be found in the LICENSE file.<br>
</pre>