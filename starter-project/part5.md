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

---

[Continue to Part 6](part6.md)