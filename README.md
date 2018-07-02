Oracle Java on Docker
=====
Build a Docker image containing Oracle Java (Server JRE specifically).

The Oracle Java Server JRE provides the same features as Oracle Java JDK commonly required for Server-side Applications (i.e. Java EE application servers). For more information about Server JRE, visit the [Understanding the Server JRE](https://blogs.oracle.com/java-platform-group/understanding-the-server-jre) blog entry from the Java Product Management team.

Just to clarify these Docker build scripts are **unofficial** Oracle Build scripts. See [Oracle Docker images](https://github.com/oracle/docker-images) on GitHub for the official Oracle Docker build scripts.

Since the image is used as base image for Oracle Unified Directory it will also add a few common unix package. In particular the following additional packages including there dependencies will be installed:
    * *libaio* Linux-native asynchronous I/O access library
    * *tar* A GNU file archiving program
    * *gzip* The GNU data compression program
    * *zip* A file compression and packaging utility compatible with PKZIP
    * *unzip* A utility for unpacking zip files
 
## Java 8
Download Server JRE 8 [My Oracle Support](https://updates.oracle.com/ARULink/PatchDetails/process_form?patch_num=27412890) file and drop it inside folder `java-8`. If you download Java 1.8 with the latest update from MOS (see Doc ID [1439822.1](https://support.oracle.com/epmos/faces/DocumentDisplay?id=1439822.1)), make sure to not unzip the `p<PATCHID>_180<UPDATE>_Linux-x86-64.zip` file. This Dockerfile expects the Java package in the form `p27412890_180172_Linux-x86-64.zip`.

Build it:

```
$ cd java-8
$ docker build -t trivadisbds/serverjre:8 .
```

## Issues
Please file your bug reports, enhancement requests, questions and other support requests within [Github's issue tracker](https://help.github.com/articles/about-issues/):

* [Existing issues](https://github.com/TrivadisDocker/OracleJava/issues)
* [submit new issue](https://github.com/TrivadisDocker/OracleJava/issues/new)

## License
trivadis/docker is licensed under the GNU General Public License v3.0. You may obtain a copy of the License at <https://www.gnu.org/licenses/gpl.html>.

To download and run Oracle Java or any other Oracle product, regardless whether inside or outside a Docker container, you must download the binaries from the Oracle website and accept the license indicated at that page. See [OTN Developer License Terms](http://www.oracle.com/technetwork/licenses/standard-license-152015.html).