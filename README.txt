==============================================================================
This library was created by SpiderOak, Inc. and is released under the GPLv3.
https://spideroak.com/
codefeedback@spideroak.com
==============================================================================

SpiderOak zipstream module

zipstream.py is a zip archive generator based on zipfile.py. It was created to
generate a zip file on-the-fly for download in a web.py (http://webpy.org/)
application. This is beneficial for when you want to provide a downloadable
archive of a large collection of regular files, which would be infeasible to
generate the archive prior to downloading.

The archive is generated as an iterator of strings, which, when joined, form
the zip archive. For example, the following code snippet would write a zip
archive containing files from 'path' to a normal file:

zf = open('zipfile.zip', 'wb')
for data in ZipStream(path):
    zf.write(data)
zf.close()

Since recent versions of web.py support returning iterators of strings to be
sent to the browser, to download a dynamically generated archive, you could
use something like this snippet:

def GET(self):
    path = '/path/to/dir/of/files'
    zip_filename = 'files.zip'
    web.header('Content-type' , 'application/zip')
    web.header('Content-Disposition', 'attachment; filename="%s"' % (
        zip_filename,))
    return ZipStream(path)

If the zlib module is available, ZipStream can generate compressed zip
archives.

Contact the SpiderOak team at spideroak_tools@spideroak.com

And be sure to back up your files! http://www.spideroak.com
