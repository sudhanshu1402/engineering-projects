# Hospital Management System

A desktop app for hospital front-office work: register patients, allocate rooms, manage staff, book appointments, and generate bills. Tkinter GUI on top of a SQLite database. Built as a DBMS course project.

## What it does

The receptionist or admin logs in, then works from a main menu with five modules:

- **Patient registration** — add, update, search, and delete patients (name, sex, DOB, blood group, address, consulting doctor, email, two contact numbers). Patient and contact details are stored in two linked tables.
- **Room allocation** — assign a patient to a room (single / twin / triple sharing), set the rate and admit date, and look up who is in which room. Refuses a room number that is already occupied.
- **Employee registration** — add and delete staff records (ID, name, sex, age, designation, salary, experience, phone, email).
- **Appointments** — book a patient with a doctor at a given date and time, delete an appointment, or list all appointments on a chosen date.
- **Billing** — record a patient's treatment and medicine charges, set the discharge date, and compute the total bill (treatment cost + medicine cost × quantity + room rate × days stayed).

Each record is validated against duplicates before insert (duplicate patient ID, room number, employee ID, or appointment number is rejected).

## Stack

- **Python 3** (standard library only)
- **Tkinter** for the GUI
- **SQLite** via the built-in `sqlite3` module

No third-party packages, so there is no `requirements.txt` — everything ships with a normal Python install.

## Database schema

Seven tables, keyed on `PATIENT_ID` (and `EMP_ID` for staff):

| Table | Holds | Key |
|-------|-------|-----|
| `PATIENT` | core patient details | `PATIENT_ID` |
| `CONTACT_NO` | patient phone numbers | `PATIENT_ID` → PATIENT |
| `employee` | staff records | `EMP_ID` |
| `ROOM` | room allocation + admit/discharge dates | `ROOM_NO` |
| `TREATMENT` | treatment name, code, cost | `PATIENT_ID` → PATIENT |
| `MEDICINE` | medicine name, quantity, cost | `PATIENT_ID` → PATIENT |
| `APPOINTMENT` | patient–doctor bookings | `AP_NO` |

The `CREATE TABLE` statements all live in `database.py` (the ones for the older tables are commented out; the `APPOINTMENT` block is the one left active). The billing total is a single SQL query joining `ROOM`, `TREATMENT`, and `MEDICINE`.

## Setup and run

The app connects to a SQLite file named `HospitalDB.db` in the working directory. The repo already includes a database file named `hospital-db.db` — note the name differs, so on first run SQLite creates a fresh empty `HospitalDB.db` instead of using the committed one. To use the app you first need the tables.

1. Create the database and tables. Open `database.py`, uncomment the `CREATE TABLE` blocks for the tables you need (only `APPOINTMENT` is active by default), then run it once:

   ```bash
   python database.py
   ```

   > Heads up: the `APPOINTMENT` block starts with `DROP TABLE IF EXISTS APPOINTMENT`, so re-running `database.py` wipes existing appointments. Comment that line out once your tables exist.

2. Start the app from the login screen:

   ```bash
   python login.py
   ```

## Logging in

Credentials are hard-coded in `login.py`:

| Username | Password |
|----------|----------|
| `admin`  | `1234`   |
| `root`   | `4321`   |

## Usage example

Register a patient, give them a room, then bill them:

1. Log in as `admin` / `1234`.
2. **Patient registration** → enter Patient ID `101`, name, sex, DOB as `1998-05-20`, blood group, contacts, doctor, address → **Submit**.
3. **Room allocation** → Patient ID `101`, room type `SINGLE`, room number `S12`, rate `4500`, date admitted `2026-07-10` → **Submit**.
4. **Billing** → Patient ID `101`, enter treatment + cost and medicine + quantity + price → **Update Data**. Set the discharge date (e.g. `2026-07-14`) → **Update Discharge Date**. Then **Generate Bill** to see the total: treatment cost + (medicine cost × qty) + (days stayed × room rate).

Dates are typed as text in `YYYY-MM-DD` and times as `HH:MM:SS`.

## How the code is laid out

| File | Role |
|------|------|
| `login.py` | Entry point — login window; opens the menu on valid credentials |
| `menu.py` | Main menu with buttons that open each module in a new window |
| `patient_form.py` | Patient insert / update / search / delete |
| `room_form.py` | Room allocation and room lookup |
| `employee_form.py` | Employee insert / delete |
| `appointment_form.py` | Appointment booking / delete / search-by-date |
| `billing_form.py` | Discharge date, treatment/medicine entry, bill total |
| `database.py` | Table creation script (run once) |

Each module is a class that builds its own Tkinter window and holds its own `sqlite3` connection. All inserts use parameterized queries (`?` placeholders), and searches use SQL `NATURAL JOIN` to pull related patient/room/contact rows together.

## Scope and known rough edges

This is a learning project, and it shows in a few places worth calling out honestly:

- Login credentials are hard-coded and stored in plaintext — fine for a demo, not for anything real.
- Phone and contact numbers use `IntVar`, so leading zeros and very long numbers won't survive.
- The committed `hospital-db.db` doesn't match the `HospitalDB.db` name the code opens, so you have to build the schema yourself (see Setup).
- The room "Update" flow has inverted logic — it reports "patient is not allocated a room" when the record actually exists — so updating a room record doesn't work as intended.

If you're reading this to learn: the useful parts are the Tkinter form structure, the multi-table SQLite schema with foreign keys, and the joins used for search and billing.
