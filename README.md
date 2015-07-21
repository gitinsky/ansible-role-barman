# Vars

postgres_host

# Links
http://www.postgresql.org/message-id/CADKbJJXP-eKGf=ntcHRJgTqiN-XhogmD2RJsRdCt4TcW7Mp8=w@mail.gmail.com
http://docs.pgbarman.org/#getting_started

# Remove failed backups

If you have failed backups in your backup list:

```bash
$ barman list-backup all
main 20150721T040401 - Tue Jul 21 04:14:43 2015 - Size: 4.3 GiB - WAL Size: 344.8 MiB
main 20150720T040401 - Mon Jul 20 04:05:23 2015 - Size: 4.3 GiB - WAL Size: 1.6 GiB
main 20150719T040401 - Sun Jul 19 04:04:48 2015 - Size: 4.3 GiB - WAL Size: 139.5 MiB
main 20150718T040401 - Sat Jul 18 04:05:02 2015 - Size: 4.3 GiB - WAL Size: 167.7 MiB
main 20150717T055336 - FAILED
main 20150715T052117 - FAILED
main 20150715T051659 - FAILED
main 20150715T050251 - FAILED
main 20150715T045745 - FAILED
main 20150715T045330 - FAILED
main 20150715T045146 - FAILED
main 20150715T044437 - FAILED
```

Just remove them:

```bash
barman list-backup all|grep '\s-\sFAILED$'| {
    while read srv id _
    do
        echo barman delete $srv $id
        barman delete $srv $id
    done
}
```
