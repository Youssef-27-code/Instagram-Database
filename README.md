# Instagram Database Clone — SQL Project

A relational database inspired by Instagram, built with MySQL. The goal was to practice database design (relationships, normalization) and writing SQL queries to answer real analytical questions.

## Database Structure

The database has 6 tables:

- **users** — user profiles and registration dates
- **photos** — photos, linked to the user who posted them
- **comments** — comments left by users on photos
- **likes** — join table tracking which users liked which photos
- **follows** — join table tracking which users follow which other users
- **tags** and **photo_tags** — hashtags, linked to photos through a join table

## Relationships

- **One-to-Many**
  - a user can post many photos
  - a photo can have many comments
- **Many-to-Many**
  - users and photos, through `likes`
  - users and users, through `follows` (a user can follow many users, and be followed by many users)
  - photos and tags, through `photo_tags`

## Example queries

**1. Find the oldest user accounts**
```sql
SELECT username, created_at
FROM users
ORDER BY created_at ASC
LIMIT 5;
```

**2. Find the most used tags**
```sql
SELECT tags.tag_name, COUNT(*) AS total_usage
FROM photo_tags
JOIN tags ON photo_tags.tag_id = tags.id
GROUP BY tags.id
ORDER BY total_usage DESC
LIMIT 5;
```

**3. Find users who liked every single photo on the platform**
```sql
SELECT username, COUNT(*) AS total_likes
FROM users
JOIN likes ON users.id = likes.user_id
GROUP BY likes.user_id
HAVING total_likes = (SELECT COUNT(*) FROM photos);
```

## Tools

MySQL

## Files

- [`schema_and_queries.sql`](./schema_and_queries.sql) — table creation, sample data, and all queries
