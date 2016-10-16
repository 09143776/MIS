v# MIS
管理信息系统
数据表<br/>
1．保养记录表</br>
CREATE TABLE `保养记录表` ( <br/>
  `保养记录ID` int(11) NOT NULL,<br/>
  `设备名称` varchar(45) DEFAULT NULL,<br/>
  `项目ID` int(11) DEFAULT NULL,<br/>
  `保养人` varchar(45) DEFAULT NULL,<br/>
  `时间` varchar(45) DEFAULT NULL,<br/>
  `保养内容` varchar(45) DEFAULT NULL,<br/>
  `设备ID` int(11) DEFAULT NULL,<br/>
  PRIMARY KEY (`保养记录ID`),<br/>
  KEY `设备名称_idx` (`设备名称`),<br/>
  CONSTRAINT `保养记录ID` FOREIGN KEY (`保养记录ID`) REFERENCES `保养消耗表` (`保养记录ID`) ON DELETE NO ACTION ON UPDATE NO ACTION
) ENGINE=InnoDB DEFAULT CHARSET=utf8;<br/>
2．保养项目表<br/>
 CREATE TABLE `保养项目表` (<br/>
  `项目ID` int(11) NOT NULL,<br/>
  `设备ID` int(11) DEFAULT NULL,<br/>
  `保养内容` varchar(45) DEFAULT NULL,<br/>
  PRIMARY KEY (`项目ID`)<br/>
) ENGINE=InnoDB DEFAULT CHARSET=utf8;<br/>
3保养消耗表<br/>
CREATE TABLE `保养消耗表` (<br/>
  `消耗ID` int(11) NOT NULL,<br/>
  `保养记录ID` int(11) DEFAULT NULL,<br/>
  `数量` int(11) DEFAULT NULL,<br/>
  `材料ID` int(11) DEFAULT NULL,<br/>
  PRIMARY KEY (`消耗ID`),<br/>
  KEY `保养记录ID_idx` (`保养记录ID`),<br/>
  CONSTRAINT `消耗ID` FOREIGN KEY (`消耗ID`) REFERENCES `材料表` (`材料ID`) ON DELETE NO ACTION ON UPDATE NO ACTION
) ENGINE=InnoDB DEFAULT CHARSET=utf8;<br/>
4．材料表<br/>
CREATE TABLE `材料表` (<br/>
  `材料ID` int(11) NOT NULL,<br/>
  `材料名称` varchar(45) DEFAULT NULL,<br/>
  `数量` int(11) DEFAULT NULL,<br/>
  PRIMARY KEY (`材料ID`)<br/>
) ENGINE=InnoDB DEFAULT CHARSET=utf8;<br/>
5．设备表<br/>
CREATE TABLE `设备表` (<br/>
  `设备ID` int(11) NOT NULL,<br/>
  `设备名称` varchar(45) DEFAULT NULL,<br/>
  `保养周期ID` int(11) DEFAULT NULL,<br/>
  PRIMARY KEY (`设备ID`),<br/>
  KEY `保养周期ID_idx` (`保养周期ID`),<br/>
  CONSTRAINT `保养周期ID` FOREIGN KEY (`保养周期ID`) REFERENCES `设备类型表` (`保养周期ID`) ON DELETE NO ACTION ON UPDATE NO ACTION
) ENGINE=InnoDB DEFAULT CHARSET=utf8;<br/>
6．设备类型表<br/>
CREATE TABLE `设备类型表` (<br/>
  `保养周期ID` int(11) NOT NULL,<br/>
  `保养周期` varchar(45) DEFAULT NULL,<br/>
  `设备ID` int(11) DEFAULT NULL,<br/>
  PRIMARY KEY (`保养周期ID`)<br/>
) ENGINE=InnoDB DEFAULT CHARSET=utf8;<br/>
1.	查询设备保养信息<br/>
SELECT * FROM 设备保养系统.保养记录表<br/>
where 保养记录ID=(select 保养记录ID from 设备保养系统.保养消耗表<br/> 
where 材料ID='1');<br/>

SELECT * FROM 设备保养系统.保养消耗表<br/>
where 材料ID='1';<br/>

SELECT * FROM 设备保养系统.保养项目表<br/>
where 设备ID='1';<br/>

2.查询设备到期<br/>
Select 设备ID from设备保养系统.设备类型表<br/>
Where 365-datediff(now(),(select date from 设备保养系统.保养类型表))<10;<br/>

3.E-R图
图上传到附件中

AXURE8.0模型地址： (http://4pzrab.axshare.com)<br/>
附件地址：(http://pan.baidu.com/s/1gfbT1IF)

