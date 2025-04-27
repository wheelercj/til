+++
title = 'Security benefits of SQL stored procedures'
date = 2025-03-12T17:04:00-07:00
lastmod = 2025-04-27T13:02:07-07:00
+++

Using [stored procedures](https://en.wikipedia.org/wiki/Stored_procedure) instead of putting SQL statements directly into a service's code can increase security. Here are some reasons why:

- Giving your service a SQL user that can only call stored procedures limits what attackers can do if they gain access to the SQL user credentials.
- If the SQL code is only accessed when it's actually needed, there will be fewer opportunities for attackers to get it. 
- By putting the SQL code in its own repo separate from the service, any attackers that get access to the database and the service's code but not the SQL repo may struggle to make sense of the data since they will have less context. Context is important for understanding data. Attackers can sometimes get context from the data itself, but that depends on how the data is organized, whether there's anything unnecessary there, whether things that should be hashed are hashed, etc. Even if reducing context only slows down attackers without stopping them, that still has value. Since ORMs and ODMs discourage the use of stored procedures, they tend to give attackers more context.

As a demonstration of the first point above, let's say your data can only be accessed by stored procedures that each take a Discord user ID as input. If an attacker gains access to your database with the credentials that can only call procedures, they can use any Discord user IDs they happen to know to immediately steal, delete, or replace the data of those users. The rest of the users they would have to brute-force. Since Discord IDs are mostly time-based, if the attacker has any hints on when a user created their account, they can use those to speed up the process. However, if the attacker wants to steal all of the data in the database, they would need to iterate through all possible Discord IDs for each table. Based on [Discord's snowflake documentation](https://discord.com/developers/docs/reference#snowflakes), there are more than 10^18 possible Discord IDs, and the number of possibilities increases by about 10^10 each year.

To put those numbers in perspective, consider the Python script below. It calculates the highest possible Discord ID and then approximates how long it would take to iterate through all possible Discord IDs when only printing an empty string for each one.

```python
import time
from tqdm import tqdm  # https://github.com/tqdm/tqdm

discord_epoch_ms: int = 1_420_070_400_000
now_ms: int = int(time.time() * 1000)

bin_max_id: str = bin(now_ms - discord_epoch_ms) + "11111" + "11111" + "111111111111"
max_id: int = int(bin_max_id, base=2)
print(f"{max_id = }")
print(f"{len(str(max_id)) = }")

for i in tqdm(range(max_id)):
    print(end="")
```

On my relatively fast computer, this code would take about 185 years to finish. This is a rough approximation for how long it would take to steal *each table*, not the entire database. Even if a table is almost empty, the code won't run any faster. The attacker could use a more efficient language than Python, but the database query will probably still be slower than the code above.

## Related

- [What's in a Discord ID?](/whats-in-a-discord-id)
- Stored procedures are more important for [multitenant](https://en.wikipedia.org/wiki/Multitenancy) ("shared") services, than single tenant ("isolated") ones.
