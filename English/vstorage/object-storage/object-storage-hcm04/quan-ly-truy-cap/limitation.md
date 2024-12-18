# Limitation

**When delegating IAM** permissions on **vStorage** , there are some limitations:

1. **Object Lock Mode Governance not supported: this mode is temporarily not supported on vStorage systems, so you can use Compliance** or **Legal Hold** modes instead to ensure data protection.
2. **Restrict permissions for IAM User:** Some features cannot customize permissions for IAM User and will default to **full permissions like Root User** , including:
   * **Bucket Versioning:** IAM User can freely enable/disable versioning without any permissions.
   * **CORS Bucket:** IAM User can set up or edit, delete CORS configuration without any restrictions.
   * **Object Lock:** IAM User can enable/disable locked object mode or change **retention day** without control.

These limitations may impact your ability to tightly control permissions when working with these features. We recommend that you consider this when granting IAM User permissions in use cases involving sensitive data.
