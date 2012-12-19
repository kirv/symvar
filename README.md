symvar
======

using non-resolving symbolic links as variables on the filesystem


introduction
======

It is common to store settings in 'INI' or 'RC' files, typically with 
the contents as readable text, following any number of arbitrarily 
different if simple formats.

My interest was in storing single named settings, and, after trying and
using various solutions, I've found that symbolic links are a good fit 
for this need.

Symbolic links are very convenient and widely used on the Linux filesystem,
and many or most operations on files can work through symbolic inks as if
directly on the targeted files.  Used in the conventional way, a symbolic
link is a kind of alias, giving a file a different name or making the
file appear to be in a different directory than the actual file.

Surprisingly, perhaps, the system tools that create and use symbolic links 
do not require that the links actually point to an existing file or directory.
Such non-resolving symbolic links might indicate a problem, and indeed, there
are tools that can be used to 'clean up' (delete) them, but in my view they
can also be viewed as an unutilized resource.

What is a symbolic link (or symlink for short)?  It is simply an inode, a
named object stored on the filesystem, where the content is 'symbolic' text,
typically the name of a file or directory.  In contrast, an ordinary file 
is also stored using an inode (that's what gives the file its name), but
the content is a pointer to one or more data blocks comprising the file's 
contents.

My goal is to represent arbitrary values in the symlink content, but in order
to try to avoid collisions with actual files, I've adopted a convention to use
a prefix of '=' on the value.  That's still not a guarantee against collisions, 
so another convention is that the symlink does not resolve to a file.  The '='
prefix is not strictly necessary, but may help to prevent accidental collisions,
and also provides a syntactic hint that the symlink is not intended to point at
a file.



