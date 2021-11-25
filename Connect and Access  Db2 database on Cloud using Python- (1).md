### Import the ibm_db Python Library


```python
import ibm_db
import pandas
import ibm_db_dbi
```

### Enter the database credentials


```python
dsn_hostname = "98538591-7217-4024-b027-8baa776ffad1.c3n41cmd0nqnrk39u98g.databases.appdomain.cloud" # e.g.: "54a2f15b-5c0f-46df-8954-7e38e612c2bd.c1ogj3sd0tgtu0lqde00.databases.appdomain.cloud"
dsn_uid = "vpt69061"        # e.g. "abc12345"
dsn_pwd = "lwQxKweEYdWnqArW"      # e.g. "7dBZ3wWt9XN6$o0J"

dsn_driver = "{IBM DB2 ODBC DRIVER}"
dsn_database = "BLUDB"            # e.g. "BLUDB"
dsn_port = "30875"                # e.g. "32733" 
dsn_protocol = "TCPIP"            # i.e. "TCPIP"
dsn_security = "SSL"              #i.e. "SSL"
```

### Create a dsn connection string


```python
dsn = (
    "DRIVER={0};"
    "DATABASE={1};"
    "HOSTNAME={2};"
    "PORT={3};"
    "PROTOCOL={4};"
    "UID={5};"
    "PWD={6};"
    "SECURITY={7};").format(dsn_driver, dsn_database, dsn_hostname, dsn_port, dsn_protocol, dsn_uid, dsn_pwd,dsn_security)

#print the connection string to check correct values are specified
print(dsn)
```

    DRIVER={IBM DB2 ODBC DRIVER};DATABASE=BLUDB;HOSTNAME=98538591-7217-4024-b027-8baa776ffad1.c3n41cmd0nqnrk39u98g.databases.appdomain.cloud;PORT=30875;PROTOCOL=TCPIP;UID=vpt69061;PWD=lwQxKweEYdWnqArW;SECURITY=SSL;
    

### Establish a connetion with the database


```python
try:
    conn = ibm_db.connect(dsn, "", "")
    print ("Connected to database: ", dsn_database, "as user: ", dsn_uid, "on host: ", dsn_hostname)

except:
    print ("Unable to connect: ", ibm_db.conn_errormsg() )
```

    Connected to database:  BLUDB as user:  vpt69061 on host:  98538591-7217-4024-b027-8baa776ffad1.c3n41cmd0nqnrk39u98g.databases.appdomain.cloud
    

### Retreive metadata for Database Server


```python
server = ibm_db.server_info(conn)

print("DBMS_NAME:", server.DBMS_NAME)
print ("DBMS_VER:  ", server.DBMS_VER)
print ("DB_NAME:   ", server.DB_NAME)
```

    DBMS_NAME: DB2/LINUXX8664
    DBMS_VER:   11.05.0600
    DB_NAME:    BLUDB
    

### Retreive metadata for Database Client


```python
client = ibm_db.client_info(conn)

print ("DRIVER_NAME:          ", client.DRIVER_NAME) 
print ("DRIVER_VER:           ", client.DRIVER_VER)
print ("DATA_SOURCE_NAME:     ", client.DATA_SOURCE_NAME)
print ("DRIVER_ODBC_VER:      ", client.DRIVER_ODBC_VER)
print ("ODBC_VER:             ", client.ODBC_VER)
print ("ODBC_SQL_CONFORMANCE: ", client.ODBC_SQL_CONFORMANCE)
print ("APPL_CODEPAGE:        ", client.APPL_CODEPAGE)
print ("CONN_CODEPAGE:        ", client.CONN_CODEPAGE)
```

    DRIVER_NAME:           DB2CLI.DLL
    DRIVER_VER:            11.05.0500
    DATA_SOURCE_NAME:      BLUDB
    DRIVER_ODBC_VER:       03.51
    ODBC_VER:              03.01.0000
    ODBC_SQL_CONFORMANCE:  EXTENDED
    APPL_CODEPAGE:         1252
    CONN_CODEPAGE:         1208
    

### Drop the table i


```python
dropQuery = "drop table INSTRUCTOR"

dropStmt = ibm_db.exec_immediate(conn, dropQuery)
```

### Create a table 


```python
createQuery = "create table INSTRUCTOR(ID INTEGER PRIMARY KEY NOT NULL, FIRSTNAME VARCHAR(20), LASTNAME VARCHAR(20), CITY VARCHAR(20), CCODE CHAR(2))"

createStmt = ibm_db.exec_immediate(conn,createQuery)
```

### Insert data in the table


```python
insertQuery = "insert into INSTRUCTOR values(1, 'Anna', 'Shetty', 'Chennai', 'CH')"

insertstmt = ibm_db.exec_immediate(conn,insertQuery)
```


```python
insertQuery1 = "insert into INSTRUCTOR values(2, 'Raju', 'Hatela', 'Tamil Nadu', 'TN')"

insertstmt1 = ibm_db.exec_immediate(conn,insertQuery1)
```


```python
insertQuery2 = "insert into INSTRUCTOR values(3, 'Shyam', 'Berde', 'Maharashtra', 'MH'), (4, 'Sid', 'Patel', 'Gujrat', 'GJ')"

insertStmt2 = ibm_db.exec_immediate(conn,insertQuery2)
```

### Query the data


```python
selectQuery = "select * from INSTRUCTOR"

selectStmt = ibm_db.exec_immediate(conn,selectQuery)

ibm_db.fetch_both(selectStmt)
```




    {'ID': 1,
     0: 1,
     'FIRSTNAME': 'Anna',
     1: 'Anna',
     'LASTNAME': 'Shetty',
     2: 'Shetty',
     'CITY': 'Chennai',
     3: 'Chennai',
     'CCODE': 'CH',
     4: 'CH'}




```python
while ibm_db.fetch_row(selectStmt) != False:
    print("ID:", ibm_db.result(selectStmt, 0), "FIRSTNAME:", ibm_db.result(selectStmt, "FIRSTNAME"), "LASTNAME:", ibm_db.result(selectStmt, "LASTNAME"), "CITY:", ibm_db.result(selectStmt, "CITY"), "CCODE:", ibm_db.result(selectStmt, "CCODE"))
```

    ID: 2 FIRSTNAME: Raju LASTNAME: Hatela CITY: Tamil Nadu CCODE: TN
    ID: 3 FIRSTNAME: Shyam LASTNAME: Berde CITY: Maharashtra CCODE: MH
    ID: 4 FIRSTNAME: Sid LASTNAME: Patel CITY: Gujrat CCODE: GJ
    


```python
updateQuery = "update INSTRUCTOR set CCODE ='MU' where FIRSTNAME='Shyam' and ID=3"

updateStmt = ibm_db.exec_immediate(conn,updateQuery)
```

### Connect to Pandas library and Retrieve data into Pandas


```python
pconn = ibm_db_dbi.Connection(conn)
```


```python
selectQuery = "select * from INSTRUCTOR"
# Retreive results into a pandas frame
pdf = pandas.read_sql(selectQuery, pconn)

pdf.LASTNAME[0]
```




    'Shetty'




```python
# Print the entire data
pdf
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>ID</th>
      <th>FIRSTNAME</th>
      <th>LASTNAME</th>
      <th>CITY</th>
      <th>CCODE</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Anna</td>
      <td>Shetty</td>
      <td>Chennai</td>
      <td>CH</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>Raju</td>
      <td>Hatela</td>
      <td>Tamil Nadu</td>
      <td>TN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Shyam</td>
      <td>Berde</td>
      <td>Maharashtra</td>
      <td>MU</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Sid</td>
      <td>Patel</td>
      <td>Gujrat</td>
      <td>GJ</td>
    </tr>
  </tbody>
</table>
</div>




```python
pdf.shape
```




    (4, 5)




```python
ibm_db.close(conn)
```




    True




```python

```
