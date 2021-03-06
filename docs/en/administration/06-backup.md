% Backup and Recovery

## Backup

While running, export the Job definitions if you do not have these in source control:

(1) Export the jobs. You will have to do this for each project

        rd-jobs list -f /path/to/backup/dir/project1/jobs.xml -p project1
        rd-jobs list -f /path/to/backup/dir/project2/jobs.xml -p project2
        ...

(2) Stop the server. See: [startup and shutdown](#startup-and-shtudown). (Rundeck data file backup should only be done with the server down.)

        rundeckd stop

(3) Copy the data files. (Assumes file datastore configuration). The
location of the data directory depends on the installation method:

       * RPM install: `/var/lib/rundeck/data`
       * Launcher install: `$RDECK_BASE/server/data`

            cp -r data /path/to/backup/dir
             
(3) Copy the log (execution output) files.

       * RPM install: `/var/lib/rundeck/logs`
       * Launcher install: `$RDECK_BASE/var/logs`

            cp -r logs /path/to/backup/dir

(4) Start the server

         rundeckd start

## Recovery

(1) Stop the server. See: [startup and shutdown](#startup-and-shtudown). (Rundeck recovery should only be done with the server down.)

        rundeckd stop

(2) Restore data/logs dir from backup (Refer to above for appropriate log/data path):

        cp -r /path/to/backup/logs logspath
        cp -r /path/to/backup/data datapath

(3) Start the server:

        rundeckd start

(4) Reload the Job definitions. You will have to do this for each project:

        rd-jobs load -f /path/to/backup/dir/project1/jobs.xml -p project1
        rd-jobs load -f /path/to/backup/dir/project2/jobs.xml -p project2
