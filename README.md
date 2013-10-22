rmdupes
=======

Remove duplicate files in one directory hierarchy from another
directory hierarchy; think of it as inverse rsync.

## why? ##

At one point, Mike thought it was a good idea to include 3rd party
source in our git repository, so he untar'd the files and committed
them. In retrospect, this wasn't a great idea and we've had these
files building up which we can't change and upgrading is a pain.

Wouldn't it be nice to remove those files from the repo? But which
ones were they? The original git commit also included some of our own
proprietary changes to our own files.

Well, I have the original tarball. Let's just untar it and see what
was in there. But how do we know which files we have changed and we
need to keep? Ah. Now you see. `rmdupes` crawls two file system
hierarchies and finds files that are *identical*: same name, same
(relative) path, and same SHA digest. These are the ones we want to
remove.

## installation ##

Just copy `rmdupes` in your `$PATH` and `chmod 0755 rmdupes`.

## options ##

  * `--verbose`: print what's happening
  * `--debug`: print what's not happening
  * `--dry-run`: don't actually delete anything
  * `--symlinks`: also remove symlinks that point to the same place

## usage ##

    rmdupes /path/to/foo /some/other/bar

Any files in `foo` that also appear in `bar` and which are *identical*
(same SHA-1 digest) will be removed from the `bar` hierarchy.

If you want to see what would be done (but wasn't):

    rmdupes /path/to/foo /some/other/bar --verbose --dry-run

If you want to see identical files (like `rsync`):

    rmdupes /path/to/foo /some/other/bar --debug --dry-run

## author ##

Scott Wiersdorf, <scott@perlcode.org>
