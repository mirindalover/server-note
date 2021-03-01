## 门户权限设计

门户权限设计可以视为网站一个模块的权限，设计到网站的用户权限、模块的用户权限以及模块内菜单的权限

- 涉及的表

> sys_user(网站用户角色)、portal_user_relation(门户角色)、portal_menu(门户菜单)、portal_user_auth(门户菜单权限)

- portal_menu表的设计

> menu_uuid、menu_level、parent_uuid、show_sort

### 接口逻辑

- 获取用户有权限的菜单

获取应用权限(管理员)->获取门户权限(管理员)->获取门户真正菜单权限

- 构建前端tree结构

1、获取数据时通过 level、sort排序

2、创建 HashMap<String, Tree>存储uuid对应的对象、List<Tree> 存储一级菜单

3、遍历查询库出来的list，根据是否是一级来存放到不同位置