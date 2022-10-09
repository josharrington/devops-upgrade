# Part 6 - Extending your dashboards with service metrics

Part 5 had a lot of interesting goodies about monitoring your _servers_ but nothing about the _services_ that run on top of them. In this section, you'll be expanding your service by adding metrics for Prometheus to scrape. Prometheus provides libraries for almost any popular language and framework to allow you to define your own custom metrics as well as exposing some metrics about your application without any additional workrequired by you.

If you are using Python+Flask, you could use https://pypi.org/project/prometheus-flask-exporter/.

Additionally, we'll want to have a dashboard full of database metrics if you chose to use a database in your project. Use a Prometheus exporter appropriate for your database vendor. For example, you can use [Postgres Exporter](https://github.com/prometheus-community/postgres_exporter) for PostgreSQL databases.

### Acceptance Criteria
1. An interesting dashboard with your application's metrics. Should include at a minimum:
    - Request latency for each route
    - Number of times each route is called
    - Total requests per minute
    - Memory usage of the application server process

---

[Continue to Part 7](part7.md)