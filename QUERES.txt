--FIRST Q1
WITH RentalCounts AS (
    SELECT 
        f.title AS film_title, 
        c.name AS category_name, 
        COUNT(r.rental_id) AS rental_count
    FROM 
        Category c
    JOIN 
        Film_Category fc ON c.category_id = fc.category_id
    JOIN 
        Film f ON fc.film_id = f.film_id
    JOIN 
        Inventory i ON f.film_id = i.film_id
    JOIN 
        Rental r ON i.inventory_id = r.inventory_id
    WHERE 
        c.name IN ('Animation', 'Children', 'Classics', 'Comedy', 'Family', 'Music')
    GROUP BY 
        f.title, c.name
),
RankedRentals AS (
    SELECT 
        film_title, 
        category_name, 
        rental_count,
        ROW_NUMBER() OVER (PARTITION BY category_name ORDER BY rental_count DESC) AS rental_rank
    FROM 
        RentalCounts
)
SELECT 
    film_title, 
    category_name, 
    rental_count,
    rental_rank
FROM 
    RankedRentals
ORDER BY 
    category_name, rental_rank;
-------------------------------------------------------------------------------
Q2
WITH FilmDurations AS (
    SELECT 
        f.film_id,
        f.title AS film_title,
        c.name AS category_name,
        f.rental_duration
    FROM 
        film f
    JOIN 
        film_category fc ON f.film_id = fc.film_id
    JOIN 
        category c ON fc.category_id = c.category_id
    WHERE 
        c.name IN ('Animation', 'Children', 'Classics', 'Comedy', 'Family', 'Music')
),
Quartiles AS (
    SELECT 
        category_name, 
        rental_duration,
        NTILE(4) OVER (ORDER BY rental_duration) AS quartile
    FROM 
        FilmDurations
),
CategorizedQuartiles AS (
    SELECT 
        category_name, 
        CASE 
            WHEN quartile = 1 THEN '1'
            WHEN quartile = 2 THEN '2'
            WHEN quartile = 3 THEN '3'
            WHEN quartile = 4 THEN '4'
        END AS rental_quartile
    FROM 
        Quartiles
)
SELECT 
    category_name AS name, 
    rental_quartile AS standard_quartile,
    COUNT(*) AS count
FROM 
CategorizedQuartiles
GROUP BY 
category_name, rental_quartile
ORDER BY 
 category_name, rental_quartile;
---------------------------------------------
Q3
WITH Category_Rentals AS (
    SELECT 
        c.name AS category,
        COUNT(r.rental_id) AS total_rentals
    FROM 
        rental r
    JOIN 
        inventory i ON r.inventory_id = i.inventory_id
    JOIN 
        film f ON i.film_id = f.film_id
    JOIN 
        film_category fc ON f.film_id = fc.film_id
    JOIN 
        category c ON fc.category_id = c.category_id
    WHERE 
        EXTRACT(month FROM r.rental_date) = 2
    GROUP BY 
        c.name
)
SELECT 
    category,
    total_rentals
FROM 
    Category_Rentals
ORDER BY 
    total_rentals DESC
LIMIT 5;

---------------------------------------------
Q4
SELECT 
    EXTRACT(MONTH FROM r.rental_date) AS Rental_month,
    EXTRACT(YEAR FROM r.rental_date) AS Rental_year, 
    s.store_id AS Store_ID,
    COUNT(r.rental_id) AS Count_rentals
FROM 
    staff s
JOIN 
    rental r ON s.staff_id = r.staff_id
GROUP BY 
    Rental_month, Rental_year, Store_ID
ORDER BY 
    Count_rentals DESC;
------------------------------------------------
