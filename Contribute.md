# Black Lives Matter. [Support the Equal Justice Initiative.](https://support.eji.org/give/153413/#!/donation/checkout)

This document explains how to contribute changes to RE2. It assumes you have installed RE2 using the [installation instructions](Install).

## Discuss your design
RE2 welcomes submissions but please let everyone know what you're working on if you want it to become part of the main repository.

Before undertaking to write something new for RE2, send mail to the [mailing list](http://groups.google.com/group/re2-dev) to discuss what you plan to do. This gives everyone a chance to validate the design, helps prevent duplication of effort, and ensures that the idea fits inside the goals for the language and tools. It also guarantees that the design is sound before code is written; the code review tool is not the place for high-level discussions.

In short, send mail before you code.  And don't start the discussion by mailing a change list!

## Testing
Before sending code out for review, run all the tests for the whole tree to make sure the changes don't break other packages or programs:

<pre>
$ cd your_re2_root
$ make test
</pre>

The test output should end with the line ` ALL TESTS PASSED. `
(Make may print an ` rm ` command after that.)

You should also add tests covering the code you are adding.  If this is a bug fix, add a test that checks the bug is really fixed.

## Code review

Changes to RE2 must be reviewed before they are submitted, no matter who makes the change. (In exceptional cases, such as fixing a build, the review can follow shortly after submitting.) 
The code review process is managed by using git to submit to the code review server.

### Configuring your Git client

Start by double-checking that you have cloned your Git repository from https://code.googlesource.com/re2, not from GitHub. That server is the code review server, running Gerrit.

<pre>
$ git config remote.origin.url
https://code.googlesource.com/re2
</pre>

Next, configure a command shortcut <code>git upload</code>.

<pre>
$ git config alias.upload 'push origin HEAD:refs/for/main'
</pre>

Next, install the Gerrit commit hook, which adds a Change-Id line to any commit you make.

<pre>
$ cd .git/hooks
$ ln -s ../../lib/git/commit-msg.hook commit-msg
</pre>

If you don't have them set globally already, set the default user name and email address to use in commits.

<pre>
$ git config user.name "Grace R. Emlin"
$ git config user.email gre@swtch.com
</pre>

### Creating a change

The code review process requires that each change live in a branch with exactly one commit beyond the main branch.
Start by switching to a new branch; you can choose any name. In this example we'll use <code>bugfix</code>

<pre>
$ git checkout -b bugfix
</pre>

Now make whatever changes you need to make, and commit them with <code>git add</code> and <code>git commit</code>.

<pre>
$ git add re2/re2.cc
$ git commit
</pre>

The first line of the commit description is conventionally a one-line summary of the change and is used as the subject for code review mail; the rest of the description elaborates. For example:

<pre>
fix bug in simplifier

See Bimmler and Shaney, ``Extreme automata,'' J. Applied Math 3(14).
Fixes #159.
</pre>

The special sentence “` Fixes #159. `” associates the change with issue 159 in the RE2 issue tracker. When this change is eventually submitted, the issue tracker will automatically mark the issue as fixed.

If you need to revise the change after <code>git commit</code>, use <code>git commit --amend</code> to rewrite the commit
instead of creating a new commit.

<pre>
$ git add re2/re2.h
$ git commit --amend
</pre>

### Synchronize your client

While you were working, others might have submitted changes to the repository. To update your client, run

<pre>
$ git fetch origin
$ git rebase origin/main
</pre>

If files you were editing have changed, Git does its best to merge the remote changes into your local changes. It may leave some files to merge by hand.
After making any necessary edits, commit them using <code>git commit --amend</code>, as usual.

### Log in to the code review site

In order to upload a change, you must log in to the code review site, obtain a password, and store
that password where Git can find it. You only need to do this for your first change.
Subsequent changes will use the same password.

Open your web browser and log in to https://code-review.googlesource.com/.
Visit https://code-review.googlesource.com/#/settings/http-password and click “Obtain Password.”
After selecting which Google Account to create a Git password for, you should end up on a page
with a password and instructions for installing that password for use by Git.
Follow those instructions.

### Uploading a change

When the change is ready, upload it using <code>git upload</code>, which you defined earlier.

<pre>
$ git upload
</pre>

Uploading the change will trigger mail to the RE2 developers that a new change is ready.

### Reviewing code

Running ` git upload ` will send an email to you and the reviewers asking them to visit the issue's web page and make coments on the change. When done, the reviewer sends comments back using the web page.

### Revise and upload

You will probably revise your code in response to the reviewer comments. When you have revised the code and are ready for another round of review, update the change as before, with <code>git add</code> and <code>git commit --amend</code>, and then re-run <code>git upload</code>.

In addition to the <code>git upload</code>, you should visit the code review web page and reply to the comments, letting the reviewer know that you've addressed them or explain why you haven't.
Once your line-by-line comment replies are ready and you've uploaded the new version, click “Reply” and enter “PTAL” (please take another look) as the message.

The reviewer can comment on the new copy, and the process repeats. The reviewer approves the change by replying with a +1.
Trusted reviewers can give the change a +2 score and submit it by clicking the “Submit”  button.
When that happens, you get an email that the code has been submitted.

The change is submitted with additional metadata in the change description, so you will not be able to merge it with
your work directly. 
Instead, switch back to the main branch, discard the old branch, and pull your work back into main.

<pre>
$ git checkout main
$ git branch -d bugfix
$ git pull
</pre>

## Copyright

Files in the RE2 repository don't list author names, both to avoid clutter and to avoid having to keep the lists up to date. Instead, your name will appear in the [Git change log](https://github.com/google/re2/commits/main) and in the [CONTRIBUTORS](https://github.com/google/re2/blob/main/CONTRIBUTORS) file and perhaps the [AUTHORS](https://github.com/google/re2/blob/main/AUTHORS) file.

The [CONTRIBUTORS](https://github.com/google/re2/blob/main/CONTRIBUTORS) file defines who the RE2 contributors—the people—are; the [AUTHORS](https://github.com/google/re2/blob/main/AUTHORS) file, which defines who “The RE2 Authors”—the copyright holders—are. The RE2 developers at Google will update these files when submitting your first change. In order for them to do that, you need to have completed one of the contributor license agreements:

  * If you are the copyright holder, you will need to agree to the [individual contributor license agreement](http://code.google.com/legal/individual-cla-v1.0.html), which can be completed online.

  * If your organization is the copyright holder, the organization will need to agree to the [corporate contributor license agreement](http://code.google.com/legal/corporate-cla-v1.0.html).  (If the copyright holder for your code has already completed the agreement in connection with another Google open source project, it does not need to be completed again.)

This rigmarole needs to be done only for your first submission.

Code that you contribute should use the standard copyright header:

<pre>
// Copyright 2010 The RE2 Authors. All rights reserved.
// Use of this source code is governed by a BSD-style
// license that can be found in the LICENSE file.
</pre>
