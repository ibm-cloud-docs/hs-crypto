# Auditing Events in {{site.data.keyword.uko_short}}

All actions performed on keystores, key templates and keys are logged in the audit log Db2 table. This Audit log can be displayed by users with adequate access role. You can find it on the left side menu under **Audit log**.

The Audit log is searchable with the following search options:

* show log entries in a given date range
* show log entries for a specific user ID (case-insensitive)
* show log entries for a specific subject:
  * key or key template uuid
  * key label
  * key template number
