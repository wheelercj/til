+++
title = 'Schema migrations'
date = 2025-04-25T22:32:12-07:00
+++

[Schema migration](https://en.wikipedia.org/wiki/Schema_migration) is sometimes referred to as "database migration", but "database migration" also has other possible meanings.

There are many ways to handle schema migrations. Which one is best depends on your goals.

- You could handle it all manually and not keep a record of the schema changes, but this is usually not a good idea.
- Many projects use ORMs like [SQLAlchemy](https://en.wikipedia.org/wiki/SQLAlchemy) or [Prisma](https://www.prisma.io/orm) specifically because they have tools that automate parts of schema migrations.
- If you will use SQL directly rather than an ORM, there are still many helpful tools with different strengths and weaknesses including:
	- [pressly/goose](https://github.com/pressly/goose)
	- [Flyway](https://documentation.red-gate.com/flyway/getting-started-with-flyway)
	- [liquibase/liquibase](https://github.com/liquibase/liquibase)
	- [ariga/atlas](https://github.com/ariga/atlas)
	- [Sqitch](https://sqitch.org/)
	- [golang-migrate/migrate](https://github.com/golang-migrate/migrate)
	- [pgroll](https://github.com/xataio/pgroll) (Postgres only)
	- [jackc/tern](https://github.com/jackc/tern) (Postgres only)
	- [purcell/postgresql-migrations](https://github.com/purcell/postgresql-migrations) (Postgres only)
	- [rubenv/sql-migrate](https://github.com/rubenv/sql-migrate) (Go only)
	- [Yoyo](https://ollycope.com/software/yoyo/latest/) (Python only)
	- [ThomWright/postgres-migrations](https://github.com/thomwright/postgres-migrations) (Node and Postgres only)
	- Here are more: [mgramin/awesome-db-tools](https://github.com/mgramin/awesome-db-tools)
- Many projects only need basic schema migration features and choose to implement their own commands, such as in the [RoboDanny](https://github.com/Rapptz/RoboDanny/blob/39af9d71ffd5f099094a05352c18b987a1dc5d04/launcher.py#L254) Discord bot.

Here's an article about how to manually migrate without any downtime: [SQL migrations in PostgreSQL, part 1 \| by Nikolai Averin \| Miro Engineering \| Medium](https://medium.com/miro-engineering/sql-migrations-in-postgresql-part-1-bc38ec1cbe75).
