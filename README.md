### Meegra database migration management tool

### COMMAND LINE VERSION:

Setup:
```sh
# create db in $HOME
$ meegra setup demo
OK - Created ${HOME}/.meegra_demo file!

$ meegra setup
ERROR - db file ${HOME}/.meegra_demo already created
 ```

Typical workflow:
```sh
# create new migration record
$ meegra sql query 

# edit mode:
# CREATE TABLE foo
# id SERIAL PRIMARY KEY,
# text VARCHAR(100) NOT NULL,
# ts_created TIMESTAMP DEFAULT NOW();

OK - Saved query with id 4!

# show all completed queries on local machine
$ meegra sql done
| id | query                                           
| 1  | ALTER TABLE demo_1 ADD COLUMN foo varchar(100); 
| 2  | CREATE TABLE demo_2 id SERIAL name text;         
| 3  | INSERT INTO demo_1 (foo) VALUES ('demo');       

# show all queries todo on this machine
$ meegra sql todo
| id | query 
| 4  | CREATE TABLE foo id SERIAL PRIMARY KEY, text VARCHAR(100) NOT NULL ts_created TIMESTAMP DEFAULT NOW(); 

# run all migrations on this machine
$ meegra sql run
Running todo queries...
OK - Executed query 4
Completed!

# show all queries todo
$ meegra sql todo
No queries to do...

# show all completed queries
$ meegra sql done
| id | query                                            
| 1  | ALTER TABLE demo_1 ADD COLUMN foo varchar(100);  
| 2  | CREATE TABLE demo_2 id SERIAL name text;          
| 3  | INSERT INTO demo_1 (foo) VALUES ('demo');        
| 4  | CREATE TABLE foo id SERIAL PRIMARY KEY, text VARCHAR(100) NOT NULL ts_created TIMESTAMP DEFAULT NOW(); 

```