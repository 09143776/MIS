<h1>一、查询用户test2可以查看的页面：</h1>
<h2>1.sql语句</h2>
 use db;
 SELECT cp.PrivilegeMaster AS '角色',
	cp.PrivilegeMasterKey AS '类型ID',
    cp.PrivilegeAccess AS '对象',
	cp.PrivilegeAccessKey AS '对象ID',
	sm.MenuName AS '菜单名称'
  FROM cf_privilege AS cp
  LEFT JOIN sys_menu AS sm ON cp.PrivilegeAccessKey = sm.MenuID AND cp.PrivilegeAccess = 'Sys_Menu'
 WHERE ((cp.PrivilegeMaster = 'CF_Role'
	AND cp.PrivilegeMasterKey
		IN (SELECT RoleID FROM cf_userrole AS cur
		LEFT JOIN cf_user AS cu ON cur.UserID = cu.UserID WHERE cu.LoginName='test2' ))
OR
(cp.PrivilegeMaster = 'CF_User' AND cp.PrivilegeMasterKey = (SELECT UserID FROM cf_user WHERE LoginName = 'test2')))
AND cp.PrivilegeOperation = 'Permit' AND cp.PrivilegeAccess = 'Sys_Menu';
<h2>2.结果截图</h2>
![结果截图](/1.png)
<h2>3.伪代码:</h2>
      1、根据名称查找人员ID:UserID
      2、根据人员ID:UserID查找改人员所对应的角色集合RoleIDs
      3、权限表 LEFT JOIN 页面表并查找
         角色为CF_Role   AND   角色ID在角色集合RoleIDs中
          OR
         角色为CF_User   AND   人员ID为UserID
         AND 权限属性为Permit   AND   权限为Sys_Menu的数据
 <h1>二、对订单页面中的操作权限：</h1>
 <h2>1.sql语句</h2>
  use db;
SELECT cp.PrivilegeMaster AS '角色',
  cp.PrivilegeMasterKey AS '类型ID',
  cp.PrivilegeAccess AS '对象',
  cp.PrivilegeAccessKey AS '对象ID',
  sb.BtnName AS '按钮名称'
  FROM cf_privilege AS cp
  LEFT JOIN sys_button AS sb ON cp.PrivilegeAccessKey = sb.BtnID AND cp.PrivilegeAccess = 'Sys_Button'
  LEFT JOIN sys_menu AS sm ON sb.MenuNo = sm.MenuNo
  WHERE ((cp.PrivilegeMaster = 'CF_Role'
            AND cp.PrivilegeMasterKey
            IN (SELECT RoleID FROM cf_userrole AS cur
              LEFT JOIN cf_user AS cu ON cur.UserID = cu.UserID WHERE cu.LoginName='test2' ))
               OR
               (cp.PrivilegeMaster = 'CF_User'
               AND cp.PrivilegeMasterKey = (SELECT UserID FROM cf_user WHERE LoginName = 'test2')))
               AND
               cp.PrivilegeOperation = 'Permit' AND cp.PrivilegeAccess = 'Sys_Button' AND sm.MenuName = '订单';
<h2>2.结果截图</h2>
![结果截图](/2.png)
<h2>3.伪代码:</h2>
      1、根据名称查找人员IDUserID
      2、根据人员IDUserID查找改人员所对应的角色集合RoleIDs
      3、权限表 LEFT JOIN 按钮表 LEFT JOIN 页面表并查找
              角色为CF_Role   AND   角色ID在角色集合RoleIDs中
               OR
             角色为CF_User   AND   人员ID为UserID
             AND 权限属性为Permit   AND   权限为Sys_Button AND 菜单名字为订单的数据
               
