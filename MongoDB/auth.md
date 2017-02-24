# mongoDB 的权限设置

## 1 设置权限

1. add a userAdminAnyDatabase to the admin db

    ```
    $ mongo admin
    > db.addUser({ user: "myadmin", pwd: "1234", roles: ["userAdminAnyDatabase"] })
    ```
2. turn on authentication in /etc/mongodb.conf
    
    ```
    auth = true
    setParameter = enableLocalhostAuthBypass=0  # I don't use this param
    ```
3. connect using the new myadmin user to any database you want and add further users:
    
    ```
    $ mongo admin -u myadmin -p 1234
    > db.addUser({ user: "user", pwd: "1234", roles: ["readWrite"] })
    ```
    
    or
    
    ```
    > use another
    > db.addUser({ user: "user", pwd: "1234", roles: ["readWrite"] })
    ```

## Reference

- [What MongoDB user privileges do I need to add a user to a new/another mongo database? - stackoverflow](http://stackoverflow.com/questions/20525103/what-mongodb-user-privileges-do-i-need-to-add-a-user-to-a-new-another-mongo-data)
