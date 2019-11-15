# MySQL docker 

## how to use

setup environment file .env

as followw
```shell=
MYSQL_INITDB=
MYSQL_USER=
MYSQL_PASSWD=
MYSQL_ROOT_PASSWD=
MYSQL_DIR=
```
## verify

connect to the localhost:3306

```script==
const mysql = require('mysql');
const dotenv = require('dotenv');

dotenv.config();

const host = process.env.MYSQL_HOST;
const dbName = process.env.MYSQL_INITDB;
const user = process.env.MYSQL_USER;
const passwd = process.env.MYSQL_PASSWD;

const connection = mysql.createConnection({
    host,
    user,
    password: passwd,
    database: dbName
});

connection.connect();

const doSum = async () =>{
    return new Promise((resolve, reject)=>{
        connection.query(`SELECT 1+1 AS solution`, (err,result, field)=>{
            if(err) {
                reject(err);
            }
            else {
                console.log(result[0]);
                resolve(result[0]);
            }
        });
    });
};

(async()=>{
    try {
        let result = await doSum();
        console.log(`result`, result.solution);
    } catch(err) {
        console.error(err);
    } finally {
        connection.end();
    }
})();

```
