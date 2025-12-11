# Rivera Cinemas - Movie Theatre System
 
**Created by:** Andrew Rivera  
**Course:** CPSC332 - File Structures and Databases

A movie theatre ticket booking system built with PHP and MySQL.

---

## Prerequisites

- PHP 7.4 or higher
- MySQL 5.7 or higher
- Web server (Apache/Nginx) or PHP built-in server
- Web browser

---

## Installation & Setup

### 1. Extract Project Files

Extract the project ZIP file. Inside you should see:
- `public/` folder with PHP files
- `includes/` folder with configuration files
- `assets/` folder with CSS
- `sql/` folder with database files

### 2. Database Setup

**Run each SQL file in this order:**

1. **Create Tables** - Copy and paste `sql/ddl.sql` into MySQL and execute
2. **Insert Sample Data** - Copy and paste `sql/seed.sql` into MySQL and execute
3. **Create Views** - Copy and paste `sql/views.sql` into MySQL and execute
4. **Create Stored Procedures** - Copy and paste `sql/procedures.sql` into MySQL and execute
5. **Create Triggers** - Copy and paste `sql/triggers.sql` into MySQL and execute

**Important:** Run the files in this exact order. Each file depends on the previous ones.

**Verification:** After running all files, check that the database is ready:

```sql
USE movie_theatre;
SHOW TABLES;  -- Should show 8 tables
SELECT COUNT(*) FROM MOVIE;  -- Should return 15 movies
SELECT COUNT(*) FROM CUSTOMER;  -- Should return 70 customers
SELECT COUNT(*) FROM TICKET;  -- Should return 450+ tickets
```

### 3. Configure Database Connection

Edit `includes/config.php` with your MySQL credentials:

```php
define('DB_HOST', 'localhost');
define('DB_NAME', 'movie_theatre');
define('DB_USER', 'root');
define('DB_PASS', 'your_password');
```

### 4. Starting the Application

**Using XAMPP:**

1. Copy project folder to `htdocs` (XAMPP)
2. Configure virtual host to point to the `public` folder
3. Start Apache server
4. Visit: `http://localhost/rivera-cinemas/public`

---

## Sample Credentials & Demo Data

### Demo Customers with Pre-Loaded Tickets

**The database includes 70 existing customers with 450+ tickets already purchased.** You can test the "My Tickets" feature with these accounts:

- **Email:** `john.smith1@email.com` OR **Order Code:** `A7B3C9F1`
- **Email:** `emma.johnson2@email.com` OR **Order Code:** `D4E6F8A2`
- **Email:** `michael.williams3@email.com` OR **Order Code:** `E9C2B5F3`

### Sample Movies Available

The database contains 15 movies:

1. **Avengers: Endgame**
2. **Avatar: The Way of Water**
3. **Spider-Man: No Way Home**
4. **Top Gun: Maverick**
5. **Barbie**
6. **Oppenheimer**
7. **Inside Out 2**
8. **Dune: Part Two**
9. **Inception**
10. **The Batman**
11. **Guardians of the Galaxy**
12. **Black Panther**
13. **Interstellar**
14. **Deadpool & Wolverine**
15. **The Super Mario Bros Movie** 

### Theatres

- **Cineplex Downtown** - Los Angeles, CA (4 auditoriums)
- **Starlight Cinema** - Los Angeles, CA (4 auditoriums)
- **Regal West** - Beverly Hills, CA (3 auditoriums)

### Showtimes

All showtimes use dynamic dates (CURDATE() + intervals), so they're always current with 90 total showtimes across 7 days

---

## Test Click Path

### Test with Pre-Loaded Demo Data

1. Go to `http://localhost/rivera-cinemas/public`
2. Click navbar **"My Tickets"**
3. Enter email: `john.smith1@email.com` OR Order Code: `A7B3C9F1`
4. Click **"Search Tickets"**
5. You should see existing tickets for John Smith
6. Try the **"Refund"** button on any Active ticket
7. Go to **"Reports"** to see analytics

### Complete Purchase Flow

**Full walkthrough of creating a new ticket purchase:**

**1. Browse Movies**
- Go to `http://localhost/rivera-cinemas/public`
- Click **"View All Movies"** or navbar **"Movies"**
- Filter by rating: Select **"PG-13"**
- Click on **"Dune: Part Two"** to view details

**2. Find Showtimes**
- From movie detail page, click **"Find Showtimes"**
- Or navbar **"Showtimes"**
- Select Theatre: **"Cineplex Downtown"**
- Select Date: **Today's date**
- Click **"Find Showtimes"**
- Click **"Select Seats"** for any showing

**3. Select Seats**
- Click on available seats
- Click **"Continue to Checkout"**

**4. Complete Purchase**
- Fill in customer information
  - Phone number optional
- Select Discount
- Click **"Complete Purchase"**

**5. View Confirmation**
- Note your **Order Code**
- Review ticket details
- Price reflects discounts and premium seats

**6. Lookup Tickets**
- Navbar > **"My Tickets"**
- Enter email: `john.smith1@email.com` OR Order Code: `A7B3C9F1`
- Click **"Search Tickets"**
- View existing tickets from the pre-loaded demo data

**7. Refund a Ticket**
- From My Tickets page
- Click **"Refund"** on any Active ticket
- Confirm the refund
- Status changes to "Refunded"

**8. View Reports**
- Navbar > **"Reports"**
