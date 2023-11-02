## CKA Exam Question
Monitor the logs of pod foobar and:<br>
&emsp; Extract log lines corresponding to error "unable-to-access-website"<br>
&emsp; Write them to /opt/KUSC00401/foobar

 Ans:
 
 ```kubectl logs foobar | grep -i unable-to-access-website > /opt/KUSC00401/foobar ```
