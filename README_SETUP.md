# House of Venus — Updated Project Setup

This update preserves the existing HTML/CSS/JavaScript + Express + MySQL project.

## What changed

- Replaced the old HV text mark in the home and services headers/footer with the supplied `JavaScript/images/logo.png` asset.
- Updated broken service image paths to files that actually exist in `JavaScript/images/` and standardized service image cropping.
- Added `bookService()` so each service button passes its service name into `Appointment.html?service=...`; the appointment page preselects matching services.
- Added cash-at-salon payment selection. Online payment is visibly unavailable until a real payment gateway is configured; the API rejects online-payment bookings and never marks bookings as paid.
- Added a SQL migration to store `payment_method` and `payment_status` while preserving existing appointments.
- Updated the slogan to “Your Beauty. Your Style. Our Passion.”
- Added a keyboard-accessible story-video modal. The actual salon video was not included in the supplied archive, so add it at `JavaScript/videos/house-of-venus-story.mp4` when available.
- Removed the archive's private `.env` file and hard-coded database credentials. Use `.env.example` to create your own local `.env`.
- Excluded `node_modules` from this ZIP. Install packages locally with `npm install`.

## Setup on Windows / VS Code

1. Extract the ZIP to a folder such as `C:\Users\YOUR_USER\Desktop\WebsiteWT`.
2. Open the `WebsiteWT` folder in VS Code.
3. Open a terminal and run:

   ```powershell
   cd backend
   Copy-Item .env.example .env
   notepad .env
   npm install
   ```

4. In `.env`, enter your local MySQL settings. Use your existing database name (the original backend used `websitewt`) and your own database password. Do not share `.env` or upload it publicly.
5. Open MySQL Workbench, select the correct existing database, and run `backend/migrations/001_add_appointment_payment_fields.sql` **once**. This adds two columns and does not delete existing appointments.
6. Start the backend in the terminal inside `backend`:

   ```powershell
   npm start
   ```

   It should listen on `http://127.0.0.1:5000`. Visit `http://127.0.0.1:5000/test-db` to check the database connection.
7. In VS Code, open `JavaScript/index.html` with Live Server. Keep the backend terminal running while testing booking.

## Test checklist

- Home and Services pages show the supplied logo.
- Service photographs load from the existing images folder.
- Clicking any listed service opens the appointment page with that service preselected.
- Cash at the salon is selected by default and displayed in the booking summary.
- The backend stores new cash bookings as `payment_method = 'cash'` and `payment_status = 'Unpaid'`.
- Online payment is unavailable until a real gateway is integrated.
- The story modal opens and closes with its close button or Escape. Playback requires the actual video file at the path above.

## Important testing note

JavaScript syntax checks and local image-path checks were run while preparing this ZIP. I could not connect to your local MySQL server or test the site in your own browser from this environment. Run the steps above and test login, booking, profile, and admin pages locally. Existing authentication routes still need a full security review before production deployment.
