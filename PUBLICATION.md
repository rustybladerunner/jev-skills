# Public-content review

Every public push, release, issue attachment and documentation export requires
a secrets and personal-data check before upload. This applies to documentation
as well as code. Prior publication does not make content safe to copy forward.

1. Review the exact files and diff, including generated outputs, images, archives,
   links and file names. Use synthetic examples or reviewed, non-identifying
   aggregates. Exclude private conversations, customer records, raw operational
   logs, account details, private-project identifiers and personal corpus.
2. Run secret scanning on the candidate content and all history that will become
   public, including commit/tag messages and author metadata. Inspect environment
   files, credentials, authentication headers, URLs containing credentials,
   machine/home paths, device identifiers and contact details. Never print secret
   matches into a public log or issue.
3. Review findings in context. Keep any approved public attribution deliberate;
   do not silently allowlist an entire file or suppress an unexplained finding.
   Automated patterns cannot reliably detect all personal data or unknown secrets.
4. Check the exact release archive and its inventory, not just the source folder.
   Prefer a reviewed export without private Git history. Retain the experimental
   notice, denominators, limitations and distinction between public reproduction
   and maintainer-reported results.
5. Record the reviewed commit/archive identity, scope, checks and any limitations
   in the release record. Stop publication when a finding remains unresolved.
   Check public read-back against the reviewed artifact after upload.

GitHub secret scanning and push protection, where enabled, supplement this
pre-publication review. They do not cover all personal information, cannot replace
content review, and do not prove that a repository contains no secrets. A check
that runs only after a public push is too late to prevent that disclosure.

If a real credential is exposed, revoke or rotate it immediately and notify its
owner privately. Removing it from the latest file is insufficient: inspect history,
releases and other copies, and coordinate remediation without reposting the value.
