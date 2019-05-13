# AWS_connection
connecting database with AWS Cloud and upload information on S3
import psycopg2
import sys
import datetime
import time
try:
    con = psycopg2.connect(database="socero_staging", user="amit", password="empower1234", 
                       host="empower.cyxw3prqohxe.us-east-1.rds.amazonaws.com", port="5432")
except:
    print("not able to connect")
cur = con.cursor()
print con
a = cur.execute("select * from events")
f = open('F:/newfile.csv')
cur.copy_from(f, 'events', columns=('post_id','start_time', 'category' ,'title', 'event_desc', 'user_id' ), sep=",")
cur.commit()
cur.close()
con.close()
