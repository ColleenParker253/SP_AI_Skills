---
name: inactive-account-audit
description: |-
  Audits SharePoint site lists for inactive accounts assigned in custom Person/Group fields and prepares an email report.

  Use when the user says:
    - "audit inactive accounts in this site"
    - "run the Forte Design Projects inactive account report"
    - "check lists for stale Person field users"
    - "find inactive users assigned in SharePoint Person columns"
---
## When to use
Use this skill to audit a SharePoint site for inactive or stale user accounts assigned in business Person/Group columns across lists.

## Inputs
- SharePoint site URL to audit.
- Excluded list names, if any.
- Recipient email address and subject for the report.
- Rules for excluding reviewed or closed items.

Default for My Project Site Name:
- Site: `https://microsoft.sharepoint.com/<sites/teams>/<sitename>`
- Exclude list: `<ListName>`
- Exclude system Person fields: Created By, Modified By, Author, Editor, Checked Out By, Shared With
- If a list has internal column `Reviewed`, skip items where `Reviewed` is Yes/true/1
- If every item in a list is Reviewed=Yes, exclude that list and note it
- Email report to `<email@microsoft.com>`
- Subject: `<SiteName> — Inactive Account Report`

## Steps
1. Discover all non-hidden SharePoint lists on the site.
2. Skip any excluded list completely; don't include it in counts or tables.
3. For each remaining list, read schema and identify custom Person/Group columns only.
4. Ignore system author/audit/sharing Person fields.
5. Read items for lists with business Person columns.
6. If internal column `Reviewed` exists, exclude reviewed items from all counts and assignments.
7. Group distinct people by list, Person column, display name/account, and count of non-reviewed items.
8. Resolve each distinct person against the directory.
9. Treat a person as inactive if the lookup fails, or if available directory data shows blocked/disabled sign-in.
10. If a stale duplicate maps to an active alias, call out the active account.
11. Build the email report table with columns: List Name, Person Name, Email/Account, Person Column, Number of Items.
12. Include notes for unreadable lists and lists excluded because all items were Reviewed=Yes.
13. Send the report email.

If a tool fails or returns incomplete data, say so plainly in the report; don't invent missing account status.

## Output format
Return a concise summary in chat:
- Whether the email was sent
- Total inactive account assignments
- Total affected non-reviewed items
- Lists intentionally excluded
- Lists that couldn't be read

The email body must include:
- Summary line with total inactive accounts and total affected items
- Report table, or an explicit statement that no inactive accounts were found
- Notes for excluded and unreadable lists
