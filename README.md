# Digital Guest Book

A Laravel 12-based guestbook management system featuring admin authentication, a public guest submission form with CAPTCHA verification, entry approval/rejection workflows, and CSV export functionality.

## Requirements

Before running the application, make sure you have the following installed:

* PHP 8.2 or newer (the project currently uses PHP 8.4.14)
* Composer
* Node.js and npm
* SQLite, MySQL, or PostgreSQL

The database connection can be configured through the `.env` file.

## Installation

Clone the repository and install the required dependencies:

```bash
git clone <repo-url> laravel_bukutamu
cd laravel_bukutamu
cp .env.example .env
composer install
npm install
php artisan key:generate
php artisan migrate
npm run dev
php artisan serve
```

For a production environment, use `npm run build` instead of `npm run dev`.

## Environment Configuration

Set up your database connection in the `.env` file. For example:

```env
DB_CONNECTION=mysql
```

You can also configure the application to use SQLite or PostgreSQL.

### Admin Account

An administrator account can be created using the database seeder:

```bash
php artisan db:seed
```

Default credentials:

* **Email:** `admin@example.com`
* **Password:** `password`

Only administrators can access the authentication system. Public registration is disabled.

## Running the Application

Use the following commands depending on your environment:

```bash
php artisan serve
```

Starts the Laravel application server.

```bash
npm run dev
```

Runs the Vite development server.

```bash
npm run build
```

Creates the production-ready frontend assets.

## Features

### Public Features

* Landing page with real-time guest statistics.
* 7-day activity sparkline.
* Public guestbook submission form.
* CAPTCHA verification to prevent unwanted submissions.
* Submitted entries are initially placed in a pending state.

### Admin Features

* Admin-only authentication.
* Dashboard containing statistics and recent activity.
* Review and manage pending guest entries.
* Approve or reject submissions with optional notes.
* View approved and rejected entries.
* Delete guestbook entries when necessary.
* Export approved or rejected entries as CSV files.
* Sort guest entries by:

  * Creation date
  * Visit date
  * Guest name
* Support ascending and descending sorting.

## Admin Workflow

1. Access the login page at `/login` using the administrator credentials.
2. After logging in, the dashboard provides an overview of guestbook statistics and recent activity.
3. Open the **Visits** section to manage guest submissions.
4. Review pending entries and either approve or reject them.
5. Add notes when reviewing an entry if needed.
6. Delete entries when necessary.
7. Export approved or rejected entries as CSV files.
8. Use the sorting dropdown to change the order of the guest list.

## Public Workflow

### Landing Page

Visit:

```text
/
```

The landing page displays statistics based on the latest available data.

### Guestbook Form

Visit:

```text
/guest/create
```

Guests can submit their information through the public form. CAPTCHA verification is required, and all submissions are placed in the pending queue until they are reviewed by an administrator.

## Database Structure

The main database tables include:

* `users` — Stores administrator accounts and their assigned roles.
* `guest_entries` — Contains guest submissions, their current status (`pending`, `approved`, or `rejected`), visit dates, notes, reviewer information, and timestamps.
* `password_reset_tokens` — Stores password reset tokens.
* `sessions` — Handles user session data.

## Testing

The project includes tests covering administrator authentication and the guest submission workflow.

Run the available tests with:

```bash
php artisan test --filter=AdminLoginTest
php artisan test --filter=GuestEntryFlowTest
```

You can also run the complete test suite using:

```bash
php artisan test
```
