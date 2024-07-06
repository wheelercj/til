+++
title = 'Learning SQL'
date = 2021-10-15T16:17:29-08:00
lastmod = 2024-07-06T12:34:41-07:00
+++

SQL (Structured Query Language) is a commonly used and reliable way for programs to store and retrieve data. In many cases, it's much better in many ways than just using files directly.

There's a lot that can be learned about SQL. Here are some resources to get you started.

1. Learn SQL with [SQLBolt](https://sqlbolt.com/) and/or [The SQL Murder Mystery](https://mystery.knightlab.com/).
2. Choose a database technology and tools.
    * [_Databases_ by Full Stack Python](https://www.fullstackpython.com/databases.html) is a guide (not entirely for Python) with various resources about databases.
    * [Supabase](https://supabase.com/) and [Turso](https://turso.tech/pricing) (and some others) have decent free tiers and make setting up databases relatively easy.
    * [Beekeeper Studio](https://www.beekeeperstudio.io/) is a an open source SQL editor and database manager with a free tier. I use it and it seems to work well.
    * Tools like [sqlc](https://sqlc.dev/) generate type-safe database interface code for you without unnecessary abstraction. Here are other SQL interface generators (or related tools) I haven't really looked into: [Jet](https://github.com/go-jet/jet), [SQLBoiler](https://github.com/volatiletech/sqlboiler), [SQLx](https://github.com/launchbadge/sqlx), [Goa](https://goa.design/), [Go kit](https://gokit.io/), [gqlgen](https://gqlgen.com/), [Bun](https://bun.uptrace.dev/).
    * If you are making an asynchronous application, you will probably want to choose an asynchronous library for interacting with your database. For example, [asyncpg](https://magicstack.github.io/asyncpg/current/) is a good choice for PostgreSQL in asynchronous Python.
    * If each user of software you're making needs their own local database, consider using [SQLite](https://www.youtube.com/watch?v=jH39c5-y6kg) so that the user doesn't have to set up the database themselves. [Here's a 2022/4/25 HN discussion](https://news.ycombinator.com/item?id=31152490) on the pros and cons SQLite versus other database technologies.
    * There are some SQL services available in the [GitHub student developer pack](https://education.github.com/pack).

## intermediate topics

* [SQL Roadmap - roadmap.sh](https://roadmap.sh/sql)
* [Sqlines](https://www.sqlines.com/home) is a collection of "tools to help you transfer data, convert database schema (DDL), views, stored procedures, packages, user-defined functions (UDFs), triggers, SQL queries, SQL scripts between different database platforms."
* [_Learn Database Normalization - 1NF, 2NF, 3NF, 4NF, 5NF_ by Decomplexify](https://www.youtube.com/watch?v=GFQaEYEc8_8)
* [_Use the Index, Luke!_ by Markus Winand](https://use-the-index-luke.com/)
* [_Simplify: move code into database functions_ by Derek Sivers](https://sive.rs/pg)
* [_Database migrations_ by Vadim Kravcenko](https://vadimkravcenko.com/shorts/database-migrations/)
* [_Things to know about databases_ by Mahdi Yusuf](https://news.ycombinator.com/item?id=31895623)
* [2023/10/1 HN discussion on database migrations](https://news.ycombinator.com/item?id=37724549)
