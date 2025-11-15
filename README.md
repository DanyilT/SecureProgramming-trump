# Donald Trump Appreciation Site — Secure Programming Assignment
This repository is a deliberately vulnerable Flask web application used as a test subject for a Secure Programming assignment: identify, exploit, and fix web application vulnerabilities. The app is intentionally simple and includes a SQLite backend so students can practice finding real weaknesses (e.g. SQL Injection, XSS, Path Traversal, CSRF, IDOR) and then implement fixes. This README documents the repository structure, how to run the app, the important branches, and a vulnerability tracking table you can use to reference pull requests and authors.

---

## Project overview
- **App:** A small Flask application ("Donald Trump Appreciation Site") that demonstrates common web security vulnerabilities and their fixes.
- **Purpose:** Teaching and assessment — identify vulnerabilities, create working exploits to demonstrate impact, and commit fixes with code comments and a final report.
- **Language:** Python (Flask) + HTML/CSS; data stored in SQLite (`trump.db` / `trump.sql`).

## Repository contents (important files/dirs)
- [`app.py`](/app.py) — main Flask application
- [`trump.sql`](/trump.sql) / [`trump.db`](/trump.db) — initial database schema / sample data
- [`.env`](/.env) — environment variables for configuration (SECRET_KEY, etc.)
- [`templates/`](/templates) — Jinja2 HTML templates (index, comments, login, profile, etc.)
- [`static/`](/static) — CSS and other assets
- [`docs/`](/docs) — downloadable files used by the app
- [`requirements.txt`](/requirements.txt) — Python dependencies for the project
- [`LICENSE`](/LICENSE) — license file
- [`README.md`](/README.md) — this file
- [Branches](https://github.com/DanyilT/SecureProgramming-trump/branches) (see next section) hold feature/fix branches for specific vulnerabilities

### Branches (high level)
- [`main`](https://github.com/DanyilT/SecureProgramming-trump/tree/main) — The primary application branch. Contains the current production/testable app. Stable or development mainline. All merged fixes should be present here.
- [`init`](https://github.com/DanyilT/SecureProgramming-trump/tree/init) — Initialization branch. Initial version of the app (that we got), contains all vulnerabilities for testing.
- [`thirdpartyattackerwebapp`](https://github.com/DanyilT/SecureProgramming-trump/tree/thirdpartyattackerwebapp) — A small separate web app used to host attacker pages (CSRF exploit pages) for demonstration in a controlled environment cross-site interactions during tests. Run this on a separate port to host exploit HTML pages.
- [`fix/...`](https://github.com/DanyilT/SecureProgramming-trump/branches/all?query=fix) — Vulnerability-fix branches. Use branch naming like [`fix/sql-injection`](https://github.com/DanyilT/SecureProgramming-trump/tree/fix/sql-injection), [`fix/stored-xss`](https://github.com/DanyilT/SecureProgramming-trump/tree/fix/stored-xss), [`fix/path-traversal`](https://github.com/DanyilT/SecureProgramming-trump/tree/fix/path-traversal), [`fix/csrf`](https://github.com/DanyilT/SecureProgramming-trump/tree/fix/csrf), etc. Links to the fix branches are provided in the Vulnerability table below.

## How to use this repo for assignments
1. Identify vulnerabilities:
   - Inspect `app.py` and `templates/` to find insecure code patterns (SQL string concatenation, .safe rendering, file path handling, missing CSRF tokens, hard-coded secrets, etc.)
   - Confirm via live testing (exploit payloads on a development instance).
2. Exploit vulnerabilities:
   - Create reproducible, non-destructive exploit payloads and record screenshots showing the effect (before fix).
3. Fix vulnerabilities:
   - Implement minimal, well-documented fixes on feature branches (one vulnerability per branch).
   - Add comments in the code explaining the fix and why it prevents the exploit.
   - Open a pull request (PR) to merge each fix branch into `main`.
4. Validation:
   - Re-run the exploit and demonstrate it no longer works; include screenshots.
   - Provide a report listing the vulnerability, steps to exploit, code changes, and proof-of-fix.

### PR and issue workflow (recommended)
1. Create a branch for each vulnerability fix: `git checkout -b fix/<short-name>`.
2. Implement the fix and add comments describing the change.
3. Open a PR against `main` referencing the issue in the title/body: `Fix: <vulnerability>`.
4. When merging, update the Vulnerability table in this README with the PR URL and the GitHub username that fixed vulnerability.

---

## Vulnerability tracking table
| #  | Vulnerability                                      | OWASP / CWE                                                          | Pull Request (fix)                                                | Fixed by (GitHub user)                                    | Fix branch (link)                                                                                                        |
|----|----------------------------------------------------|----------------------------------------------------------------------|-------------------------------------------------------------------|-----------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------|
| 1  | SQL Injection (login)                              | OWASP A01:2021 — Injection (CWE-89)                                  | [#1](https://github.com/DanyilT/SecureProgramming-trump/pull/1)   | [DanyilT](https://github.com/DanyilT)                     | [fix/sql-injection](https://github.com/DanyilT/SecureProgramming-trump/tree/fix/sql-injection)                           |
| 2  | Path Traversal (download)                          | OWASP A05:2021 — Security Misconfiguration / Path traversal (CWE-22) | [#2](https://github.com/DanyilT/SecureProgramming-trump/pull/2)   | [DanyilT](https://github.com/DanyilT)                     | [fix/path-traversal](https://github.com/DanyilT/SecureProgramming-trump/tree/fix/path-traversal)                         |
| 3  | Open Redirect                                      | OWASP A05:2021 — Security Misconfiguration / Open Redirect (CWE-601) | [#3](https://github.com/DanyilT/SecureProgramming-trump/pull/3)   | [DanyilT](https://github.com/DanyilT)                     | [fix/open-redirect](https://github.com/DanyilT/SecureProgramming-trump/tree/fix/open-redirect)                           |
| 4  | Stored XSS (comments)                              | OWASP A03:2021 — Cross-Site Scripting (CWE-79)                       | [#5](https://github.com/DanyilT/SecureProgramming-trump/pull/5)   | [IlliaStefanovskyi](https://github.com/IlliaStefanovskyi) | [fix/stored-xss](https://github.com/DanyilT/SecureProgramming-trump/tree/fix/stored-xss)                                 |
| 5  | Broken Access Control (admin panel)                | OWASP A01:2021 — Broken Access Control (CWE-639)                     | [#6](https://github.com/DanyilT/SecureProgramming-trump/pull/6)   | [IlliaStefanovskyi](https://github.com/IlliaStefanovskyi) | [fix/broken-access-control](https://github.com/DanyilT/SecureProgramming-trump/tree/fix/broken-access-control)           |
| 6  | Reflected XSS (search)                             | OWASP A03:2021 — XSS (CWE-79)                                        | [#7](https://github.com/DanyilT/SecureProgramming-trump/pull/7)   | [artemsa223](https://github.com/artemsa223)               | [fix/reflected-xss](https://github.com/DanyilT/SecureProgramming-trump/tree/fix/reflected-xss)                           |
| 7  | Insecure Direct Object Reference – IDOR (profile)  | OWASP A01:2021 — Broken Access Control (CWE-639)                     | [#8](https://github.com/DanyilT/SecureProgramming-trump/pull/8)   | [DanyilT](https://github.com/DanyilT)                     | [fix/idor](https://github.com/DanyilT/SecureProgramming-trump/tree/fix/idor)                                             |
| 8  | Plaintext Password Storage                         | OWASP A02:2021 — Cryptographic Failures (CWE-312 / CWE-256)          | [#9](https://github.com/DanyilT/SecureProgramming-trump/pull/9)   | [IlliaStefanovskyi](https://github.com/IlliaStefanovskyi) | [fix/plaintext-password-storage](https://github.com/DanyilT/SecureProgramming-trump/tree/fix/plaintext-password-storage) |
| 9  | Hardcoded Secret Key / Weak secret                 | OWASP A02:2021 — Cryptographic Failures (CWE-798)                    | [#10](https://github.com/DanyilT/SecureProgramming-trump/pull/10) | [artemsa223](https://github.com/artemsa223)               | [fix/secret_key](https://github.com/DanyilT/SecureProgramming-trump/tree/fix/secret_key)                                 |
| 10 | Database Configuration Exposure                    | OWASP A05:2021 — Security Misconfiguration                           | [#11](https://github.com/DanyilT/SecureProgramming-trump/pull/11) | [artemsa223](https://github.com/artemsa223)               | [fix/database-config](https://github.com/DanyilT/SecureProgramming-trump/tree/fix/database-config)                       |
| 11 | Debug Mode Enabled in Production                   | OWASP A05:2021 — Security Misconfiguration (CWE-489)                 | [#12](https://github.com/DanyilT/SecureProgramming-trump/pull/12) | [artemsa223](https://github.com/artemsa223)               | [fix/degug-enabled](https://github.com/DanyilT/SecureProgramming-trump/tree/fix/degug-enabled)                           |
| 12 | Sensitive Data Exposure (full credit card display) | OWASP A02:2021 — Cryptographic Failures (CWE-200/CWE-359)            | [#13](https://github.com/DanyilT/SecureProgramming-trump/pull/13) | [DanyilT](https://github.com/DanyilT)                     | [fix/sensitive-data-exposure](https://github.com/DanyilT/SecureProgramming-trump/tree/fix/sensitive-data-exposure)       |
| 13 | Password Field Visible                             | OWASP A04:2021 — Insecure Design                                     | [#14](https://github.com/DanyilT/SecureProgramming-trump/pull/14) | [IlliaStefanovskyi](https://github.com/IlliaStefanovskyi) | [fix/password-field-visible](https://github.com/DanyilT/SecureProgramming-trump/tree/fix/password-field-visible)         |
| 14 | CSRF (missing tokens)                              | OWASP A08:2021 — CSRF (CWE-352)                                      | [#15](https://github.com/DanyilT/SecureProgramming-trump/pull/15) | [DanyilT](https://github.com/DanyilT)                     | [fix/csrf](https://github.com/DanyilT/SecureProgramming-trump/tree/fix/csrf)                                             |

---

## Quick start (run the app locally)

1. **Clone the repo**
    ```bash
    git clone https://github.com/DanyilT/SecureProgramming-trump.git
    cd SecureProgramming-trump
    ```

2. **Create and activate a virtual environment** (recommended)
    ```bash
    python -m venv venv
    # Linux / macOS
    source venv/bin/activate
    # Windows (PowerShell)
    venv\Scripts\Activate.ps1
    ```
    - Exit the virtual environment, later, with:
      ```bash
      deactivate
      ```

3. **Install dependencies**
    ```bash
    pip install -r requirements.txt
    ```

4. **Initialize and run the app**
   - The app contains an initialization routine that will create `trump.db` from `trump.sql` if it does not exist. Start the app:
    ```bash
    python app.py
    ```
   - The default runs on [`http://127.0.0.1:5000/`](http://127.0.0.1:5000/).
   - Stop the server with `Ctrl + C`.

5. (Optional) **Run the attacker web app**
   - If you want to demonstrate CSRF/XSS exploits with an external page, switch to the `thirdpartyattackerwebapp` branch and run that small web server to host exploit pages.
    ```bash
    git checkout thirdpartyattackerwebapp
    python -m http.server 8000
    ```
   - Access the attacker app at [`http://127.0.0.1:8000/`](http://127.0.0.1:8000/).
   - Stop the server with `Ctrl + C`.

---

## Credits
- **Repository owner:** [_DanyilT_](https://github.com/DanyilT)
- **Contributors:**
  - [_IlliaStefanovskyi_](https://github.com/IlliaStefanovskyi)
  - [_artemsa223_](https://github.com/artemsa223)
- **License:** This project is under [MIT License](./LICENSE)
