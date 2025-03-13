+++
title = 'Security benefits of SQL stored procedures'
date = 2025-03-12T17:04:00-07:00
+++

Using [stored procedures](https://en.wikipedia.org/wiki/Stored_procedure) instead of putting SQL statements directly into a service's code can increase security. Here are some reasons why:

- Giving your service a SQL user that can only call stored procedures limits what attackers can do if they gain access to the SQL user credentials.
- If the SQL code is only accessed when it's actually needed, there will be fewer opportunities for attackers to get it. 
- By putting the SQL code in its own repo separate from the service, any attackers that get access to the database and the service's code but not the SQL repo may struggle to make sense of the data since they will have less context. Context is important for understanding data. Attackers can sometimes get context from the data itself, but that depends on how the data is organized, whether there's anything unnecessary there, whether things that should be hashed are hashed, etc. Even if reducing context only slows down attackers without stopping them, that still has value. Since ORMs and ODMs discourage the use of stored procedures, they tend to give attackers more context.

Stored procedures are more important for [multitenant](https://en.wikipedia.org/wiki/Multitenancy) ("shared") services, than single tenant ("isolated") ones.
