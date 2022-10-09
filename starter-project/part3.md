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

---

[Continue to Part 4]