# How to setup the server for trial

I(vorotamoroz) want to discuss it a little more. Using fly.io is discussed on [Main repo](https://github.com/vrtmrz/obsidian-livesync/discussions/85)

# Using fly.io

1. Install the CLI ([Docs](https://fly.io/docs/hands-on/installing/))
```
$ curl -L https://fly.io/install.sh | sh
```
or 
```
iwr https://fly.io/install.ps1 -useb | iex
```

2. Sign up (Credit card is required)
```
flyctl auth signup
```

3. Create the working directory
```
mkdir flyio
cd flyio
mkdir couchdb
cd couchdb
```

5. Create an app by CouchDB's image
```
flyctl launch --image couchdb
```

Wizard will be launched, answer as you like
```
$ flyctl launch --image couchdb:latest
Creating app in ..../flyio/couchdb
Using image couchdb:latest
? App Name (leave blank to use an auto-generated name):
Automatically selected personal organization: vorotamoroz
? Select region: nrt (Tokyo, Japan)
Created app xxxxxx-yyyyyyy-0000 in organization personal
Wrote config file fly.toml
? Would you like to setup a Postgresql database now? No
? Would you like to deploy now? No
```

6. Create data volume
```
fly volumes create --region nrt couchdata --size 2
```
(This means make 2 GB data volume in the Tokyo region, you have to adjust region you selected)

8. Modify created fly.toml as like below. Please change COUCHDB_USER
(I noticed that I snipped instance information lines, please keep these lines) 
```

[build]
  image = "couchdb:latest"

[env]
  COUCHDB_USER = "your_name"

[mounts]
  source="couchdata"
  destination="/opt/couchdb/data"

[experimental]
  allowed_public_ports = []
  auto_rollback = true

[[services]]
  http_checks = []
  internal_port = 5984
  processes = ["app"]
  protocol = "tcp"
  script_checks = []
  [services.concurrency]
    hard_limit = 25
    soft_limit = 20
    type = "connections"

  [[services.ports]]
    force_https = true
    handlers = ["http"]
    port = 80

  [[services.ports]]
    handlers = ["tls", "http"]
    port = 443

  [[services.tcp_checks]]
    grace_period = "1s"
    interval = "15s"
    restart_limit = 0
    timeout = "2s"

```

10. Set your password as you like.
```
flyctl secrets set COUCHDB_PASSWORD=your_password
```

11. Deploy
```
flyctl deploy
```

12. Open in browser.
```
flyctl open
```
If you get CouchDB's information, It's ok.

13. Open /\_utils, Set up CouchDB (Just hit `Configure a Single Node`)
https://xxxxxx-yyyyyyy-0000.fly.dev/_utils/#/setup
If you have been asked username and password, use COUCHDB_USER and COUCHDB_PASSWORD.

14. Set up Self-hosted LiveSync 

| key | value |
| --- | --- |
| URI | https://xxxxxx-yyyyyyy-0000.fly.dev |
| Username | COUCHDB_USER |
| Password | COUCHDB_PASSWORD |
| Database name | anything_you_like |

15. Hit the `Check database configuration` button and Every `Fix` button.

16. Hit the `Test database connection` button.
If you get `Connected to ...`, it works!
17. If you suspend the server. you can do this by setting count to 0. (We can run it again with count 1.)

```
fly scale count 0
```

