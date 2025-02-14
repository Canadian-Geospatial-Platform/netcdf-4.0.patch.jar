# netcdf-4.0.patch.jar

In 2024 (and 2025), attempt to build FGP version of GeoNetwork from source with Maven fails with the following message:

> [ERROR] Failed to execute goal on project core: Could not resolve dependencies for project org.geonetwork-opensource:core:jar:3.6.2-SNAPSHOT: edu.ucar:netcdf:jar:4.0.patch was not found in https://repo.osgeo.org/repository/release/ during a previous attempt. This failure was cached in the local repository and resolution is not reattempted until the update interval of osgeo has elapsed or updates are forced -> [Help 1]

As bernard reported at [#3160 (repo entry for netcdf/4.0.patch broken: misses the jar file) – OSGeo](https://trac.osgeo.org/osgeo/ticket/3160) on 2024-04-03, the netcdf-4.0.patch.jar was missing from <https://repo.osgeo.org/service/rest/repository/browse/release/edu/ucar/netcdf/4.0.patch/>, and that is still the case to this day.

Fortunately, NRCan colleague Andrew Henry has a cached copy in web/target/geonetwork/WEB-INF/lib/netcdf-4.0.patch.jar inside his local FGP GeoNetwork repository, and copying that file to ~/.m2/repository/edu/ucar/netcdf/4.0.patch/ does the trick:

```
$ ls -l ~/.m2/repository/edu/ucar/netcdf/4.0.patch/
total 3600
-rw-r--r--. 1 afok afok 3669919 Aug 17  2021 netcdf-4.0.patch.jar
-rw-r--r--. 1 afok afok     809 Feb 14 06:55 netcdf-4.0.patch.jar.lastUpdated
-rw-r--r--. 1 afok afok     190 Feb 14 06:34 netcdf-4.0.patch.pom
-rw-r--r--. 1 afok afok      40 Feb 14 06:34 netcdf-4.0.patch.pom.sha1
-rw-r--r--. 1 afok afok     168 Feb 14 06:34 _remote.repositories
```

And Maven is happy again!  `mvn clean install -Penv-prod,nap -DskipTests` (etc.) builds successfully!

This repository is a place to share the copy of netcdf-4.0.patch.jar in our cache:

- file size: 3.67 MB
- md5: 59d8b7ca98a97cef72f0c5494f458fa0
- sha1: aab48a9ee0b4befbf0932faac510f924a0dff4a7

to support the aforementioned [Ticket #3160 (repo entry for netcdf/4.0.patch broken: misses the jar file) – OSGeo](https://trac.osgeo.org/osgeo/ticket/3160).
Attempt to upload netcdf-4.0.patch.jar directly to the ticket failed due to upload file size limit of 585.9 KB there, hence this repository.

Cheers!
