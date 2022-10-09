# Part 2 - Deploy It Manually

So you have a web service you've built on your own? Great! Now you need to deploy it somewhere and make it accessible to everyone.

NOTE: This will cost money. Ensure you understand the limits of the free tier of the provider you choose and turn off or delete any resources you create when you are finished with them.

- Spin up a cloud hosting account. You can use any cloud provider (GCP, Azure, DigitalOcean, Linode, etc) but AWS is the most popular. You will need to add a credit card. Costs for AWS should be very minimal as we'll try to keep everything in the free tier.
- Create a new server in that environment. Depending on which cloud provider you chose, you may need to also set up networking.
  - For AWS, this is a good place to start: https://aws.amazon.com/ec2/getting-started/
- Install the required software on your server to run the application. This includes the database, the web server, the application server if necessary, and so on. For python and flask, see https://flask.palletsprojects.com/en/2.0.x/tutorial/deploy/
- Register a domain. This can be specific to your service or more broad. I recommend every engineer owns a domain and their projects can be hosted on it along with their portfolio or resume. Namecheap is a good choice.
- Get a DNS host. If you used Namecheap, this is included for free.
- Choose how you want your project to be accessed. I recommend keeping it simple and making it a subdomain of your new domain. ie `myproject.mydomain.com`
- Ensure you can reach your service from the internet.
- Now we need to add HTTPS! For this, just use [Let's Encrypt](https://letsencrypt.org/).
- Ensure all of the steps you took were documented in your project.
- Show it off to your friends, coworkers, whatever! Celebrate.

### Acceptance Criteria
1. Your service is accessible over the internet.
2. You can access it via a nice URL (myproject.mydomain.com)
3. Traffic to and from your service is encrypted. Bonus points for a good score on [SSL Labs Server Test](https://www.ssllabs.com/ssltest/).

---

[Continue to Part 3](part3.md)