
# List content

https://www.cyberciti.biz/faq/list-the-contents-of-a-tar-or-targz-file/

```
tar -ztvf my-data.tar.gz
tar -jtvf file.tar.bz2
tar -tvf projects.tar.bz2 '*.pl'
```

* **t**: List the contents of an archive.
* **v**: Verbosely list files processed (display detailed information).
* **z**: Filter the archive through gzip so that we can open compressed (decompress) .gz tar file.
* **j**: Filter archive through bzip2, use to decompress .bz2 files.
* **f** filename: Use archive file called filename.
