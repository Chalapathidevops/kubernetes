Create a new nginx ingress resource as follows: - Name: pong - Namespace: ing-internal - Exposing service hi on path /hi using service port 5678 The availability of service hi can be checked using the following command, which should return hi: #curl -kL <INTERNAL_IP>/hi