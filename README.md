### Git Pre-Commit Hook check sensitive data in local repo
version: v0.8.1

**Description:**

For checking use 'Gitleaks' https://github.com/gitleaks/gitleaks 

The script will automatically check the operating system (Linux or macOS) and install GitLaks if it is not already installed.
If was finded secret data, commit will be rejected.

**Requirement:**

 - enable gitleaks in git config:
   `git config hooks.gitleaks.enable true`
   
 - move this script to your repo in `.git/hooks folder`, file name
   must be `pre-commit`

 - add permission to execute script:
   `chmod +x pre-commit`

**Usage:**

After change in your code and use `git commit`, pre-commit script will return result of check.:

Example if found secret:

```sh
Running Git Pre-Commit Hook...
gitleaks is enabled. Starting check...

    ○
    │╲
    │ ○
    ○ ░
    ░    gitleaks

Finding:     key: "REDACTED" # your tg token her...
Secret:      REDACTED
RuleID:      generic-api-key
Entropy:     4.137537
File:        k8s/secret-tele.k8s.yaml
Line:        7
Fingerprint: k8s/secret-tele.k8s.yaml:generic-api-key:7

5:49PM INF 1 commits scanned.
5:49PM INF scan completed in 10.8ms
5:49PM WRN leaks found: 1
gitleaks found secret. Commit aborted.

```
