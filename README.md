# smf-jenkins
solaris smf manifest for Jenkins

```
# cp manifest/svc-jenkins /lib/svc/manifest/site
# cp method/svc-jenkins /lib/svc/method
# svcadm restart manifest-import:default
```

```
# svcprop -p options jenkins
options/httpListenAddress astring 0.0.0.0
options/http_port count 8080
options/prefix astring /jenkins
```


Example: Changing the http_port (--httpPort option)
```
# svccfg -s jenkins setprop  options/http_port='8081'

# svcadm refresh jenkins
jenkins@solaris:~/Git/smf-jenkins$ svcprop -p options jenkins
options/httpListenAddress astring 0.0.0.0
options/prefix astring /jenkins
options/http_port count 8081
```
