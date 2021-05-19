# Starter Project

Because a DevOps Engineer is not an entry-level position, you need to be able to demonstrate your skills to employers to make it in this field. You will need to show off your skills in systems management, networking, development, and release management. The projects in this repo will give you some foundations to build on and let you build a portfolio to exhibit your new-found skillset.

This is *not* a comprehensive guide on everything you need to know, it is only a rough outline to get you familiar with much of the typical work in this field.

A few tips:
1. Read the section in its entirety before starting on it.
2. Take your time.
3. At the bottom of each section will be a list of acceptance criteria. You should do your best to meet every item.
4. Feel free to [submit an issue](https://docs.github.com/en/github/managing-your-work-on-github/creating-an-issue) to this repo for assistance.

# Part 0 - Requirements

1. Get a Github account. You need somewhere to save your code and to show it off! If you've never used git before, [start here](https://product.hubspot.com/blog/git-and-github-tutorial-for-beginners). Feel free to switch out for Gitlab if you prefer, just remember to adjust the instructions below to your needs.
2. Get a good code editor. If you don't already have a favorite, VS Code is a good choice and works on all platforms.
3. Set aside some time several times per week to work on this. Don't let it stagnate.
4. Any computer you have access to will be able to perform all these steps. You do not need special equipment.
5. A credit card. Costs will be minimal but you will probably need to spend a little money here, <$100 USD.

# Part 1 - Build Something

If you are going to support a development organization, you need to understand what it takes to build software. This will not get you the full exposure of a software engineering position but will help you get familiar with softare development in general.

You will need to build a web service that performs some task. This can be anything you want! I recommend building something relevant to your interests. Choose any language or framework you feel most comfortable with.

Go as far and wide as you want for this service. Keep it as just a simple HTTP endpoint or go big and build a nice HTML/CSS/JS UI around it too! Bonus points if you separate the two into separate services.

Your service should have the following basic parts, however:

1. Should talk HTTP. This ensures the service you build will be ready for the next parts. It also let's anybody interact with it!
2. Should be stored in a Github repo.
3. Should follow the principals of the [twelve factor app](https://12factor.net/). Importantly, never commit credentials to your repo!
4. Intentionally leave out one or two features you would like to implement. We'll follow up on those later. Create issues in Github to track the progress of those missing features.

If you are stuck on what to build, here are a few project ideas to get you started. Feel free to modify them as you wish. Or build multiple to start getting comfortable!

1. Warm up: A basic HTTP service that performs basic arithmetic. The service should accept a POST with two or more numbers and perform an operation against them as specified by the user.
2. Build a basic blog engine. The website will consist of one page where blog posts are displayed and another where blog posts are submitted. The blog contents will be stored in a database.
3. Build an image hosting website. The website will allow users to upload an image that will then be hosted by your website, similar to Imgur. You should process the images so that you have a thumbnail, the original image, and an image with a watermark on top of it. All of these should be available to the user after uploading. The user should also have a way to delete the image later.

Not sure which language or framework to choose? Use Python and Flask. [See here for a tutorial](https://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-i-hello-world).

Ensure the project is well documented and includes a README to introduce readers to it and explains how to run it.

### Acceptance criteria
1. Your service exposes an HTTP endpoint and performs some logic based on user input.
2. Your application code is saved in a Github repo.
3. Includes a README.md at the root level with screenshots and instructions on how to build and run it.
4. Follows the principles in [The Twelve Factor App](https://12factor.net).

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

# Part 3 - Infrastructure as Code

Delete everything you just deployed manually. All the servers, all the network configuration. Everything. We will rebuild!

We're going to take all the lessons learned from Part 2 and make them repeatable, auditable, and executable. We're talking about Infrastructure as Code (IaC)! If you're not familiar with IaC, go read [this article](https://stackify.com/what-is-infrastructure-as-code-how-it-works-best-practices-tutorials/).

Generally speaking, in any modern deployment, you will have two "tiers" of IaC.
- One for configuring the infrastructure layer -- everything below the server OS. This includes networking, the servers themselves, security controls, databases, third party services, and so on. Typically, this will be one or more of the following tools:
  - Terraform
  - AWS Cloudformation
  - GCP Deployment Manager
  - Azure Resource Manager
- Another for configuring the deployment targets. This includes, but is not limited to, the server OS and kubernetes objects. Typical tools include:
  - Ansible
  - Chef
  - Puppet
  - Helm

For your project, you will use [Terraform](https://www.terraform.io/) and [Ansible](https://www.terraform.io/). These are free tools that have wide community and enterprise support. Whichever cloud provider you chose to work with will likely have support in Terraform.

1. Create separate repos for your terraform and ansible projects.
2. Start working on terraform. Create all the infrastructure-level components from Part 2. Networking, servers, etc. If your project uses a database, use your cloud provider's hosted database offering.
    - It's okay to _not_ configure the OS of your server at this stage. Just get an empty server deployed for now.
    - Your goal should be to never have to touch the GUI in your cloud provider's console, save setting up some initial credentials to allow access from Terraform.
    - Keep your terraform code reasonably simple at this stage. Avoid using third-party modules so you can learn how Terraform and your cloud provider work.
    - Do not commit your terraform state to your git repository.
        - Why? Terraform state may contain secrets which you wouldn't want to expose. Add it to your `.gitignore`
        - Instead, use a remote backend or just keep it locally for now. For example, if you use AWS, you can use the S3 backend. See https://www.terraform.io/docs/language/settings/backends/index.html
3. Now work on ansible. You will need to configure the entire OS from Ansible to get your software deployed. To keep it simple, ansible should download your project you developed in Part 1 from github.
    - Your initial setup can use a static inventory file -- some IP addresses or hostnames you manually enter into a text file.
    - Configure the OS with the appropriate software to run your application
    - I highly recommend reviewing [this directory layout](https://dev.to/tmidi/ansible-directory-layout-5edj). Ansible is sometimes too flexible in terms of how you organize your file structure. This helped me immensely when trying to wrap my head around it.
    - Consider applying various security settings based on the CIS Benchmark for your OS of choice.
    - The software you created in Part 1 should start automatically. You shouldn't need to manually log in to the server (except during troubleshooting). It should also start automatically in the event of a reboot.
    - Once you are happy with the configuration, switch to using dynamic inventory. This will be important later as the IP addresses and hostnames of our servers will not be known in advance. This is the case for most modern software deployments.
      - For AWS EC2, see https://devopscube.com/setup-ansible-aws-dynamic-inventory/
      - For DigitalOcean, see https://www.digitalocean.com/community/tools/do-ansible-inventory

When everything is configured and you can successfully access your site, run `terraform destroy`. Take a deep breath. Then run `terraform apply` and apply ansible to your new servers. If you did this correctly, your new site should be running again with just a couple of commands from your local development environment.

### Acceptance Criteria
1. All terraform code is checked in to a Github repository.
2. Your terraform state should _not_ be in the Github repository.
3. Your ansible code is in a different repository.
4. The server can tolerate a reboot and come back online without intervention.
5. A strong resolve in the wake of smoldering servers.

# Part 4 - Continuous Integration and Automated Deployment

Read about [Continuous Integration](https://www.cloudbees.com/continuous-delivery/continuous-integration).

During development of modern software, it is common to use [git flow](https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow) or some variant of it for teams to collaborate on changes to their projects.

When changes are made to a git repo, we can automatically perform some actions based on what is being done. Every major git repo host will support either their own Continuous Integration tooling or allow you to hook in your own (such as Jenkins). Your goal should be to never log in to a server yourself to deploy new code.

Using [Github Actions](https://github.com/features/actions), perform the following:

1. When a pull request is submitted against your project's repository, run various tests against your code to verify it is not broken. For example:
    - Unit tests
    - Code linting tests (black for Python formatting, mypy for python type checking)
    - Security auditing tests (bandit for python)
2. When a pull request is approved and merged to the main (or master) branch, perform those tests again.
3. When a tag is pushed to your repo, deploy the software to your hosting environment.
    - There are a few ways to go about this. For now, just use a basic semantic versioning schema. For example: pushing tag `v0.1.0` would deploy to your hosting environment.
    - Ensure tags that do not fit the schema you set (in the above example, tags starting with `v`) do not deploy.
    - The deployment methodology between each company and team may differ. For example, a merge to master may deploy to a development environment. Or a pull request may deploy that branch to an entirely new environment created just for that PR. For now, keep it simple.
4. For this project, simply run ansible as your deployment step. You should be able to define in your ansible vars which tag from your git repo to deploy.
    - Ensure any secrets (ssh keys, api keys) are not available to the public. Ensure these keys are not available to any CI tools (including actions) in pull requests. This prevents credential leakage.
5. Develop a new feature and deploy it!

### Acceptance Criteria
1. Pull requests against your repo get scanned or tested automatically.
2. Merges to your main/master branch are scanned or tested in the same way.
3. Tags pushed to your repo are deployed automatically.

# Part 5 - Monitoring and Logging

Imagine your service is long lived and you have many happy, paying customers. How do you ensure they _remain_ happy, paying customers? It is a foregone conclusion that the most popular services on the web are up 24/7 but it takes a lot of engineering work to keep it that way. You need to ensure that your services remain available and performant and that issues are resolved quickly.

In Part 5, you will be deploying monitoring and logging services. For the purposes of this project, they can exist on a single server. However, they should exist on a separate one from the one hosting your service.

There are many commercial products that can help you here. Popular examples are DataDog, New Relic, AWS CloudWatch, and Dynatrace. These are worth exploring and some have a free tier. Open source examples include the Elastic stack, Zabbix, Graphite, and Influxdb. However, for the purposes of this project, we will be deploying [Prometheus](https://prometheus.io/) for metrics collection, [Loki](https://grafana.com/oss/loki/) for logs, and [Grafana](https://grafana.com/) for visualizations.

I highly recommend reading up on the [official Prometheus documentation](https://prometheus.io/docs/prometheus/latest/getting_started/). [This overview] is also a very good high-level overview of the Prometheus ecosystem.

Perform the following:
1. Install [node exporter](https://github.com/prometheus/node_exporter) on your application server. Expect that this will be installed on every server you deploy in the future.
2. Add a new server deployment to your Terraform repository. This will be the server we use for our monitoring and logging services.
3. Using Ansible, install Prometheus on it.
4. Configure Prometheus to scrape the node exporter endpoint on your application server and monitoring server.
    - Ensure you have configured the prometheus server to have network access to the application server's node exporter endpoint.
    - Depending on the cloud provider you chose, this may change how you approach it. If the networking layer for your cloud provider offers a firewall attached to each server instance (AWS Security Group, GCP Firewall Rules), use terraform to configure the firewall on the instance. You will need to configure the OS-level firewall if your cloud provider does not have firewall rules managed outside of the server instance.
    - Node exporter should _only_ be accessible to your monitoring server and, perhaps, your public IP. The wide internet should not have access.
5. Using Ansible, install Alertmanager.
6. Configure Prometheus to send alerts to Alertmanager.
7. Configure some basic alerts in Prometheus for your application server. For example, if disk usage is greater than 90% or if any server is unreachable.
8. Configure Alertmanager to forward alerts to you
    - TODO: Make some recommendations on easy ways to receive alerts. Idea: Create a free personal slack workspace.
9. Using Ansible, install Grafana.
10. Install the [community node exporter dashboard](https://grafana.com/grafana/dashboards/1860). This will get you some visualizations quickly.
    - You don't need to do this part with Ansible. But if you did, it would be copying the Dashboard json to the correct location and restarting Grafana.
11. Using Ansible, Install Loki.
12. Using Ansible, Install Promtail on both servers. Configure it to send the following to Loki:
    - Application server's access and error logs
    - Application server's audit logs (SSH logins, sudo access denied, etc)
    - Grafana logs
    - Prometheus logs
    - Alertmanager logs

    I recommend configuring `file_sd_configs` in Promtail and placing a service-specific config file in the specified directory from each of the above's ansible playbook. This lets the individual services in ansible configure their logging themselves.
13. Configure Grafana so that you can view logs from Loki.

Loki reference
- https://grafana.com/go/webinar/intro-to-loki-like-prometheus-but-for-logs/?pg=oss-loki&plcmt=hero-txt
- https://grafana.com/docs/loki/latest/clients/promtail/


### Acceptance Criteria
1. You should be able to deploy each component (Prometheus, Alertmanager, Grafana) to a separate server in Ansible with minimal additional effort (hint: keep them in separate playbooks/roles)
2. Every server has basic stats available in Grafana (CPU/Memory/Disk Usage)
3. Application logs (access logs, error logs) should be accessible from Grafana.
4. Only the monitoring server and a technician (you) should have access to any exporters.
5. Only Grafana and a technician (you) should have access to the Prometheus and Alertmanager endpoints.
6. Of course, this should all be configured with code. You should be able to destroy these servers and have a full environment back up in under 10 minutes.

# Part 6 - Extending your dashboards with service metrics

Part 5 had a lot of interesting goodies about monitoring your _servers_ but nothing about the _services_ that run on top of them. In this section, you'll be expanding your service by adding metrics for Prometheus to scrape. Prometheus provides libraries for almost any popular language and framework to allow you to define your own custom metrics as well as exposing some metrics about your application without any additional workrequired by you.

If you are using Python+Flask, you could use https://pypi.org/project/prometheus-flask-exporter/.

### Acceptance Criteria
1. An interesting dashboard with your application's metrics. Should include at a minimum:
    - Request latency for each route
    - Number of times each route is called
    - Total requests per minute
    - Memory usage of the application server process

# Part 7 - High Availability and Disaster Recovery

TODO

# Part 8 - Document, Document, Document

At the end of your project, anyone should be able to view your repositories and their documentation and spin up their own copy of your service in its entirety without any additional assistance. If you intend for potential employers to understand what you did, you need to make it easy and obvious for them.

# How do I stand out?

Now that you have a service that is deployed and showcased, how do you differentiate yourself from the other people doing the same?

- Add unit tests and/or to your code
- Make your website look pretty.
- TODO
