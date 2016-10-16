# MIS
管理信息系统
数据表
1．保养记录表
CREATE TABLE `保养记录表` (
  `保养记录ID` int(11) NOT NULL,
  `设备名称` varchar(45) DEFAULT NULL,
  `项目ID` int(11) DEFAULT NULL,
  `保养人` varchar(45) DEFAULT NULL,
  `时间` varchar(45) DEFAULT NULL,
  `保养内容` varchar(45) DEFAULT NULL,
  `设备ID` int(11) DEFAULT NULL,
  PRIMARY KEY (`保养记录ID`),
  KEY `设备名称_idx` (`设备名称`),
  CONSTRAINT `保养记录ID` FOREIGN KEY (`保养记录ID`) REFERENCES `保养消耗表` (`保养记录ID`) ON DELETE NO ACTION ON UPDATE NO ACTION
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
2．保养项目表
 CREATE TABLE `保养项目表` (
  `项目ID` int(11) NOT NULL,
  `设备ID` int(11) DEFAULT NULL,
  `保养内容` varchar(45) DEFAULT NULL,
  PRIMARY KEY (`项目ID`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
3保养消耗表
CREATE TABLE `保养消耗表` (
  `消耗ID` int(11) NOT NULL,
  `保养记录ID` int(11) DEFAULT NULL,
  `数量` int(11) DEFAULT NULL,
  `材料ID` int(11) DEFAULT NULL,
  PRIMARY KEY (`消耗ID`),
  KEY `保养记录ID_idx` (`保养记录ID`),
  CONSTRAINT `消耗ID` FOREIGN KEY (`消耗ID`) REFERENCES `材料表` (`材料ID`) ON DELETE NO ACTION ON UPDATE NO ACTION
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
4．材料表
CREATE TABLE `材料表` (
  `材料ID` int(11) NOT NULL,
  `材料名称` varchar(45) DEFAULT NULL,
  `数量` int(11) DEFAULT NULL,
  PRIMARY KEY (`材料ID`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
5．设备表
CREATE TABLE `设备表` (
  `设备ID` int(11) NOT NULL,
  `设备名称` varchar(45) DEFAULT NULL,
  `保养周期ID` int(11) DEFAULT NULL,
  PRIMARY KEY (`设备ID`),
  KEY `保养周期ID_idx` (`保养周期ID`),
  CONSTRAINT `保养周期ID` FOREIGN KEY (`保养周期ID`) REFERENCES `设备类型表` (`保养周期ID`) ON DELETE NO ACTION ON UPDATE NO ACTION
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
6．设备类型表
CREATE TABLE `设备类型表` (
  `保养周期ID` int(11) NOT NULL,
  `保养周期` varchar(45) DEFAULT NULL,
  `设备ID` int(11) DEFAULT NULL,
  PRIMARY KEY (`保养周期ID`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
1.	查询设备保养信息
SELECT * FROM 设备保养系统.保养记录表
where 保养记录ID=(select 保养记录ID from 设备保养系统.保养消耗表 
where 材料ID='1');

SELECT * FROM 设备保养系统.保养消耗表
where 材料ID='1';

SELECT * FROM 设备保养系统.保养项目表
where 设备ID='1';

2.查询设备到期
Select 设备ID from设备保养系统.设备类型表
Where 365-datediff(now(),(select date from 设备保养系统.保养类型表))<10;

3.E-R图
图上传到附件中

AXURE8.0模型地址： (http://4pzrab.axshare.com)
附件地址：(http://pan.baidu.com/s/1gfbT1IF)

