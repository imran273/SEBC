## Accepting Changes to the Course Material

Read this file once you've unpacked your course ZIP file 

Please make sure:
a) Your repo is named `SEBC,` not `SEBC-master`
b) The top-level directory in the repo is not `SEBC-master`

Setting the repository name and top-level directories correctly
reduces our evaluation time a great deal. Please do not add work
to your repository until the setup is right.

Once this is done:
* Create an empty repository called `SEBC` on your GitHub account. 
  * Do **not** create a `README.md` file to initialize it.
* Next, right-click the `Clone or download` button to copy your repo's URL.
* In the SEBC directory on your laptop, invoke the following:
  * `git init`
  * `git config --global user.name "<your name>"`
  * `git config --global user.email "<your email address>"`
  * `git remote add origin <paste in the GitHub URL>`

Your local git repo is now ready to <i>push</i> files to your GitHub
repo. In the same directory on your laptop, invoke the following:

* `git status`
* `git add .`
* `git commit -m "Push course materials for Shanghai, May 2017"`
* `git push -u origin master`

If this completes successfully, you can browse your GitHub repo to
see the files have copied to it. If this did not work as expected,
please consult with an instructor.

As stated in `README.md`, **DO NOT** add or change files directly
on your GitHub repo.  Make all file changes locally and push them.
This routine will avoid synchronization problems that can occur
when both copies have been edited in a different way at the same
time.

---

## tl;dr: Why Use GitHub?

You probably have not used a source-code control system with a training course before. We've incorporated
`git` and GitHub into this one for a few reasons.

The outcomes we care most about include:
* Learning to follow existing technical documentation
* Identifying unfamiliar tools and practices
* Letting systems fail when they are configured improperly
* Using mistakes and failures as learning points and teachable moments.

We think PowerPoint slides do not promote hands-on skills development
and the journalling process we use very well. To track and document
your progress, and even annotate the course material to your liking,
we need a system that leaves the teaching content open to change
and active note-taking.

PowerPoint often force the author to paraphrase or gloss richer
sources of information to fit one slide.  We would rather link to
an existing source you can refer to when you need more context or
information.  There are several benefits:

* The source material remains transparent to the viewer
* One source can be replaced with a more comprehensive or recent one easily
* Errors can be traced to the source
* Errors in interpreting the source are eliminated

In addition, slide formatting is a big cost in traditional course
development. In a subject area focused on skills development in
Hadoop -- an ecosystem with dozens of evolving components, all
moving at different rates of development -- the half-life of that
knowledge is short. Static course material has not only a potential
for maintaining an error for a long time. It can also age out quickly
where the refresh window of content development (say, 6-12 months)
is a big multiple of a software release schedule (quarterly).

To mitigate these risks, traditional course development will set
the software release it covers and provide labs written in controlled
environment. Labs may be vetted to a process that proves the labs
work under a variety of failure scenarios. A solution set may be
used both to prove lab integrity and make it possible for anyone
to 'complete' them.  In the interests of time, the student may be
guided carefully on what to type or click.

These labs tend to show the software works as described. By design
they may sidestep showing how the software can be applied to a
reasonable use case that has not been factored into lab design.

---

## Ok, but why should I have to use GitHub?

In short, so we can create a dialog for your learning.

Using the mechanism for creating Issues, we then have a common medium for:

* Citing errors or obsolete references in the course material (they do exist!)
* Documenting your learning process, including failures
* Notifying collaborators of your progress
* Continuously updating the course material
