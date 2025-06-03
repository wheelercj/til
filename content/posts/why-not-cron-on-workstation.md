+++
title = 'Why not cron on workstation'
date = 2025-04-09T17:42:07-07:00
lastmod = 2025-06-03T01:42:17-07:00
+++

It's often helpful to use some scripts for organizing files and other regular workstation maintenance. For example, I sometimes make a local backup of my emails by running `timeout 30 thunderbird --headless`, which opens Thunderbird without opening the GUI and closes it 30 seconds later.

The last few weeks, I've been experimenting with various ways to automate when these scripts run, including `cron` and `anacron`. The main problem with using cron on a workstation rather than a server is that it skips jobs if their time to run is when the computer is off or suspended. Workstations are often suspended, so cron is unreliable for them.

Anacron is designed to fix that problem. When a job's time to run is missed, anacron runs the job as soon as the computer is running again.

However, I ran into problems with anacron too. The most important one was knowing if and when a job didn't run correctly. A job could run fine for months and then start failing. If a job has been failing for a while, that could mean losing a lot of important data. There are ways to fix this, the most common of which is to set up anacron to send you an email when something goes wrong. The process seems to involve creating a configuration file with your email account password or some kind of access token.

I decided not to go that route for several reasons including because some of what I regularly do cannot be fully automated anyways. Since I already have a script I manually run that tells me when to export what from where, it's easy enough to just add more functions to that script. Then if anything goes wrong, I'll immediately see an error message in my terminal.

The script is very simple right now. Here's part of it:

```python
def main():
    now: datetime = datetime.now()
    today: str = str(now.year) + "-" + str(now.month).zfill(2) + "-" + str(now.day).zfill(2)

    try:
        cwd: str = os.getcwd()
        print("Temporarily moving to the downloads folder")
        os.chdir("/home/chris/Downloads")

        check_restic_backup_config()
        open_thunderbird()
        back_up_calendars(today)
        back_up_fastmail_sieve_code(today)
        back_up_fastmail_mail_rules(today)
        back_up_ublock_filters()
        back_up_firefox_bookmarks(today)
        back_up_todoist_tasks()
    finally:
        print("Moving back to the previous folder")
        os.chdir(cwd)
```

This is reliable, effective, and only takes a few minutes for each run. The script started mostly as a [do-nothing script](https://news.ycombinator.com/item?id=42976698): a script that just printed instructions for me to follow and told me to press enter when done with each step. I've been gradually automating more of the steps starting with the parts that are easiest and most helpful to automate. Maybe next I'll add a way to easily skip steps when I want to.

I'll probably use cron and anacron extensively in the future, but for my main workstation, I'm more happy with a custom Python script for the time being.

## 2025/4/17 update

I created a decorator to add a confirmation prompt to each job. Now, when `open_thunderbird()` is called, the message `Run open_thunderbird? (y/n): ` appears so I can easily skip that step if I want to. The only change to the `open_thunderbird` function was adding `@job` above its signature. Here's the `job` definition:

```py
from collections.abc import Callable
from functools import wraps


def job(
    f1: Callable[..., None] | None = None, name: str | None = None
) -> Callable[..., None | Callable[..., None]]:
    """A decorator factory that adds a confirmation prompt

    This decorator can be used with or without arguments.

    When used with a name like `@job(name="My Task")`, it will prompt the user with that
    name before running the decorated function.

    When used without a name like `@job`, it will use the decorated function's name in
    the prompt.
    """
    def decorator(f2: Callable[..., None]) -> Callable[..., None]:
        name_s: str
        if name:
            name_s = name
        else:
            name_s = f2.__name__

        @wraps(f2)
        def inner(*args, **kwargs):
            while True:
                ok: str = input(f"Run {name_s}? (y/n): ")
                if ok.lower() in ("y", "yes"):
                    f2(*args, **kwargs)
                    return
                elif ok.lower() in ("n", "no"):
                    return

        return inner

    if f1 is None:
        return decorator
    else:
        return decorator(f1)
```

## 2025/5/31 update

Some of the jobs I defined require temporarily plugging in a flash drive or other external drive. Below is a context manager that makes external devices easier to automate. It asks the user to plug in the device, yields to code that uses the device, and then safely ejects the device. The context manager uses some commands that might only work in Linux.

```py
import subprocess
from contextlib import contextmanager
from pathlib import Path
from time import sleep
from typing import Generator


@contextmanager
def external_device(path: str | Path) -> Generator[Path]:
    location: Path = Path(path)

    _ = input(f"Plug in {location.name}, then press enter")
    sleep(2)
    if not location.is_dir():
        raise RuntimeError(f"{location.name} was not found")
    print(f"Found {location.name}")

    try:
        yield location
    finally:
        print(f"Getting {location.name} device name to eject it")
        lsblk_process = subprocess.Popen(
            ["lsblk"],
            stdout=subprocess.PIPE,
            text=True,
        )
        assert lsblk_process.stdout
        grep_process = subprocess.Popen(
            ["grep", "-i", location.name],
            stdin=lsblk_process.stdout,
            stdout=subprocess.PIPE,
            stderr=subprocess.PIPE,
            text=True,
        )
        lsblk_process.stdout.close()  # allow lsblk to finish if grep exits early
        output, errors = grep_process.communicate()
        if grep_process.returncode != 0:
            raise RuntimeError(f"grep: {errors}")

        device_name: str = output.split()[0].strip("└─")
        print(f"{device_name = }")

        print(f"Unmounting {location.name}")
        subprocess.run(
            ["udisksctl", "unmount", "--block-device", "/dev/" + device_name],
            check=True,
        )
        print(f"Powering off {location.name}")
        subprocess.run(
            ["udisksctl", "power-off", "--block-device", "/dev/" + device_name.rstrip("0123456789")],
            check=True,
        )
        print(f"{location.name} ejected")

        _ = input(f"Unplug {location.name}, then press enter")

```

You can use the context manager like this:

```py
import shutil
from pathlib import Path


file = Path("my_file.txt")

with external_device("/media/chris/SanDisk") as flash_drive:
    print(f"Moving file onto {flash_drive.name}")
    shutil.move(file, flash_drive / "my_folder")
```

`flash_drive` is a [pathlib.Path](https://docs.python.org/3/library/pathlib.html).

Find out what path to use for the device by plugging it in and running `ls /media/<your user name>`. The device should in the list.
