# metabase-db2-driver
DB2 Driver for Metabase v0.39.0.1, works with Db2 LUW V11.5.

Thanks to everyone.
+ @dludwig-jrt https://github.com/damienchambe/metabase-db2-driver
+ @cabo40 https://github.com/cabo40/metabase-db2-driver  
+ @damienchambe https://github.com/damienchambe/metabase-db2-driver

## Building the driver
### Prereqs: Install Metabase locally, compiled for building drivers

```bash
cd /path/to/
git clone -b v0.39.0.1 https://github.com/metabase/metabase.git
cd metabase
lein install-for-building-drivers
```

### Build it

```bash
cd /path/to/<metabase-db2-driver>
lein clean
DEBUG=1 LEIN_SNAPSHOTS_IN_RELEASE=true lein uberjar
```

### Copy it to your plugins dir and restart Metabase
```bash
cp target/uberjar/db2.metabase-driver.jar /path/to/metabase/plugins/
jar -jar /path/to/metabase/metabase.jar
```

## Configurations

You can run as follows to avoid the CharConversionException exceptions. By this way, JCC converts invalid characters to NULL instead of throwing exceptions.

```bash
java -Ddb2.jcc.charsetDecoderEncoder=3 -jar metabase.jar
```


Use this additional JDBC properties for performance, uncommitted read ("dirty" read), and to be able to use date and time

```bash
defaultIsolationLevel=1;readOnly=true;prompt=false;naming=sql;date format=iso;time format=hms;time separator=colon;
```

