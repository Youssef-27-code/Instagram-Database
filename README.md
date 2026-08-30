#  Instagram Database Schema & SQL Analysis

A comprehensive relational database design and analytical SQL query suite modeled after Instagram's core functionality. This project demonstrates database normalization, primary/foreign key relationships, and complex query solving for business insights.

---

##  Database Schema & Architecture

The database models key interactions within a social media platform and consists of 6 main tables:

* **Users:** User profiles and registration dates.
* **Photos:** Image metadata linked to the posting user.
* **Comments:** User comments on specific photos.
* **Likes:** Track interactions (Many-to-Many relationship between Users and Photos).
* **Follows:** User follow/unfollow relationships (Self-referencing Many-to-Many).
* **Tags & Photo_Tags:** Hashtag implementation allowing many-to-many associations between photos and tags.

---

##  Entity Relationships (ER Summary)

* **One-to-Many (1:N):** 
  - `Users` ➔ `Photos` (A user can post multiple photos).
  - `Photos` ➔ `Comments` (A photo can have multiple comments).
* **Many-to-Many (M:N):** 
  - `Users` ➔ `Photos` (via `likes` join table).
  - `Users` ➔ `Users` (via `follows` join table for user connections).
  - `Photos` ➔ `Tags` (via `photo_tags` join table).

---

##  Business Logic & Key SQL Queries

Below are examples of analytical SQL queries implemented in the project:

### 1. Identifying Oldest Users (Reward Loyal Accounts)
```sql
SELECT username, created_at 
FROM users 
ORDER BY created_at ASC 
LIMIT 5;

SELECT tags.tag_name, COUNT(*) AS total_usage
FROM photo_tags
JOIN tags ON photo_tags.tag_id = tags.id
GROUP BY tags.id
ORDER BY total_usage DESC
LIMIT 5;

SELECT username, COUNT(*) AS total_likes 
FROM users 
JOIN likes ON users.id = likes.user_id 
GROUP BY likes.user_id 
HAVING total_likes = (SELECT COUNT(*) FROM photos);


 Tech Stack & Tools
Database Management System: MySQL
Tool: MySQL Workbench 
