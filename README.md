<h1 align="center">🎬 SQL Project – DVD Rental Analysis</h1>

<p align="center">
  A data analysis project using SQL to explore trends and insights in a film rental database.
</p>

---

## 📘 Project Overview

This project focuses on analyzing a film rental database using **SQL queries**.  
We perform data exploration and extraction from a real-world DVD rental dataset to answer business-relevant questions and identify patterns in customer behavior, rental frequency, and film performance.

---

## 📂 Project Structure

| File                              | Description                                                        |
|-----------------------------------|--------------------------------------------------------------------|
| `sql-project-submission-template-2.pdf` | Full documentation with explanations and query results         |
| `QUERES.txt`                      | Raw SQL queries used in the analysis                              |
| `queries.sql`                     | SQL script containing the core analysis queries                   |
| `restore.sql`                     | SQL script to restore the database schema and data                |
| `dvd-rental-erd-2.pdf`            | Entity Relationship Diagram (ERD) of the DVD rental database      |
| `dvdrental.zip`                   | Compressed dataset with all necessary database files              |

---

## 📊 Key Queries and Their Purpose

- 🎞️ **Most Rented Family Movies**  
  Retrieves top-rented movies from family-friendly genres like *Animation*, *Children*, *Comedy*, *Family*, and *Music*.

- 📈 **Rental Duration Quartiles**  
  Groups family-friendly films into quartiles based on how long they were rented on average.

- 📅 **Top 5 Categories for February**  
  Identifies the most popular film categories rented during the month of February.

- 👨‍💼 **Rental Orders by Staff**  
  Shows how many rental transactions each staff member processed over time.

---

## 🛠️ How to Run the Project

1. Unzip `dvdrental.zip` and restore the database using `restore.sql` in your SQL environment (e.g., PostgreSQL).
2. Run the queries from `queries.sql` or `QUERES.txt` inside your SQL tool.
3. Review the output to gain insights into rental patterns and performance.

💡 *Recommended Environment:* PostgreSQL (since the dataset is structured for it)

---


> 📌 This project demonstrates how structured query language (SQL) can be used to derive insights and support business decisions in media rental services.


This project is licensed under the MIT License - see the LICENSE file for details.

