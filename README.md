# staffeli_nt

Staffeli NT Technology


Getting Started
===============

With Staffeli, we work with local course clones. We aim to keep these
clones compatible with git.

We recommend that you create a local directory ``canvas``,
``absalon``, or similar, for all of you Canvas-related local course
clones. Staffeli needs some initial help to be able to login with your
credentials. You need to [generate a
token](https://guides.instructure.com/m/4214/l/40399-how-do-i-obtain-an-api-access-token-for-an-account)
for Staffeli to use, and save it in your home directory in a file with
the name `.canvas.token`.

**NB!** This is your personal token so **do not** share it with others,
else they can easily impersonate you using a tool like Staffeli.
Unfortunately, to the best of our knowledge, Canvas has no means to
segregate or specialize tokens, so this is really "all or nothing".

Install required libraries
--------------------------

    $ pip3 install -r requirements.txt

Or you can install in a [virtual
environment](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/#creating-a-virtual-environment):

 1. Create a virtual environment called `env`.

    On macOS and Linux:

        $ python3 -m venv env

    On Windows:

        $ py -m venv env

 2. Activate `env`

    On macOS and Linux:

        $ source env/bin/activate

    On Windows:

        $ .\env\Scripts\activate

 3. Now install the requirements for `staffeli_nt` in `env`

        $ pip3 install -r requirements.txt




Fetch Submissions for an Assignment
-----------------------------------

Use `download.py <course_id> <template.yaml> <assignment-dir>`. For
instance, to fetch all submissions for "ass1":

    $ <staffeli_nt_path>/download.py 42376 ass1-template.yml ass1


Upload Feedback and grades
--------------------------

Use `upload.py <template.yaml> <assignment-dir> [--live] [--step]`.
The default to do a *dry run*, that is **not** to upload anything
unless the `--live` flag is given.

For instance, to review all feedback for submissions in the directory
`ass1` before uploading:

    $ <staffeli_nt_path>/upload.py ass1-template.yml ass1 --step


To upload all feedback for submissions in the directory
`ass1`:

    $ <staffeli_nt_path>/upload.py ass1-template.yml ass1 --live

To upload feedback for a single submission:

    $ upload_single.py <POINTS> <meta.yml> <grade.yml> <feedback.txt> [--live]


Template format
---------------

A (minimal) template could look like:

```yaml
name: Mini asignment
passing-points: 3

tasks:
  - overall:
      title: Overall
      points: 6
      rubric: |
        Some default feedback.

        Your code and report are unreadable.

        Wow, that's really clever.
```

The field `passing-points` is optional. Adding this field will have
the effect, that the grade posted is `1` if the total sum of points is
greater than or equal to `passing-points`, and `0` otherwise.
