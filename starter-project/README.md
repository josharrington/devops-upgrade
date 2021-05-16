# Starter Project

Because a DevOps Engineer is not an entry-level position, you need to be able to demonstrate your skills to employers to make it in this field. You will need to show off your skills in systems management, networking, development, and release management. The projects in this repo will give you some foundations to build on and let you build a portfolio to exhibit your new-found skillset.

This is *not* a comprehensive guide on everything you need to know, it is only a rough outline to get you familiar with much of the typical work in this field.

# Part 0 - Requirements

1. Get a Github account. You need somewhere to save your code and to show it off! If you've never used git before, [start here](https://product.hubspot.com/blog/git-and-github-tutorial-for-beginners).
2. Get a good code editor. If you don't already have a favorite, VS Code is a good choice and works on all platforms.
3. Set aside some time several times per week to work on this. Don't let it stagnate.
4. Any computer you have access to will be able to perform all these steps. You do not need special equipment.
5. A credit card. Costs will be minimal but you will probably need to spend a little money here, <$50 USD.

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
3. Now work on ansible. You will need to configure the entire OS from Ansible to get your software deployed. To keep it simple, ansible should download your project you developed in Part 1 from github.
    - Your initial setup can use a static inventory file -- some IP addresses or hostnames you manually enter into a text file.
    - Configure the OS with the appropriate software to run your application
    - Consider applying various security settings based on the CIS Benchmark for your OS of choice.
    - The software you created in Part 1 should start automatically. You shouldn't need to manually log in to the server (except during troubleshooting).
    - Once you are happy with the configuration, switch to using dynamic inventory. This will be important later as the IP addresses and hostnames of our servers will not be known in advance. This is the case for most modern software deployments.
      - For AWS EC2, see https://devopscube.com/setup-ansible-aws-dynamic-inventory/
      - For DigitalOcean, see https://www.digitalocean.com/community/tools/do-ansible-inventory

When everything is configured and you can successfully access your site, run `terraform destroy`. Take a deep breath. Then run `terraform apply` and apply ansible to your new servers. If you did this correctly, your new site should be running again with just a couple of commands from your local development environment.

# Part 4 - Continuous Integration and Automated Deployment

During development of modern software, it is common to use (git flow)[https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow] or some variant of it for teams to collaborate on changes to their projects.

When changes are made to a git repo, we can automatically perform some actions based on what is being done. Every major git repo host will support either their own Continuous Integration tooling or allow you to hook in your own (such as Jenkins). Your goal should be to never log in to a server yourself to deploy new code.

Using [Github Actions](https://github.com/features/actions), perform the following:

1. When a pull request is submitted against your project's repository, run various tests against your code to verify it is not broken. For example:
    - Unit tests
    - Code linting tests (black for Python, mypy for python type checking)
    - Security auditing tests (bandit for python)
2. When a pull request is approved and merged to the main (or master) branch, perform those tests again.
3. When a tag is pushed to your repo, deploy the software to your hosting environment.
    - There are a few ways to go about this. For now, just use a basic semantic versioning schema. For example: pushing tag `v0.1.0` would deploy to your hosting environment.
    - Ensure tags that do not fit the schema you set (in the above example, tags starting with `v`) do not deploy.
    - The deployment methodology between each company and team may differ. For example, a merge to master may deploy to a development environment. Or a pull request may deploy that branch to an entirely new environment created just for that PR. For now, keep it simple.
4. For this project, simply run ansible as your deployment step. You should be able to define in your ansible vars which tag from your git repo to deploy.

# Part 5 - Monitoring and Logging

# Part 6 - High Availability and Disaster Recovery

# Part 7 - Document, Document, Document

At the end of your project, anyone should be able to view your repositories and their documentation and spin up their own copy of your service in its entirety without any additional assistance. If you intend for potential employers to understand what you did, you need to make it easy and obvious for them.

TODO

# How do I stand out?

Now that you have a service that is deployed and showcased, how do you differentiate yourself from the other people doing the same?

- Add unit tests and/or to your code
- Make your website look pretty.
- TODO
