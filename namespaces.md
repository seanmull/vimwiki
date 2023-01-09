Dev name spaces not reachable

- Sharan mentioned this may have to do with the loadbalencer missing on the cluster
- The issue stems from each service sharing the same ip config in the service.yaml
- The service will spin up but all subsequent ones will have a conflict since they will all share the same ip.
- There was also an issue with the build script in live.  It was haveing problems updating the yaml files with the correct namespace name.
- The issue was the xargs command works differently between [os](os) and linux/wsl
- The build script will rebuild the services.
- We also need to map the DNS server to the updated service url. This is done through the route 53 aws service
- 
