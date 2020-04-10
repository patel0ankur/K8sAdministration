Deployment strategies:

1. Recreate - best for development environment:
Pro:
application state entirely renewed
Cons:
downtime that depends on both shutdown and boot duration of the application

2. Rollout:
Pros:
version is slowly released across instances
convenient for stateful applications that can handle rebalancing of the data

Cons:
rollout/rollback can take time
supporting multiple APIs is hard
no control over traffic

3. Blue/Green Deployment:
In blue/green deployment the "green" version of the application is deployed alongside the "blue" version.
After testing that the new version meets the requirements, we update the Kubernetes Service object that plays the role of
load balancer to send traffic to the new version by replacing the version label in the selector field.

Pros:
instant rollout/rollback
avoid versioning issue, change the entire cluster state in one go

Cons:
requires double the resources
proper test of the entire platform should be done before releasing to production
handling stateful applications can be hard

Development/staging environments: a recreate or ramped deployment is usually a good choice.
Production: a ramped or blue/green deployment is usually a good choice, but proper testing of the new platform is necessary.
