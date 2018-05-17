# SpiderOak zipstream module

## The offical repo is at https://github.com/SpiderOak/ZipStream please use that instead. 


### This library was created by SpiderOak, Inc. and is released under the GPLv3.
* https://spideroak.com/
* codefeedback@spideroak.com


zipstream.py is a zip archive generator based on zipfile.py. It was created to
generate a zip file on-the-fly for download in a web.py (http://webpy.org/)
application. This is beneficial for when you want to provide a downloadable
archive of a large collection of regular files, which would be infeasible to
generate the archive prior to downloading.

The archive is generated as an iterator of strings, which, when joined, form
the zip archive. For example, the following code snippet would write a zip
archive containing files from 'path' to a normal file:

```python
zf = open('zipfile.zip', 'wb')
for data in ZipStream(path):
    zf.write(data)
zf.close()
```

Since recent versions of web.py support returning iterators of strings to be
sent to the browser, to download a dynamically generated archive, you could
use something like this snippet:

```python
def GET(self):
    path = '/path/to/dir/of/files'
    zip_filename = 'files.zip'
    web.header('Content-type' , 'application/zip')
    web.header('Content-Disposition', 'attachment; filename="%s"' % (
        zip_filename,))
    return ZipStream(path)
```

If the zlib module is available, ZipStream can generate compressed zip
archives.

Contact the SpiderOak team at spideroak_tools@spideroak.com

And be sure to back up your files! http://www.spideroak.com


## ZipStream works with HUGE files too!

Generate 6 gigs of random data
```bash
ionadmin@onfire:/results/zip$ dd if=/dev/urandom of=file.blob bs=1048576 count=6000
```

Get the checksum of the generated file
```bash
ionadmin@onfire:/results/zip$ md5sum file.blob
11ef7625569f44977789caa785b5f112  file.blob
```

Now compress it using zipstream

```python
from zipstream import ZipStream
toZip = "/results/zip/file.blob"
zf = open('zipfile.zip', 'wb')
for data in ZipStream(toZip):
    zf.write(data)
zf.close()
```

Check the output zipfile checksum

```bash
ionadmin@onfire:/results/zip/output$ md5sum zipfile.zip
405437edcb0c81d7639e01f8f1e50417  zipfile.zip
```

Unzip the zipped file
`
ionadmin@onfire:/results/zip/output$ unzip zipfile.zip
`

The resulting file checksum

```bash
ionadmin@onfire:/results/zip/output$ md5sum file.blob
11ef7625569f44977789caa785b5f112  file.blob
```

So ZipStream is a great solution if you need to zip large files with Python 2.6.5. 

zipfile with Python 2.6.5 is broken for large files - http://bugs.python.org/issue8571 

Python 2.6.5 is part of Ubuntu 10.04. So this ZipStream is a great solution to zip large files with Python 2.6.5!

