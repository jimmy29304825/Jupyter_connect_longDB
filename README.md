# Jupyter_connect_longDB
this is a python jupyter which can connect longdb
```bash
docker-compose up -d
```
after you start the container, you have to do the command below
```bash
# Enter to jupyter's container
sudo docker exec -it line-chat-bot-jupyter bash

# Copy data from /tmp/driver
cp /tmp/driver/splice_odbc_linux64-2.7.62.0.tar.gz /tmp

# or Download yourself
cd /tmp; wget https://splice-releases.s3.amazonaws.com/odbc-driver/Linux64/splice_odbc_linux64-2.7.62.0.tar.gz

# Untar file
cd /tmp; tar -zxvf splice_odbc_linux64-2.7.62.0.tar.gz

# Install package
cd splice_odbc_linux64-2.7.62.0; ./install.sh

# enter >> set URL = [LongDB's IP] >> enter

# or Edit odbc.ini file 
nano /tmp/splice_odbc_linux64-2.7.62.0/odbc.ini
# URL = 127.0.0.1 change to LongDB's IP
```
test connect in jupyter
```python
import pyodbc
# Connect to LongDB
cnxn=pyodbc.connect("DSN=SpliceODBC64")

# Call sql command
cursor=cnxn.cursor()

# Run sql command
cursor.execute("select * from sys.systables")

# Get one row out
row=cursor.fetchone()
print('row:',row)

# Get all row out
row=cursor.fetchall()
print('row:',row)
```
