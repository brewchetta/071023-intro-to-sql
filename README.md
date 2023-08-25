# Intro to SQL

Here are the commands and output from class:

```SQL
Enter ".help" for usage hints.
sqlite> .schema
sqlite> CREATE TABLE students (
   ...> name TEXT
   ...> );
sqlite> .schema
CREATE TABLE students (
name TEXT
);
sqlite> INSERT INTO students (name) VALUES ("Chett");
sqlite> SELECT * FROM students;
Chett
sqlite> .headers on
sqlite> .mode column
sqlite> SELECT * FROM students;
name
-----
Chett
sqlite> DROP TABLE students;
sqlite> .schema
sqlite> CREATE TABLE students (
   ...> id INTEGER PRIMARY KEY,
   ...> name TEXT,
   ...> grade NUMBER,
   ...> enrolled BOOLEAN
   ...> );
sqlite> .schema
CREATE TABLE students (
id INTEGER PRIMARY KEY,
name TEXT,
grade NUMBER,
enrolled BOOLEAN
);
sqlite> INSERT INTO students (name, grade, enrolled) VALUES (`Sakib`, 64, false);
Error: in prepare, no such column: Sakib (1)
sqlite> INSERT INTO students (name, grade, enrolled) VALUES ("Sakib", 64, false);
sqlite> SELECT * FROM students;
id  name   grade  enrolled
--  -----  -----  --------
1   Sakib  64     0       
sqlite> INSERT INTO students (name, grade, enrolled) VALUES ("Luke Skywalker", 70, true);
sqlite> INSERT INTO students (enrolled, name, grade) VALUES ();
Error: in prepare, near ")": syntax error (1)
sqlite> .headers on
sqlite> .mode columns
sqlite> .help
.archive ...             Manage SQL archives
.auth ON|OFF             Show authorizer callbacks
.backup ?DB? FILE        Backup DB (default "main") to FILE
.bail on|off             Stop after hitting an error.  Default OFF
.binary on|off           Turn binary output on or off.  Default OFF
.cd DIRECTORY            Change the working directory to DIRECTORY
.changes on|off          Show number of rows changed by SQL
.check GLOB              Fail if output since .testcase does not match
.clone NEWDB             Clone data into NEWDB from the existing database
.connection [close] [#]  Open or close an auxiliary database connection
.databases               List names and files of attached databases
.dbconfig ?op? ?val?     List or change sqlite3_db_config() options
.dbinfo ?DB?             Show status information about the database
.dump ?OBJECTS?          Render database content as SQL
.echo on|off             Turn command echo on or off
.eqp on|off|full|...     Enable or disable automatic EXPLAIN QUERY PLAN
.excel                   Display the output of next command in spreadsheet
.exit ?CODE?             Exit this program with return-code CODE
.expert                  EXPERIMENTAL. Suggest indexes for queries
.explain ?on|off|auto?   Change the EXPLAIN formatting mode.  Default: auto
.filectrl CMD ...        Run various sqlite3_file_control() operations
.fullschema ?--indent?   Show schema and the content of sqlite_stat tables
.headers on|off          Turn display of headers on or off
.help ?-all? ?PATTERN?   Show help text for PATTERN
.import FILE TABLE       Import data from FILE into TABLE
.imposter INDEX TABLE    Create imposter table TABLE on index INDEX
.indexes ?TABLE?         Show names of indexes
.limit ?LIMIT? ?VAL?     Display or change the value of an SQLITE_LIMIT
.lint OPTIONS            Report potential schema issues.
.load FILE ?ENTRY?       Load an extension library
.log FILE|off            Turn logging on or off.  FILE can be stderr/stdout
.mode MODE ?TABLE?       Set output mode
.nonce STRING            Disable safe mode for one command if the nonce matches
.nullvalue STRING        Use STRING in place of NULL values
.once ?OPTIONS? ?FILE?   Output for the next SQL command only to FILE
.open ?OPTIONS? ?FILE?   Close existing database and reopen FILE
.output ?FILE?           Send output to FILE or stdout if FILE is omitted
.parameter CMD ...       Manage SQL parameter bindings
.print STRING...         Print literal STRING
.progress N              Invoke progress handler after every N opcodes
.prompt MAIN CONTINUE    Replace the standard prompts
.quit                    Exit this program
.read FILE               Read input from FILE
.recover                 Recover as much data as possible from corrupt db.
.restore ?DB? FILE       Restore content of DB (default "main") from FILE
.save FILE               Write in-memory database into FILE
.scanstats on|off        Turn sqlite3_stmt_scanstatus() metrics on or off
.schema ?PATTERN?        Show the CREATE statements matching PATTERN
.selftest ?OPTIONS?      Run tests defined in the SELFTEST table
.separator COL ?ROW?     Change the column and row separators
.session ?NAME? CMD ...  Create or control sessions
.sha3sum ...             Compute a SHA3 hash of database content
.shell CMD ARGS...       Run CMD ARGS... in a system shell
.show                    Show the current values for various settings
.stats ?ARG?             Show stats or turn stats on or off
.system CMD ARGS...      Run CMD ARGS... in a system shell
.tables ?TABLE?          List names of tables matching LIKE pattern TABLE
.testcase NAME           Begin redirecting output to 'testcase-out.txt'
.testctrl CMD ...        Run various sqlite3_test_control() operations
.timeout MS              Try opening locked tables for MS milliseconds
.timer on|off            Turn SQL timer on or off
.trace ?OPTIONS?         Output each SQL statement as it is run
.vfsinfo ?AUX?           Information about the top-level VFS
.vfslist                 List all available VFSes
.vfsname ?AUX?           Print the name of the VFS stack
.width NUM1 NUM2 ...     Set minimum column widths for columnar output
sqlite> INSERT INTO students (enrolled, name, grade) VALUES (false, "Chett", 85);
sqlite> SELECT * FROM students;
id  name            grade  enrolled
--  --------------  -----  --------
1   Sakib           64     0       
2   Luke Skywalker  70     1       
3   Chett           85     0       
sqlite> SELECT * FROM students
   ...> WHERE NOT enrolled;
id  name   grade  enrolled
--  -----  -----  --------
1   Sakib  64     0       
3   Chett  85     0       
sqlite> SELECT * FROM students
   ...> WHERE enrolled = 0;
id  name   grade  enrolled
--  -----  -----  --------
1   Sakib  64     0       
3   Chett  85     0       
sqlite> SELECT * FROM students
   ...> WHERE name = "Luke Skywalker";
id  name            grade  enrolled
--  --------------  -----  --------
2   Luke Skywalker  70     1       
sqlite> SELECT * FROM students
   ...> WHERE name LIKE "%Luke%";
id  name            grade  enrolled
--  --------------  -----  --------
2   Luke Skywalker  70     1       
sqlite> SELECT * FROM students
   ...> WHERE name LIKE "Luke%";
id  name            grade  enrolled
--  --------------  -----  --------
2   Luke Skywalker  70     1       
sqlite> SELECT * FROM students
   ...> WHERE name LIKE "%Luke";
sqlite> SELECT * FROM students
   ...> WHERE id = 1;
id  name   grade  enrolled
--  -----  -----  --------
1   Sakib  64     0       
sqlite> UPDATE students (grade) VALUES (65) WHERE id = 1;
Error: in prepare, near "(": syntax error (1)
sqlite> UPDATE students
   ...> SET grade = 65
   ...> WHERE id = 1;
sqlite> SELECT * FROM students;
id  name            grade  enrolled
--  --------------  -----  --------
1   Sakib           65     0       
2   Luke Skywalker  70     1       
3   Chett           85     0       
sqlite> UPDATE students
   ...> SET grade = 100, enrolled = true
   ...> WHERE id = 1;
sqlite> SELECT * FROM students;
id  name            grade  enrolled
--  --------------  -----  --------
1   Sakib           100    1       
2   Luke Skywalker  70     1       
3   Chett           85     0       
sqlite> UPDATE students SET enrolled = 1 WHERE id = 3;
sqlite> SELECT * FROM students;
id  name            grade  enrolled
--  --------------  -----  --------
1   Sakib           100    1       
2   Luke Skywalker  70     1       
3   Chett           85     1       
sqlite> UPDATE students SET enrolled = 0 WHERE grade > 80;
sqlite> SELECT * FROM students;
id  name            grade  enrolled
--  --------------  -----  --------
1   Sakib           100    0       
2   Luke Skywalker  70     1       
3   Chett           85     0       
sqlite> DELETE FROM students WHERE id = 2;
sqlite> SELECT * FROM students;
id  name   grade  enrolled
--  -----  -----  --------
1   Sakib  100    0       
3   Chett  85     0       
sqlite> INSERT INTO students (name, grade, enrolled) VALUES ("Mohammad", 82, true);
sqlite> SELECT * FROM students;
id  name      grade  enrolled
--  --------  -----  --------
1   Sakib     100    0       
3   Chett     85     0       
4   Mohammad  82     1       
sqlite> INSERT INTO students (id, name, grade, enrolled) VALUES (2, "Mohammad", 82, true);
sqlite> SELECT * FROM students;
id  name      grade  enrolled
--  --------  -----  --------
1   Sakib     100    0       
2   Mohammad  82     1       
3   Chett     85     0       
4   Mohammad  82     1       
sqlite> DELETE FROM students WHERE id = 2;
sqlite> SELECT * FROM students;
id  name      grade  enrolled
--  --------  -----  --------
1   Sakib     100    0       
3   Chett     85     0       
4   Mohammad  82     1       
sqlite> INSERT INTO students (name, grade, enrolled) VALUES ("Bob the raccoon", 0, true);
sqlite> SELECT * FROM students;
id  name             grade  enrolled
--  ---------------  -----  --------
1   Sakib            100    0       
3   Chett            85     0       
4   Mohammad         82     1       
5   Bob the raccoon  0      1       
sqlite> DELETE FROM students WHERE id = 5;
sqlite> SELECT * FROM students;
id  name      grade  enrolled
--  --------  -----  --------
1   Sakib     100    0       
3   Chett     85     0       
4   Mohammad  82     1       
sqlite> INSERT INTO students (name, grade, enrolled) VALUES ("Bob the raccoon", 0, true);
sqlite> SELECT * FROM students;
id  name             grade  enrolled
--  ---------------  -----  --------
1   Sakib            100    0       
3   Chett            85     0       
4   Mohammad         82     1       
5   Bob the raccoon  0      1       
sqlite> INSERT INTO students (id, name, grade, enrolled) VALUES (5, "Bob the raccoon", 0, true);
Error: stepping, UNIQUE constraint failed: students.id (19)
sqlite> INSERT INTO students (id, name, grade, enrolled) VALUES (10, "Bob the raccoon", 0, true);
sqlite> SELECT * FROM students;
id  name             grade  enrolled
--  ---------------  -----  --------
1   Sakib            100    0       
3   Chett            85     0       
4   Mohammad         82     1       
5   Bob the raccoon  0      1       
10  Bob the raccoon  0      1       
sqlite> INSERT INTO students (name, grade, enrolled) VALUES ("Bob the raccoon", 0, true);
sqlite> SELECT * FROM students;
id  name             grade  enrolled
--  ---------------  -----  --------
1   Sakib            100    0       
3   Chett            85     0       
4   Mohammad         82     1       
5   Bob the raccoon  0      1       
10  Bob the raccoon  0      1       
11  Bob the raccoon  0      1       
sqlite> UPDATE students SET vaccinated = true;
Error: in prepare, no such column: vaccinated (1)
sqlite> ALTER TABLE students ADD vaccinated BOOLEAN;
sqlite> SELECT * FROM students;
id  name             grade  enrolled  vaccinated
--  ---------------  -----  --------  ----------
1   Sakib            100    0                   
3   Chett            85     0                   
4   Mohammad         82     1                   
5   Bob the raccoon  0      1                   
10  Bob the raccoon  0      1                   
11  Bob the raccoon  0      1                   
sqlite> UPDATE students
   ...> SET vaccinated true;
Error: in prepare, near "true": syntax error (1)
sqlite> UPDATE students
   ...> SET vaccinated = true
   ...> WHERE id = 3;
sqlite> SELECT * FROM students;
id  name             grade  enrolled  vaccinated
--  ---------------  -----  --------  ----------
1   Sakib            100    0                   
3   Chett            85     0         1         
4   Mohammad         82     1                   
5   Bob the raccoon  0      1                   
10  Bob the raccoon  0      1                   
11  Bob the raccoon  0      1                   
sqlite> UPDATE students
   ...> SET vaccinated = true
   ...> WHERE id = 3,4,5,10,11;
Error: in prepare, near ",": syntax error (1)
sqlite> UPDATE students
   ...> SET vaccinated = true
   ...> WHERE id IN (3,5,11);
sqlite> SELECT * FROM students;
id  name             grade  enrolled  vaccinated
--  ---------------  -----  --------  ----------
1   Sakib            100    0                   
3   Chett            85     0         1         
4   Mohammad         82     1                   
5   Bob the raccoon  0      1         1         
10  Bob the raccoon  0      1                   
11  Bob the raccoon  0      1         1         
sqlite> UPDATE students SET vaccinated = NULL WHERE id = 3;
sqlite> SELECT * FROM students;
id  name             grade  enrolled  vaccinated
--  ---------------  -----  --------  ----------
1   Sakib            100    0                   
3   Chett            85     0                   
4   Mohammad         82     1                   
5   Bob the raccoon  0      1         1         
10  Bob the raccoon  0      1                   
11  Bob the raccoon  0      1         1         
sqlite> UPDATE students SET name = NULL, grade = NULL WHERE id = 3;
sqlite> SELECT * FROM students;
id  name             grade  enrolled  vaccinated
--  ---------------  -----  --------  ----------
1   Sakib            100    0                   
3                           0                   
4   Mohammad         82     1                   
5   Bob the raccoon  0      1         1         
10  Bob the raccoon  0      1                   
11  Bob the raccoon  0      1         1         
sqlite> ALTER TABLE students RENAME COLUMN vaccinated TO passing;
sqlite> SELECT * FROM students;
id  name             grade  enrolled  passing
--  ---------------  -----  --------  -------
1   Sakib            100    0                
3                           0                
4   Mohammad         82     1                
5   Bob the raccoon  0      1         1      
10  Bob the raccoon  0      1                
11  Bob the raccoon  0      1         1      
sqlite> SELECT LENGTH("students") AS number_of_students;
number_of_students
------------------
8                 
sqlite> SELECT LENGTH(students) AS number_of_students;
Error: in prepare, no such column: students (1)
sqlite> SELECT COUNT(id) FROM students;
COUNT(id)
---------
6        
sqlite> SELECT COUNT(name) FROM students;
COUNT(name)
-----------
5          
sqlite> SELECT AVG(grade) FROM students;
AVG(grade)
----------
36.4      
sqlite> .quit
```
