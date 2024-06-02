# Stop and start windows update services

<!-- Run cmd as an admin -->

$ net stop wuauserv
$ net stop cryptSvc
$ net stop bits
$ net stop msiserver

<!-- To start just run the same commands but with net start -->

<!-- TO clear update cache go to C:\Windows\SoftwareDistribution\ , select all files, right-click a file, and choose the trash can icon-->
