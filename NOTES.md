# Notes

While going through the codebase to complete the task I noticed and fixed a few things:

- **JWT tokens had no expiry** (`controllers/auth.js`) — a stolen token would stay valid indefinitely. Added a 7-day expiry.
- **`||` operator bug** (`routes/lead.js`) — `('manager' || 'super_admin')` evaluates to `'manager'` in JS, so `super_admin` users were silently blocked from leads they should have access to. Fixed with `.includes()`.
- **Password saved in plaintext** (`controllers/notification.js`) — registration requests stored the user's raw password in the notifications collection. Removed it from the saved data.
