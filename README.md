# cockroachdb-release

![cockroach](http://i.imgur.com/4qKtitB.gif)

Release for [CockroachDB](https://github.com/cockroachdb/cockroach).

- Requires DNS
- Requires NTP synced time (ie ntp-release)
- Only supports TLS authentication
- Includes simple smoke tests errand

## Deploy

```
$ bosh -d cockroachdb deploy manifests/example.yml --vars-store ./creds.yml
```

Port forward admin UI locally:

```
$ bosh -d cockroachdb ssh cockroachdb/0 --opts=" -L 8080:127.0.0.1:8080"
```

Get debug info:

```
$ bosh -d cockroachdb run-errand report-health
$ bosh -d cockroachdb run-errand report-vars
$ bosh -d cockroachdb run-errand report-nodes-local

# or alternatively
$ bosh -d cockroachdb ssh cockroachdb -c '/var/vcap/jobs/cockroachdb/bin/debug' -r
```

Access `test` user generated certificates:

```
$ bosh interpolate ./creds.yml --path /cockroachdb_user_test/ca
$ bosh interpolate ./creds.yml --path /cockroachdb_user_test/certificate
$ bosh interpolate ./creds.yml --path /cockroachdb_user_test/private_key
```

See:

- [docs/usage.md](docs/usage.md)
- [docs/dev.md](docs/usage.md)
