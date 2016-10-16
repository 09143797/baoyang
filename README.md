# baoyang
1.数据表：<br/>
保养记录表：<br/>
CREATE TABLE `保养记录` (<br/>
  `保养记录id` int(11) NOT NULL AUTO_INCREMENT,<br/>
  `设备id` int(11) DEFAULT NULL,<br/>
  `保养者id` int(11) DEFAULT NULL,<br/>
  `保养日期` varchar(45) DEFAULT NULL,<br/>
  PRIMARY KEY (`保养记录id`),<br/>
  KEY `4_idx` (`设备id`),<br/>
  CONSTRAINT `4` FOREIGN KEY (`设备id`) REFERENCES `设备表` (`设备id`) ON DELETE NO ACTION ON UPDATE NO ACTION<br/>
) ENGINE=InnoDB AUTO_INCREMENT=2 DEFAULT CHARSET=utf8;<br/>
保养完成情况表：<br/>
CREATE TABLE `保养完成情况` (<br/>
  `保养项目id` int(11) NOT NULL,<br/>
  `设备id` int(11) DEFAULT NULL,<br/>
  `完成情况` varchar(45) DEFAULT NULL,<br/>
  `备注` varchar(45) DEFAULT NULL,<br/>
  PRIMARY KEY (`保养项目id`)<br/>
) ENGINE=InnoDB DEFAULT CHARSET=utf8;<br/>
保养消耗表：<br/>
CREATE TABLE `保养消耗` (<br/>
  `保养消耗id` int(11) NOT NULL,<br/>
  `材料名称name` varchar(45) DEFAULT NULL,<br/>
  `材料数量count` int(11) DEFAULT NULL,<br/>
  `保养记录id` varchar(45) DEFAULT NULL,<br/>
  PRIMARY KEY (`保养消耗id`)<br/>
) ENGINE=InnoDB DEFAULT CHARSET=utf8;<br/>
保养者表：<br/>
CREATE TABLE `保养者` (<br/>
  `保养者id` int(11) NOT NULL,<br/>
  `保养者name` varchar(45) DEFAULT NULL,<br/>
  `班组` varchar(45) DEFAULT NULL,<br/>
  PRIMARY KEY (`保养者id`)<br/>
) ENGINE=InnoDB DEFAULT CHARSET=utf8;<br/>
保养项目内容表：<br/>
CREATE TABLE `保养项目内容` (<br/>
  `保养项目id` int(11) NOT NULL,<br/>
  `保养内容content` varchar(45) DEFAULT NULL,<br/>
  PRIMARY KEY (`保养项目id`)<br/>
) ENGINE=InnoDB DEFAULT CHARSET=utf8;<br/>
设备表：<br/>
CREATE TABLE `设备表` (<br/>
  `设备id` int(11) NOT NULL<br/>
  `最后保养时间` date DEFAULT NULL,<br/>
  `保养周期` varchar(45) DEFAULT NULL,<br/>
  PRIMARY KEY (`设备id`)<br/>
) ENGINE=InnoDB DEFAULT CHARSET=utf8;<br/>
2.查询语句：
该检修的设备：
select * from 设备表;
select 设备id from 设备表;
where 365-datediff(now(),(select 最后保养时间 from 设备表))<3;
![er图](https://github.com/09143797/baoyang/blob/master/er图.png)
检修报告：
select 保养者，保养日期 from 保养记录;
where 设备id=1；
![w1](https://github.com/09143797/baoyang/blob/master/w1.png)
select 完成情况，备注 from 保养完成情况;
where 设备id=1；
![w2](https://github.com/09143797/baoyang/blob/master/w2.png)
select 保养内容 from 保养项目内容;
where 保养项目id=（select 保养项目id from 保养完成情况 where 设备id=1）；
![w3](https://github.com/09143797/baoyang/blob/master/w3.png)
