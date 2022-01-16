# End-to-end-ETL-Automation

This repository gives a clear understanding of extraction of data from the source, transform the data and load the data to the target through full automation.

# Explanation

I have created a database name sss in mysql table then I use this database. Next step is I created a table name txntab in hive then, load the data reside in HDFS directory /user/cloudera/txnsd.txt into mysql table txntab.

Next, I go to the edge node and create a file using touch exec.sh, then use command vi exec.sh and paste the sqoop and hive commands which i need to automate.

# Those following are the jobs which i want to automate

     1) sqoop import --connect jdbc:mysql://localhost/sss --username root --password cloudera  --table txntab -m 1 --target-dir /user/cloudera/srcdata
     2) hive -e "create table srctab1(id int,tdate string,category string) row format delimited fields terminated by ',' location '/user/cloudera/srcdata';create external table tartab1(id int,tdate string,category string) row format delimited fields terminated by ',' location '/user/cloudera/ttdir';insert into tartab1 select * from srctab1 where category='Gymnastics';drop table srctab1;drop table tartab1;"

# Complete step by tep process
1- create a database name sss;

2- Use sss;

3- create table txntab(id int,tdate varchar(100),category varchar(100));

4- load data local infile '/home/cloudera/data/txnsd.txt' into table txntab fields terminated by ',';

5- touch exec.sh (edge node command)

6- vi exec.sh    (----- Click 'I' ----> put the below commands ---> Click 'ESC' --- > :wq!)

7. Paste those below commands 

     sqoop import --connect jdbc:mysql://localhost/sss --username root --password cloudera  --table txntab -m 1 --target-dir /user/cloudera/srcdata
      
     hive -e "create table srctab1(id int,tdate string,category string) row format delimited fields terminated by ',' location '/user/cloudera/srcdata';create external table    tartab1(id int,tdate string,category string) row format delimited fields terminated by ',' location '/user/cloudera/ttdir';insert into tartab1 select * from srctab1 where category='Gymnastics';drop table srctab1;drop table tartab1;"
      
 8. Run sh exec.sh (edge node command).

      
