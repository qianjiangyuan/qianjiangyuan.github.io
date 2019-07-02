# 4.5: db

db设计不用多讲，使用的是influxdb，操作和MySQL相同。

表结构如下：

jobtable

```
     `id`        INT          NOT NULL AUTO_INCREMENT,
     `jobId` varchar(50)   NOT NULL,
     `familyToken` varchar(50)   NOT NULL,
     `isParent` INT   NOT NULL,
     `jobName`         varchar(1024) NOT NULL,
     `userName`         varchar(255) NOT NULL,
     `jobStatus`         varchar(255) NOT NULL DEFAULT 'unapproved',
     `jobStatusDetail` LONGTEXT  NULL, 
     `jobType`         varchar(255) NOT NULL,
     `jobDescriptionPath`  TEXT NULL,
     `jobDescription`  LONGTEXT  NULL,
     `jobTime` DATETIME     DEFAULT CURRENT_TIMESTAMP NOT NULL,
     `endpoints` LONGTEXT  NULL, 
     `errorMsg` LONGTEXT  NULL, 
     `jobParams` LONGTEXT  NOT NULL, 
     `jobMeta` LONGTEXT  NULL, 
     `jobLog` LONGTEXT  NULL, 
     `retries`             int    NULL DEFAULT 0,
     PRIMARY KEY (`id`),
     INDEX (`userName`),
     INDEX (`jobTime`),
     INDEX (`jobId`),
     INDEX (`jobStatus`)
```



clusterstatustable

```
     `id`        INT   NOT NULL AUTO_INCREMENT,
     `status`         TEXT NOT NULL,
     `time` DATETIME     DEFAULT CURRENT_TIMESTAMP NOT NULL,
     PRIMARY KEY (`id`)
```

commandtable

```
    `id`        INT     NOT NULL AUTO_INCREMENT,
    `jobId` varchar(50)   NOT NULL,
    `status`         varchar(255) NOT NULL DEFAULT 'pending',
    `time` DATETIME     DEFAULT CURRENT_TIMESTAMP NOT NULL,
    `command` TEXT NOT NULL, 
    `output` TEXT NULL, 
    PRIMARY KEY (`id`)
```

usertable

```
`id`        INT     NOT NULL AUTO_INCREMENT,
`username`         varchar(255) NOT NULL,
`userId`         varchar(255) NOT NULL,
`time` DATETIME     DEFAULT CURRENT_TIMESTAMP NOT NULL,
PRIMARY KEY (`id`)
```

