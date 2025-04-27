+++
title = "What's in a Discord ID?"
date = 2025-04-27T01:07:47-07:00
+++

Discord account IDs have four parts, the interesting one of which is when the account was created. Below is a way to retrieve a Discord account's creation time from the account's ID using Python. If you don't need to automate this, it's probably easier to open `https://discord.com/users/<Discord account ID>`.

```python
from datetime import datetime
from datetime import timezone


def split_snowflake(snowflake: int) -> tuple[datetime, int, int, int]:
    """Splits a Discord snowflake, such as a user ID, into its parts

    Returns
    -------
    dt: datetime
        The date and time the snowflake was created.
    worker_id: int
        The internal worker ID.
    process_id: int
        The internal process ID.
    increment: int
        The ID's increment. For each ID generated on a process, this number
        is incremented.

    References
    ----------
    - https://discord.com/developers/docs/reference#snowflakes
    """
    discord_epoch_ms: int = 1420070400000
    unix_timestamp_ms: int = (snowflake >> 22) + discord_epoch_ms
    unix_timestamp_s: float = unix_timestamp_ms / 1000
    dt: datetime = datetime.fromtimestamp(unix_timestamp_s, tz=timezone.utc)

    worker_id: int = (snowflake & 0x3E0000) >> 17
    process_id: int = (snowflake & 0x1F000) >> 12
    increment: int = snowflake & 0xFFF

    return dt, worker_id, process_id, increment


def test_split_snowflake():
    dt: datetime = datetime(
        year=2016,
        month=4,
        day=30,
        hour=11,
        minute=18,
        second=25,
        microsecond=796000,
        tzinfo=timezone.utc,
    )

    assert split_snowflake(175928847299117063) == (dt, 1, 0, 7)
```
