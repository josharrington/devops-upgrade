# Part 7 - High Availability

In production, a service must be able to withstand an outage of a single component of the stack. This is particularly true in many cloud scenarios where a single server can be destroyed at a moment's notice.

Perform the following:

1. Deploy two or more identical servers that hosts your service. If you're on a major cloud provider such as AWS, ensure the server can automatically be recovered in the event of a server failure. For AWS, this means using an autoscaling group.
2. Set up a load balancer to check the health of your service on each server and split the traffic between the two servers.
3. Configure your https certificate to terminate at the load balancer instead of at the individual server. If you're using AWS, use ACM.
4. If your service requires a login or has any session, ensure that my request can be serviced by _any_ server behind your load balancer. (Investigate where the best place to store session information is for your particular framework and language. Redis or your DB are good options)
5. Ensure no state on any particular server lives outside of a single request. This means any file uploads are moved off the server after processing, for example.

You should now have a robust service that can withstand a single application server outage. Destroy to your heart's content!

Setting this up isn't just useful for server outages, however. You can take advantage of the high availability to deploy new versions of your application in a rolling deployment. If you're using an autoscaling group in AWS, this would mean either creating a new autoscaling group or modifying the parameters of the autoscaling group and issuing an instance refresh. If your particular cloud provider does not have something akin to an autoscaling group, this can be an ansible playbook or script that fetches the existing hosts dynamically and installs the new software onto each server. Make sure the servers are not receiving traffic when this occurs, take them out of the load balancer first!

### Acceptance Criteria
1. Your service can withstand a single server outage and not be impacted.
2. Your application logs should contain the _real_ ip of the client and not of the load balancer. (See X-Forwarded-For headers)
3. You can deploy a new version of your service without any downtime.

---

[Continue to Part 8](part8.md)