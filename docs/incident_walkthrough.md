# Incident Walkthrough

## Scenario

Support receives a ticket reporting that several users cannot complete verification after submitting their documents.

## Triage Questions

- Are failures isolated to one user or repeated across multiple users?
- Do failures share the same error reason?
- Are webhook deliveries failing after verification attempts?
- Are there duplicate user records that could affect workflow state?

## Investigation Steps

1. Run `python scripts/seed_db.py` to create sample data.
2. Run `python scripts/report.py` to execute the investigation queries.
3. Review `failed_verifications.sql` for recent failure patterns.
4. Review `duplicate_failed_webhooks.sql` for repeated downstream delivery failures.
5. Review `duplicate_users.sql` to check for data quality issues.

## Example Findings

The query results may show:

- multiple failed verification attempts with the same failure reason
- repeated webhook delivery failures for the same verification ID
- duplicate user records tied to the same email address

## Support Conclusion

If the failures cluster around repeated webhook delivery issues, the next action is to escalate with:

- affected verification IDs
- user impact summary
- repeated error signature
- timestamp range
- query names used for evidence

This keeps the escalation grounded in data instead of general symptoms.
