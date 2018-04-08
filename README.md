# Glue

Glue is the simplest way to upload and retrieve files on the web. 

To push a file, simply do: 

```
$ curl http://glue.io --upload-file mario-ascii-art.txt 
{"key":"589a111a5cd04fcb8e280421a21b47977c03bd47e015427cbf374d051be40d7f"}
```
Use this key to fetch this this file:

```
$ curl http://glue.io/589a111a5cd04fcb8e280421a21b47977c03bd47e015427cbf374d051be40d7f
── ── ── ── ── ── ── ██ ██ ██ ██ ── ██ ██ ██ ── 
── ── ── ── ── ██ ██ ▓▓ ▓▓ ▓▓ ██ ██ ░░ ░░ ░░ ██ 
── ── ── ── ██ ▓▓ ▓▓ ▓▓ ▓▓ ▓▓ ▓▓ ██ ░░ ░░ ░░ ██ 
── ── ── ██ ▓▓ ▓▓ ▓▓ ██ ██ ██ ██ ██ ██ ░░ ░░ ██ 
── ── ██ ▓▓ ▓▓ ▓▓ ██ ██ ██ ██ ██ ██ ██ ██ ░░ ██ 
── ── ██ ▓▓ ██ ██ ░░ ░░ ░░ ░░ ░░ ░░ ██ ██ ██ ── 
── ██ ██ ██ ██ ░░ ░░ ░░ ██ ░░ ██ ░░ ██ ▓▓ ▓▓ ██ 
── ██ ░░ ██ ██ ░░ ░░ ░░ ██ ░░ ██ ░░ ██ ▓▓ ▓▓ ██ 
██ ░░ ░░ ██ ██ ██ ░░ ░░ ░░ ░░ ░░ ░░ ░░ ██ ▓▓ ██ 
██ ░░ ░░ ░░ ██ ░░ ░░ ██ ░░ ░░ ░░ ░░ ░░ ██ ▓▓ ██ 
── ██ ░░ ░░ ░░ ░░ ██ ██ ██ ██ ░░ ░░ ██ ██ ██ ── 
── ── ██ ██ ░░ ░░ ░░ ░░ ██ ██ ██ ██ ██ ▓▓ ██ ── 
── ── ── ██ ██ ██ ░░ ░░ ░░ ░░ ░░ ██ ▓▓ ▓▓ ██ ── 
── ░░ ██ ▓▓ ▓▓ ██ ██ ██ ██ ██ ██ ██ ▓▓ ██ ── ── 
── ██ ▓▓ ▓▓ ▓▓ ▓▓ ██ ██ ░░ ░░ ░░ ██ ██ ── ── ── 
██ ██ ▓▓ ▓▓ ▓▓ ▓▓ ██ ░░ ░░ ░░ ░░ ░░ ██ ── ── ── 
██ ██ ▓▓ ▓▓ ▓▓ ▓▓ ██ ░░ ░░ ░░ ░░ ░░ ██ ── ── ── 
██ ██ ██ ▓▓ ▓▓ ▓▓ ▓▓ ██ ░░ ░░ ░░ ██ ██ ██ ██ ── 
── ██ ██ ██ ▓▓ ▓▓ ▓▓ ██ ██ ██ ██ ██ ██ ██ ██ ── 
── ── ██ ██ ██ ██ ██ ██ ██ ██ ██ ██ ██ ▓▓ ▓▓ ██ 
── ██ ▓▓ ▓▓ ██ ██ ██ ██ ██ ██ ██ ██ ▓▓ ▓▓ ▓▓ ██ 
██ ██ ▓▓ ██ ██ ██ ██ ██ ██ ██ ██ ██ ▓▓ ▓▓ ▓▓ ██ 
██ ▓▓ ▓▓ ██ ██ ██ ██ ██ ██ ██ ██ ██ ▓▓ ▓▓ ▓▓ ██ 
██ ▓▓ ▓▓ ██ ██ ██ ██ ██ ── ── ── ██ ▓▓ ▓▓ ██ ██ 
██ ▓▓ ▓▓ ██ ██ ── ── ── ── ── ── ── ██ ██ ██ ── 
── ██ ██ ── ── ── ── ── ── ── ── ── ── ── ── ──

```

Delete an existing file using its key: 

```
$ curl -X DELETE http://glue.io/589a111a5cd04fcb8e280421a21b47977c03bd47e015427cbf374d051be40d7f
{"err":"none"}
```

Glue can detects mime types even if they are not specified in the original request:

```
$ curl -v http://glue.io --upload-file /path/to/some/pic.jpg
{"key":"f7e124f754ed42ba80efb394fb6d49de159f8f4eef234b8d8bf5537ff3f3987a"}
```

Point your browser to [http://glue.io/f7e124f754ed42ba80efb394fb6d49de159f8f4eef234b8d8bf5537ff3f3987a](http://glue.io/f7e124f754ed42ba80efb394fb6d49de159f8f4eef234b8d8bf5537ff3f3987a) to see the image.

![Render images in browser](https://raw.githubusercontent.com/wicknicks/uploads/master/success-kid-glue.png)


Glue is meant to be a simple way for developers to share files with each other, without having to setup SSH keys or create accounts with popular file sharing services. For this reason, we impose the following limits:

1. Only files up to 16MiB are allowed.
2. Files which have not been retrieved for over 30 days may be deleted.
3. A max of 100 uploads per hour and 1000 uploads per day.
4. Finally, do not upload sensitive or private information. 
