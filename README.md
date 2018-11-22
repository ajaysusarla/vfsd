# vfsd

Daemon that listens for files to be inserted into the VFS

vfsd listens to port 9908 for TCP connections which obey the following
protocol:

`GET [sha1] [size]\n`

after which the server responds with:

`OK [sha1] [size]\n`

followed by the entire file, or:

`NO [error]\n`

followed by disconnecting.

The other command is:

`PUT [sha1] [size]\n`

after which the server reads the specified number of bytes from the
wire and calculates the sha1 and size. Upon success it inserts the
file into place and returns:

`OK [sha1] [size]\n`.

If there is any error it returns:

`NO [error]\n`

Either way it closes the connection.

