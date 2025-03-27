+++
title = 'Object lock with Restic'
date = 2025-03-26T23:35:34-07:00
+++

[Restic](https://restic.net/) is an excellent tool for backing up files. It runs much faster than many other widely used backup programs (such as Duplicati and Borg), and it has almost all of the features one might want. [Its users include Filippo Valsorda](https://words.filippo.io/restic-cryptography/). 

However, like most backup software, Restic does not yet directly work well with object lock, which is a feature some cloud storage providers (including Backblaze B2) have to protect against ransomware. Object lock makes files temporarily immutable so that they cannot be deleted or changed for a duration of your choice. It is possible to use object lock directly with Restic, but supposedly it's much easier to use [Restic's rest-server](https://github.com/restic/rest-server/) in append-only mode and [rclone](https://rclone.org/commands/rclone_serve_restic/)'s `rclone serve restic` command.

The main reason why Restic does not directly work well with object lock is that Restic is not lock-free. Restic needs to be able to delete locks when it's done with them. According to [Comparison rustic and restic](https://rustic.cli.rs/docs/comparison-restic.html), Restic will become lock-free in version 0.19.

## Related

> Security considerations in append-only mode
> 
> TL;DR: With append-only repositories, one should specifically use the \--keep-within option of the forget command when removing snapshots.
> 
> To prevent a compromised backup client from deleting its backups (for example due to a ransomware infection), a repository service/backend can serve the repository in a so-called append-only mode. This means that the repository is served in such a way that it can only be written to and read from, while delete and overwrite operations are denied. Restic’s [rest-server](https://github.com/restic/rest-server/) features an append-only mode, but few other standard backends do. To support append-only with such backends, one can use [rclone](https://rclone.org/commands/rclone_serve_restic/) as a complement in between the backup client and the backend service.
> 
> — [Removing backup snapshots — restic 0.17.3 documentation](https://restic.readthedocs.io/en/stable/060_forget.html#:~:text=with%20tag%20example.-,Security%20considerations%20in%20append,and%20the%20backend%20service.,-To%20remove%20snapshots)

> An adversary who compromises a host system with append-only (read+write allowed, delete+overwrite denied) access to the backup repository could:
> 
> - Capture the password and decrypt backups from the past and in the future (see the “leaked key” example below for related information).
> - Render new backups untrustworthy *after* the host has been compromised (due to having complete control over new backups). An attacker cannot delete or manipulate old backups. As such, restoring old snapshots created *before* a host compromise remains possible.
> - Potentially manipulate the use of the forget command into deleting all legitimate snapshots, keeping only bogus snapshots added by the attacker. Ransomware might try this in order to leave only one option to get your data back: paying the ransom. For safe use of forget, please see the corresponding documentation on removing backup snapshots and append-only mode.
> 
> — [References — restic 0.17.3 documentation](https://restic.readthedocs.io/en/stable/100_references.html#:~:text=detect%0Athis%20attack.-,An%20adversary%20who%20compromises,and%20append%2Donly%20mode.,-An%20adversary%20who)
