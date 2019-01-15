**Perl for Oracle**

You need to install oracle InstantClient rpms from Oracle WebSite. For
examle:
```
   oracle-instantclient12.2-basic-12.2.0.1.0-1.x86_64.rpm
   oracle-instantclient12.2-devel-12.2.0.1.0-1.x86_64.rpm
   oracle-instantclient12.2-sqlplus-12.2.0.1.0-1.x86_64.rpm
   yum localinstall -y oracle*.rpm --nogpgcheck
```
These InstantClient package will be installed in the following
directories:
```
   /usr/lib/oracle/12.2/client64/bin (sqlplus)
   /usr/lib/oracle/12.2/client64/lib (basic)
   /usr/share/oracle/12.2 (devel)
```
You need to set Oracle Environment Variables
```
   export PATH=/usr/lib/oracle/12.2/client64/bin:\$PATH
   export LD\_LIBRARY\_PATH=/usr/lib/oracle/12.2/client64/lib
   export ORACLE\_HOME=/usr/lib/oracle/12.2/client64
   export TNS\_ADMIN=/path/to/your/tnsnames-file
```
Install perl-DBI perl-ExtUtils-MakeMaker
```
   yum install -y perl-DBI perl-ExtUtils-MakeMaker
```
Install Perl DBD::Oracle module
```
   Download the Perl DBD-Oracle-Version-tar.gz file from cpan.metacpan.org
   Extract the gz file
   Run perl Makefile.PL ; make ; make install
   Oracle.pm under /usr/local/lib64/perl5/DBD/Oracle.pm
```
To use DBI Oracle module you need to setup environments
```
   ORACLE_HOME, LD_LBRARY_PATH, TNS_ADMIN
```
Test script
```use DBI;
   $dbh = DBI->connect("dbi:Oracle:$dbname", $user, $passwd);
```
# oraperl.sh (single script to install DBD::Oracle Module)
```
yum localinstall -y oracle\*.rpm \--nogpgcheck

export PATH=/usr/lib/oracle/12.2/client64/bin:$PATH
export LD_LIBRARY_PATH=/usr/lib/oracle/12.2/client64/lib
export ORACLE_HOME=/usr/lib/oracle/12.2/client64

yum install -y perl-DBI
yum install -y perl-ExtUtils-MakeMaker perl-ExtUtils-ParseXS
perl-Digest-SHA

echo "Build DBD::ORacle Module DBD-Oracle-1.76.tar.gz"
DBDFile=`ls -l DBD-Oracle* | awk '{print \$9}'`
tar -xzvf $DBDFile -C /tmp
cd /tmp/DBD-Oracle*
DBDir=$PWD
perl Makefile.PL
make
make install
rm -rf $DBDir
```
**Perl for MySQL**
```
yum install perl-DBD-MySQL or yum install \"perl(DBD::mysql)\"
```
**Perl for Postgres **
```
yum install perl-DBD-Pg or yum install \"perl(DBD::Pg)\"
```
**Perl for MongoDB **
```
Download MongoDB.tar.gz file from metacpan.org and run
make Makefile.PL; make; make install
MongoDB requires many Dependencies - please the mtacpan.org
```
**Other perl Modules you may need for other applications**
```
SASL yum install perl-Authen-SASL
SSL yum install perl-IO-Socket-SSL
```

**Other useful perl commands**

How to find \@INC path
```
perl -V
```
How to list out all the installed Perl Modules
```
   #!/bin/perl
   use File::Find;
   my @files;
   find(
      {
       wanted => sub {
       push @files, $File::Find::fullname
       if -f $File::Find::fullname && \\.pm$/
          },
       follow => 1,
       follow_skip => 2,
      },
   @INC
   );
```
```
How to check if a perl module installed
   perl -MModule::Name -e1 OR perldoc Module::Name
```
```
Add your custom Perl Module path
   Export PERL5LIB=
   *A list of directories in which to look for Perl library files
    before looking in the standard library.*
```
