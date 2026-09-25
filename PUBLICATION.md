# Check privacy before publishing

Check for secrets and personal data before every public push, release, issue
attachment, or documentation export. This applies to prose as well as code.
Something being public already doesn't make it safe to copy into a new release.

1. **Review what will leave the private workspace.** Read the exact files and
   diff, including generated files, images, archives, links, and file names. Use
   synthetic examples or reviewed summaries that don't identify people. Exclude
   private conversations, customer records, raw operational logs, account details,
   private-project identifiers, and personal source material.
2. **Scan content and history before upload.** Include every commit that will
   become public, along with commit/tag messages and author details. Check for
   environment files, credentials, authentication headers, credentials in URLs,
   home-directory paths, device identifiers, and contact details. Never put matched
   secrets in a public log or issue.
3. **Review each finding.** Keep public attribution deliberate. Don't allowlist
   a whole file or dismiss an unexplained match. Automated patterns miss some
   personal information and unknown secret formats.
4. **Check the actual release package.** Review the archive and file inventory,
   not just the source folder. Prefer a reviewed export without private Git
   history. Keep the experimental notice, counts, and limitations. Say which
   results readers can reproduce and which ones we are reporting from private records.
5. **Record and verify the result.** Save the reviewed commit or archive identity,
   checks, scope, and limitations in the release record. Do not publish unresolved
   findings. After upload, compare the public files with the reviewed version.

GitHub secret scanning and push protection add useful checks where enabled. They
don't cover all personal information or prove that a repo contains no secrets.
A scan that runs only after a public push cannot prevent that disclosure.

If a real credential is exposed, revoke or rotate it immediately and notify its
owner privately. Deleting it from the latest file isn't enough. Check history,
releases, and other copies, and coordinate cleanup without reposting the value.
