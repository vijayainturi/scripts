# scripts
Genericsqoop.sh


source ../.setSqoop
echo "Pls enter userid:"
read USERID
echo "Pls enter your passwd:"
read PASSWD
echo "Pls enter IP address of db host:"
read HIP
echo "Pls enter the number of mappers:"
read NUMMAP
echo "Pls enter the partition:"
read PART
echo "Pls enter the Teradata SQL:"
read TD_SQL
echo "Pls enter the target directory folder name:"
read TARGET_LOC
sqoop import -Djava.security.egd=file:/dev/./urandom -libjars $HIVE_LIB_JARS \
-Dteradata.db.input.job.type=hdfs \
-e "select * from $TD_SQL" \
--connect jdbc:teradata://$HIP/database=RX_TB \
--connection-manager org.apache.sqoop.teradata.TeradataConnManager \
--username $USERID --password $PASSWD \
--as-textfile \
--fields-terminated-by '|' \
--target-dir /data/prod/cvs/$TARGET_LOC/$PART \
--m $NUMMAP
