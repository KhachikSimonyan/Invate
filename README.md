# InviteFlow Pro

InviteFlow Pro is a ready-to-run PHP web app for managing private invitations, RSVP approvals, outfit photo submission, approval/rejection comments, reminders, calendar export, private invitation links, in-app notifications, optional email/SMS/Telegram hooks, basic image moderation, and chat between inviter and guest.

## Features

- User registration and login
- Create invitations with:
  - place
  - date
  - time
  - description/request
  - dress code
  - outfit photo deadline (days before event)
- Guest can accept or decline invitation
- Inviter receives notifications on accept/decline
- Guest uploads outfit photo before the deadline
- Inviter can approve or reject the outfit
- Rejection comment is required when rejecting
- Guest re-uploads a new photo if rejected
- File upload limit: 5MB
- Private invitation link via secure token
- Calendar export (`.ics`)
- Reminder engine for:
  - upcoming event reminder
  - outfit upload reminder
- Notification center
- Optional email / SMS / Telegram notification hooks
- Basic image moderation:
  - actual-image validation
  - allowed MIME types only
  - max size enforcement
- Chat between inviter and guest
- JSON file storage auto-initialization (no database dependency)

## Requirements

- PHP 8.0+

## Run locally

From the project root:

```bash
php -S localhost:8000 -t public
```

Then open:

```bash
http://localhost:8000
```

## Default workflow

1. Register two users.
2. Login as inviter.
3. Create an invitation.
4. Login as guest.
5. Accept or decline it.
6. If accepted, upload an outfit photo before the deadline.
7. Login as inviter and approve/reject the photo.
8. Chat and track notifications.

## Running reminders

Open this URL while logged in:

```bash
http://localhost:8000/?action=run_reminders
```

This creates reminder notifications and also attempts external delivery if configured.

## External notification setup

Edit `app/config.php`.

Supported hooks:
- Email (via `mail()`)
- Telegram Bot API
- Twilio SMS

These require your real credentials and server configuration.
Without credentials, the system still works with in-app notifications.

## Notes

- Calendar integration is implemented as `.ics` download.
- Image moderation is implemented as server-side image validation plus the inviter approval workflow.
- AI-based image moderation can be added later through a third-party API.
- Storage is file-based in `storage/data.json`, so this package works even when SQLite is unavailable.

## Project structure

- `public/` — entry point, assets, uploaded files
- `app/` — configuration and helper functions
- `storage/` — JSON storage
