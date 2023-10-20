## CKA Exam Question
Monitor the logs of pod foobar and:
  - Extract log lines corresponding to error "unable-to-access-website"
  - Write them to /opt/KUSC00401/foobar

 Ans:
 
 ```kubectl logs foobar | grep unable-to-access-website > /opt/KUSC00401/foobar ```