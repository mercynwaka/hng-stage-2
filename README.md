HNG Stage 2 — Blue-Green Deployment with Nginx and Node.js

This project demostrates a BLUE-GREEN deployment setup using docker-compose,Nginx and Node.js(Express) application. It shws how trafffic automatically fails over from the blue app to the green app when failure is induced without causing and disruption.

Project Overview:

Blue app - active version (v1-blue) 
Green app - standby/backup version (v1-green)
Nginx - acts as a load balancer that routes traffic to the healthy app
Docker-compose - orchestrates containers and environment

Nginx monitors both app instances and switches traffic to the healthy one when an upstream fails.

This verifies the baseline(that Blue app is active)
curl -i http://localhost:8080/version

This induce failure/chaos
curl -X GET http://localhost:8081/chaos/error

To verify that it's failing
curl -i http://localhost:8081/

When you run again, it switch to green. It means nginx load balancer automatically failed over to the healthy Green app when blue started failing.
curl -i http://localhost:8080/version

To restore blue to normal operation
curl -X POST http://localhost:8081/chaos/stop

then verify:
curl -i http://localhost:8081/

Ip address: 184.72.88.235:8080
