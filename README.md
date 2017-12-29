# Sqoop
->By default sqoop lauches 4 mappers at a time that's why import data  is divided into 4 files.
->If the table contain primary key in the table 
   command:sqoop import --connect jdbc:mysql://localhost/sai --username root -P --table ml
->If the table doesn't have the primary key the above command can't work.In this case we have use split-by or -m 1(use one mapper)
  Split-by:If the table doesnot have the primary key we have use either mapper or split-by.It use 4 mappers to split the data and stores the data in four files and doesnot store null valuesif the data is not     indexed(sorted).It sort the data and it takes time depending on the data.Split-by splits data accordning to the column
  example: [cloudera@quickstart ~]$ sqoop import --connect jdbc:mysql://localhost/sai --username root -P --table mp --split-by sno --target-dir /user/cloudera/pp
  -m 1:It doesnot sort the values.It uses only one mapper and stores the data in one file and it stores null values.
    example:[cloudera@quickstart ~]$ sqoop import --connect jdbc:mysql://localhost/sai --username root -P --table mp -m 1 sno --target-dir /user/cloudera/sp
 ->Incremental-import:every day table is updated.Updated values is added by using incremental import.Limitaion is the value shoud be in sorted(indexed) way.
   [cloudera@quickstart ~]$ sqoop import --connect jdbc:mysql://localhost/retail_db --username root -P --table sna -m 1 --target-dir /user/cloudera/test1 
   cloudera@quickstart ~]$ sqoop import --connect jdbc:mysql://localhost/retail_db --username root -P --table sna -m 1 --target-dir /user/cloudera/test1 --incremental append --check-column id --last-value 4
   Sqoop Job with Incremental :(created and saved the query we can use for multiple times by exec command an djob name)
[cloudera@quickstart ~]$ sqoop job --create exi -- import --connect jdbc:mysql://localhost/retail_db --username root -P --table sna -m 1 --target-dir /user/cloudera/test --incremental append --check-column id --last-value 0
[cloudera@quickstart ~]$ sqoop job --exec exi
[cloudera@quickstart ~]$ sqoop job --list(list all jobs)
[cloudera@quickstart ~]$ sqoop job --delete ei(delete the job)


