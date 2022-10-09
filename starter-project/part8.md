# Part 8 - Disaster Recovery

Now that we have a resilient service, we have to talk about the part that was blatantly left out: the database. What happens if _this_ server fails irrecoverably? You lose all your customers!


You need to have a backup plan in place for your database (if your service requires one) and be able to recover from a backup.

Perform the following:

1. Using your cloud vendor's native tools, craft a plan to back up your database server on a nightly, weekly, and monthly basis.
2. Manually trigger a backup or wait for an automatic one to occur.
3. Delete your database.
4. Recover your database.
5. Document the backup and recovery procedure. Ensure you can use your infrastructure as code tooling to perform it.
6. Consider how you would send those backups to somewhere else in case you ever lost access to your cloud account.

Disaster can strike your service at many different levels and you should be aware of the ways to recover from them. Not only could you lose your database but you could lose access to your cloud accounts, have your cloud accounts deleted, forget to renew your credit card information, the whole gambit.

Your infrastructure as code is a critical part of disaster recovery. It is effectively executable documentation on how to deploy your services and infrastructure. In the event you lost all of your infrastructure, how long would it take you to recover today?

### Acceptance Criteria
1. You have backup plans configured for your database.
2. Your backup and recovery procedures are documented.

---

[Continue to Part 9](part9.md)