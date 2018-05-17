<!-- CSS work goes here for the time being -->
<!-- set a:link text-decoration to none -->
<!-- set a:hover text-decoration to underline -->
<!-- http://forums.markdownpad.com/discussion/143/include-pdf-pagebreak-instructions-in-markdown/p1 -->

---
<div style="page-break-after: always;"></div>

# <center> Challenges - May 18, 2018 - Singapore

* Overview
  * Build a CM-managed CDH cluster and secure it
* Place your work in the `challenges/labs` folder
  * All text files require  Markdown (`.md`) extension and formatting
  * All screenshots must be in PNG format
  * You will create each required file yourself
* You may consult with each other and research online
  * Submit only your own work
* Update GitHub often -- don't wait until the end
* If you break your cluster, or your cluster breaks you:
  * Tell the instructor
  * Push the work you have into GitHub
  * Create an Issue to describe what you think went wrong

---
<div style="page-break-after: always;"></div>

## <center> Challenge Setup

* Create the Issue `Challenges Setup`
* Make sure `manojsundaram` and `melvin-koh` are Collaborators
* Assign the Issue to yourself and label it `started`
* Destroy your lab instances and create 5 new instances (Follow the same instructions from the lab, plus make sure your root volume EBS storage has 50 GB allocated).
* In the file `challenges/labs/0_setup.md`:
  * List the cloud provider you are using
  * List your instances by IP address and DNS name (don't use `/etc/hosts` for this)
  * List the Linux release you are using
  * List the file system capacity for the first node
  * List the command and output for `yum repolist enabled`
* Add the following Linux accounts to all nodes
  * User `jimenez` with a UID of `2800`
  * User `beltran` with a UID of `2900`
  * Create the group `astros` and add `beltran` to it
  * Create the group `rangers` and add `jimenez` to it
* List the `/etc/passwd` entries for `jimenez` and `beltran`
  * Do not list the entire file
* List the `/etc/group` entries for `astros` and `rangers`
  * Do not list the entire file
* Push these updates to GitHub
* Label your Issue `review`
* Assign the Issue to the instructor

---
<div style="page-break-after: always;"></div>

## <center> Challenge 1: Install a MySQL/MariaDB server

* Create the Issue `Install Database`
* Assign the Issue to yourself and label it `started`
* Install MySQL 5.5 or MariaDB 5.5 on the first node listed in `0_setup.md`
  * Use a YUM repository to install the package
  * Copy the repo configuration you use to `challenges/labs/1_my-database-server.repo.md`
* On all cluster nodes
  * Install the database client package and JDBC connector jar on all nodes
* Start the server and create these databases:
  * `scm`
  * `rman`
  * `hive`
  * `oozie`
  * `hue`
  * `sentry`
* Record the following in `challenges/labs/1_db-server.md`
  * The command `hostname -f` and its output
  * The command `mysql -u <user> -p<password> -e "status;"` and its output
  * The command `mysql -u <user>  -p<password> -e "show databases;"` and its output
* Push this work to GitHub
* Label the Issue `review` and assign it to the instructor

---
<div style="page-break-after: always;"></div>

## <center> Challenge 2: Install Cloudera Manager

* Create the Issue `Install CM`
* Assign yourself and label it `started`
* Install Cloudera Manager on the second node listed in `0_setup.md`
* List the command and output for `ls /etc/yum.repos.d` in `challenges/labs/1_cm.md`
  * Copy `cloudera-manager.repo` to `challenges/labs/2_cloudera-manager.repo.md`
* Connect Cloudera Manager Server to its database
  * Use the `scm_prepare_database.sh` script to create the `db.properties` file
  * List the full command and its output in `2_properties.md`
  * Add the `db.properties` file content to `2_properties.md`
* Start the Cloudera Manager server
* In `challenges/labs/2_cm_startup.md` add:
  * The first line of the server log
  * The line(s) that contain the phrase "Started Jetty server"
* Push these changes to GitHub and label the Issue `review`
* Assign the issue to the instructor

---
<div style="page-break-after: always;"></div>

## <center> Challenge 3 - Install CDH 5.13

* Create the Issue `Install CDH`
* Assign yourself and label it `started`
* Deploy Coreset services + HBase
  * Rename your cluster after your GitHub handle
* Create user directories in HDFS for `jimenez` and `beltran`
* Add the following to `3_cm.md`:
    * The command and output for `hdfs dfs -ls /user`
    * The command and output from the CM API call `../api/v5/hosts`
    * The command and output from the CM API call `../api/v11/clusters/<githubName>/services`
* Install the Hive sample data using Hue
    * Copy a Hue screen that shows the tables are loaded to `challenges/labs/3_hue_hive.png`
* Push this work to GitHub and label the Issue `review`
* Assign the issue to the instructor

---
<div style="page-break-after: always;"></div>

## <center> Challenge 4 - HDFS Testing

* Create the Issue `Test HDFS`
* Assign yourself and label it `started`
* As user `jimenez`, use `teragen` to generate a 65,536,000-record dataset
  * Write the output to 8 files
  * Set the block size to 64 MB
  * Set the mapper container size to 512 MiB
  * Name the target directory `tgen`
  * Use the `time` command to capture job duration
* Put the following in `challenges/labs/4_teragen.md`
  * The full `teragen` command and output
  * The result of the `time` command
  * The command and output of `hdfs dfs -ls /user/jimenez/tgen`
  * The command and output of `hadoop fsck -blocks /user/jimenez`
* Push this work to GitHub and label the Issue `review`
* Assign the issue to the instructors

---
<div style="page-break-after: always;"></div>

## <center> Challenge 5 - Kerberize the cluster

* Create the Issue `Kerberize cluster`
* Assign the issue to yourself and label it `started`
* Install an MIT KDC on the first node of your cluster
  * Name your realm after your GitHub handle
  * Use `SG` as a suffix
  * For example: `MANOJS.SG`
* Create Kerberos user principals for `jimenez`, `beltran`, and `cloudera-scm`
  * Assign `cloudera-scm` the privileges needed to create service principals and keytab files
* Kerberize the cluster
* Run the `terasort` program as user `jimenez` with the output target `/user/jimenez/tsort`
  * Use the `tgen` directory as input
  * Copy the command and full output to `challenges/labs/5_terasort.md`
* Run the Hadoop `pi` program as user `beltran`
  * Use the task parameters to `50` and `100`
  * Copy the command and full output to `challenges/labs/5_pi.md`
*  Copy the configuration files in `/var/kerberos/krb5kdc/` to your repo:
    * Add the prefix `5_` and the suffix `.md` to the original file name
    * Example: `5_kdc.conf.md`
* Push this work to GitHub and label the Issue `review`
* Assign the issue to the instructor

---
<div style="page-break-after: always;"></div>

## <center> Challenge 6 - Install & Configure the Sentry Service

* Create the Issue `Install Sentry`
  * Label it `started`
* Use Cloudera Manager to install and enable Sentry
* Configure both Hive & Impala to use Sentry
* Create a role for `HttpViewer` that can read the `web_logs` database
  * Assign the `rangers` group to this role
* Create a role for `ServiceViewer` that can read the `customers` databases
  * Assign the `astros` group to this role
* Use `beeline` to select ten records from `web_logs`
* Use `beeswax` to select ten records from `customers`
* Capture the beeline text and save to `6_beeline.md`
* Screen-capture the results for beeswax and save to `6_beeswax.png`
* Label the issue `review`
* Assign the issue to the instructor
* Push all work to GitHub

---
<div style="page-break-after: always;"></div>

## <center> When time runs out:

* Commit any outstanding changes from your repo to GitHub
* Email `manojs@cloudera.com`that you have stopped pushing to your repo
---
<div style="page-break-after: always;"></div>
