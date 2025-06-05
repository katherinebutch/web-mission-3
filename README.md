# Mission 3



## Ссылка на папку со скринкастами и ссылками для копирования в Buildship:



https://drive.google.com/drive/folders/1vWoMIYMde0yoqpkrtIPX6Nms2zDL7Ayl?usp=sharing

## SQL Queries



**Запрос 1 - получить список юзернеймов пользователей**

SELECT username FROM users

```sql
SELECT username FROM users
```

**Запрос 2 - получить кол-во отправленных сообщений каждым пользователем:**

username - number of sent messages

```sql
SELECT id, COUNT(*) AS number_of_sent_messages
FROM messages
GROUP BY id;
```

**Запрос 3 - получить пользователя с самым большим кол-вом полученных сообщений и само количество**

username - number of received messages

```sql
SELECT 
    u.username,
    COUNT(m.id) AS "number of received messages"
FROM 
    users u
JOIN 
    messages m ON u.id = m."to"
GROUP BY 
    u.username
ORDER BY 
    COUNT(m.id) DESC
LIMIT 1;
```

**Запрос 4 - получить среднее кол-во сообщений, отправленное каждым пользователем**

username - number of received messages

```sql
    SELECT 
    AVG(message_count) AS "average_messages_per_user"
FROM 
    (SELECT u.id,
        COUNT(m.id) AS message_count
    FROM 
        users u
    LEFT JOIN 
        messages m ON u.id = m."from"
    WHERE
        u.id IN (1, 2) 
    GROUP BY u.id
    ) 
AS 
    user_message_counts;
```

