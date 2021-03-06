In order to deploy a new version of mysql-dist artifact
to Maven Central you should do the following steps:

 1. Update `deploy/pom.xml` file with a new version of MySQL

 2. Download five files from http://dev.mysql.com/downloads/mysql/

   1. Windows 64
   2. Windows
   3. MacOS
   4. Linux amd64
   5. Linux x86

 3. Unpack them all

 4. Zip each of them with the following command:

```
$ cd directory_with_dist_content
$ zip -r ../linux-amd64.zip *
```

 5. Install it locally and test how it works with the plugin

```
$ mvn install:install-file -Dfile=mac-x86_64.zip -DgroupId=com.jcabi -DartifactId=mysql-dist -Dversion=5.6.21 -Dpackaging=zip -Dclassifier=mac-x86_64
```

 6. Sign them all, using gnupg:

```
$ gpg -ab pom.xml
$ gpg -ab mac-x86_64.zip
$ gpg -ab linux-amd64.zip
$ gpg -ab linux-x86_64.zip
$ gpg -ab windows-amd64.zip
$ gpg -ab windows-x86.zip
```

 5. Login to sonatype and deploy them both (pom.xml and all dist-*.zip). You
 should have these files before upload:

```
pom.xml
pom.pom.asc
mac-x86_64.zip
mac-x86_64.zip.asc
linux-amd64.zip
linux-amd64.zip.asc
linux-x86_64.zip
linux-x86_64.zip.asc
windows-amd64.zip
windows-amd64.zip.asc
windows-x86.zip
windows-x86.zip.asc
```
