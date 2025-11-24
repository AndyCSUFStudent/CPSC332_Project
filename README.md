# Movie Theatre Database - Part B
**Andrew Rivera**  
**CPSC 332**

---

## Database Setup Instructions

### Requirements
- XAMPP installed and running
- MySQL service started
- phpMyAdmin accessible at http://localhost/phpmyadmin

---

## Loading the Database

### Step 1: Create Tables (DDL)
1. Open phpMyAdmin
2. Click "SQL" tab
3. Open `ddl.sql` file and paste content to query window
5. Click "Go"
6. Verify 8 tables created: THEATRE, AUDITORIUM, SEAT, MOVIE, CUSTOMER, SHOWTIME, TICKET, TICKET_AUDIT

### Step 2: Load Data (Seed)
1. Click "SQL" tab
2. Open `seed.sql` file and paste content to query window
4. Click "Go"

### Step 3: Create Views
1. Click "SQL" tab
2. Open `views.sql` file and paste content to query window
4. Click "Go"

### Step 4: Create Triggers
1. Click "SQL" tab
2. Open `triggers.sql` file and paste content to query window
4. Click "Go"

### Step 5: Create Stored Procedures
1. Click "SQL" tab
2. Open `procedures.sql` file and paste content to query window
4. Click "Go"

---

## Test Queries

### Test Views

**View 1: Top Movies by Tickets**
```sql
SELECT * FROM top_movies_by_tickets LIMIT 5;
```

**View 2: Sold Out Showtimes**
```sql
SELECT * FROM sold_out_showtimes;
```

**View 3: Theatre Utilization**
```sql
SELECT * FROM theatre_utilization;
```

### Test Triggers

**Test Trigger 1: Prevent Double Booking**
```sql
-- Trying to book an already booked seat
INSERT INTO TICKET (showtime_id, seat_id, customer_id, final_price, seat_type, discount_type, status)
VALUES (1, 1, 10, 12.00, 'Standard', 'None', 'Active');
```
Expected: Error message "This seat is already booked for this showtime"

**Test Trigger 2: Audit Refunds**
```sql
-- Refund a ticket
UPDATE TICKET SET status = 'Refunded' WHERE ticket_id = 1;

-- Check audit log
SELECT * FROM TICKET_AUDIT;
```
Expected: See refund logged in TICKET_AUDIT table

### Test Stored Procedure

**Procedure 1: Get Available Seats**
```sql
CALL get_available_seats(2);
```
Expected: Returns list of available seats for showtime 2

**Procedure 2: Get Customer Tickets**
```sql
CALL get_customer_tickets(1);
```
Expected: Returns all tickets purchased by customer 1

**Procedure 3: Sell Ticket**
```sql
-- Find available seat in auditorium_id 2
SELECT s.seat_id 
FROM SEAT s
WHERE s.auditorium_id = 2
  AND s.seat_id NOT IN (SELECT seat_id FROM TICKET WHERE showtime_id = 1)
LIMIT 1;

-- Use found seat_id (example: 50)
CALL sell_ticket(1, 50, 5, 'Student');

-- Verify
SELECT * FROM TICKET WHERE showtime_id = 1 AND seat_id = 50;
```
Expected: New ticket created successfully from found available seat

---

## Backup Instructions

### Run Backup Script
backup.sql script creates backup copies of all tables with date prefix

1. Click "SQL" tab in phpMyAdmin
2. Open `backup.sql` file and paste content to query box
4. Click "Go"

Backup filename format examples:
- `backup_20251123_THEATRE`
- `backup_20251123_AUDITORIUM`
- `backup_20251123_SEAT`

**Verify backup:**
```sql
SHOW TABLES LIKE 'backup_%';
SELECT COUNT(*) FROM backup_20251123_TICKET;
```

---

## Database Summary

- **3 Theatres** in Los Angeles/Beverly Hills area
- **11 Auditoriums** with different screen types (Standard, IMAX, Dolby)
- **~1800 Seats** across all auditoriums
- **15 Movies**
- **70 Customers** (50 registered + 20 guest checkout)
- **90 Showtimes** over 2 weeks
- **~450 Tickets** sold

---

## Files Included

1. `ddl.sql` - Creates database tables
2. `seed.sql` - Loads sample data
3. `views.sql` - Creates 3 views
4. `triggers.sql` - Creates 2 triggers
5. `procedures.sql` - Creates 1 stored procedure
6. `backup.sql` - Backup instructions
7. `README.md` - This current file

---

## Notes

- Showtimes use dynamic dates so view 3 always works

**Pricing:**
- Base: $8 (matinee) / $12 (evening)
- Premium seats: +$3
- Discounts: Student -$2, Senior -$3, Child -$4
- Formula: Base Price + Seat Type - Discount
