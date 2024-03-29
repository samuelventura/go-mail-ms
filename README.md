# go-mail-ms

Send only restful mail micro service

- curl is the cli
- open relay 
- no policy

## api

```bash
# show domain
curl -X GET http://127.0.0.1:31650/api/domain/domain.tld
# show domain pub key for dkim dns record
curl -X GET http://127.0.0.1:31650/api/domain/domain.tld/pub
# add domain generates rsa key pair
curl -X POST http://127.0.0.1:31650/api/domain/domain.tld
# delete domain
curl -X DELETE http://127.0.0.1:31650/api/domain/domain.tld
# import domain in json format
curl -X POST http://127.0.0.1:31650/api/domain --data @path/file.json
# list domain names
curl -X GET http://127.0.0.1:31650/api/domain
# send mail in text/plain | text/html format
curl -X POST http://127.0.0.1:31650/api/mail \
  -H "Mail-From: i@domain.tld" \
  -H "Mail-To: u@gmail.com" \
  -H "Mail-Subject: Mail Subject" \
  -H "Mail-Mime: text/plain" \
  --data "Mail body."
```

## helpers

```bash
#MAIL_LOGS=/var/log
#MAIL_ENDPOINT=127.0.0.1:31650
#MAIL_DB_DRIVER=sqlite|postgres
#MAIL_DB_SOURCE=<driver dependant>
#https://gorm.io/docs/connecting_to_the_database.html
ssh -D 31699 proxy.com
export MAIL_SOCKS=127.0.0.1:31699
export MAIL_HOSTNAME=proxy.com
go install && go-mail-ms
go install && go-mail-ss
sqlite3 ~/go/bin/go-mail-ms.db3 ".tables"
sqlite3 ~/go/bin/go-mail-ms.db3 ".schema domain_dros"
sqlite3 ~/go/bin/go-mail-ms.db3 ".schema message_dros"
sqlite3 ~/go/bin/go-mail-ms.db3 ".schema attempt_dros"
sqlite3 ~/go/bin/go-mail-ms.db3 "select * from domain_dros"
sqlite3 ~/go/bin/go-mail-ms.db3 "select * from message_dros"
sqlite3 ~/go/bin/go-mail-ms.db3 "select * from attempt_dros"
#for go-sqlite in linux
sudo apt install build-essentials
dig gmail.com MX
```

# resources

- https://dkimcore.org/
- http://www.open-spf.org/
- https://www.mail-tester.com/
- https://www.mailgenius.com/
- https://tldp.org/HOWTO/Spam-Filtering-for-MX/smtpintro.html
