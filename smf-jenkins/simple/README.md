
```
jenkins@solaris:~$ svcbundle -o jenkins.xml -s service-name=site/jenkins \
-s model=child -s instance-name=default \
-s start-method="java -jar /export/home/jenkins/jenkins.war"
```


Already apply th following patch:
```
jenkins@solaris:~$ gdiff -c jenkins_orig.xml jenkins.xml
*** jenkins_orig.xml    Wed Dec  9 00:38:45 2015
--- jenkins.xml Wed Dec  9 00:39:27 2015
*** 15,21 ****
              <service_fmri value="svc:/milestone/multi-user"/>
          </dependency>
          <exec_method timeout_seconds="60" type="method" name="start"
!             exec="java -jar /export/home/jenkins/jenkins.war"/>
          <!--
              The exec attribute below can be changed to a command that SMF
              should execute to stop the service.  See smf_method(5) for more
--- 15,29 ----
              <service_fmri value="svc:/milestone/multi-user"/>
          </dependency>
          <exec_method timeout_seconds="60" type="method" name="start"
!             exec="java -jar /export/home/jenkins/jenkins.war">
!               <method_context>
!                   <method_credential group='nobody'
!                       privileges='basic,net_privaddr' user='jenkins'/>
!                   <method_environment>
!                       <envvar name='JENKINS_HOME' value='/export/home/jenkins'/>
!                   </method_environment>
!               </method_context>
!       </exec_method>
          <!--
              The exec attribute below can be changed to a command that SMF
              should execute to stop the service.  See smf_method(5) for more
```
