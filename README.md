# Makerspace

A PHP/MySQL application with login, logout and a member dashboard. The current implementation is distributed in [`makerspace_final.zip`](makerspace_final.zip).

## Repository contents

| File | Purpose |
| --- | --- |
| `makerspace_final.zip` | Application source, inside the `makerspace_final/` directory. |
| `20251112_Projektauftrag_Open_Makerspace.pdf` | Project assignment. |
| `AGENTS.md` | Instructions and confirmed context for future development. |

## Local setup

Prerequisites: PHP with PDO and the PDO MySQL driver, a MySQL database, and an archive extraction tool. The supported PHP version has not been documented or verified yet.

1. Extract `makerspace_final.zip`, keeping its directory structure. On macOS/Linux:

   ```bash
   unzip makerspace_final.zip
   ```

2. Configure the database connection in the extracted `makerspace_final/db.php` for your local database. Keep real credentials out of Git.

3. Provide a database with the schema expected by the application. **The repository currently contains no SQL schema or database migration.** Do not assume extracting the ZIP creates tables or a test account.

4. Serve the extracted application locally:

   ```bash
   php -S 127.0.0.1:8000 -t makerspace_final
   ```

5. Open [the login page](http://127.0.0.1:8000/login.php). A matching user must already exist in the database; `login.php` checks its password using `password_verify`.

PHP's built-in server is for local development. These instructions describe the existing source layout; a complete login test still requires the missing schema and a local test user.

## Application entry points

- `login.php`: looks up a user by username and verifies the stored password hash.
- `dashboard.php`: requires a logged-in session, loads members and displays `dashboard_view.php`.
- `logout.php`: destroys the session and returns to the login page.
- `db.php`: creates the PDO database connection.
- `login_view.php`, `dashboard_view.php`, `dashboard_admin_view.php` and `message.php`: HTML views and shared feedback display. The current dashboard controller includes `dashboard_view.php`; an admin view file exists, but automatic role-based routing is not implemented there.

The dashboard query references the `users` columns `id`, `username`, `klasse`, `telnum`, `password`, `role`, `access` and `created_at`. This list documents source expectations; column types, constraints, account provisioning and the authoritative schema remain **UNKNOWN**.

## Verification status

Documentation was checked against all eight PHP files and the actual ZIP paths. The archive is unchanged. PHP/MySQL runtime behavior and the project assignment have not been validated as part of this documentation update.
