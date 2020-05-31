# DayZ Trader and Bank logging

### Requires

[Trader Bank logging from Steam Workshop](https://steamcommunity.com/sharedfiles/filedetails/?id=2114540423 "@TBLogging")

[Trader mod by Dr_J0nes](https://steamcommunity.com/sharedfiles/filedetails/?id=1590841260)

[Banking mod by Deadcraft](https://steamcommunity.com/workshop/filedetails/?id=1836257061)


### Instructions

Open `class.php` and edit your DayZ server profile directory at line 9. This is where your log files and other mod config files are.

Run `database.sql` onto your MySQL server.

Edit in MySQL connection details, starting line 16 `class.php`. You can have a SELECT only privileged user for tight security on the front end or just use an INSERT, UPDATE, SELECT privileged user for the whole class.

#### Fetching logs

Putting log files into the Database (`fetch.php`):

```php
<?php
require_once('class.php');
$dz = new dzTraderBankLogging();

$dz->setLogType('trade');//Trader logs
$dz->processLogs();

$dz->setLogType('atm');//ATM logs
$dz->processLogs();
```

Point a Cron job at this for every one or two minutes for up-to date data or once an hour otherwise.


`index.php` has most recent hours as 24 by default and limit for most recent table as 100 default.
Change these with `index.php?hours=X&limit=X`


__NOTE There is no access protection for the front end, it is best to have front end files on a localhost__