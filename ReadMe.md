后台管理系统
技术点：springboot+mybaits+shiro+maven+springAop
sql文件：放在resources下面 jtsys.sql
主要实现系统管理功能，商品管理或者其它业务需要在扩展

主要功能：日志管理/用户管理/角色管理/部门管理/菜单管理
    
shiro框架的使用：https://blog.csdn.net/weixin_45146962/article/details/109696518

## 动吧

### 系统技术点

#### spring
- IOC/DI
    - Spring管理MAP容器
    - 注入方式：构造和set注入
- AOP
    - Aspect 切面
    - Pointcut 切入点，对应一个类或者一个方法
        - bean 粗粒度,类级别
        - within 粗粒度,类级别
        - **excution 细粒度,方法 excution(\* com.XxxService..\*.\*(..))**
        - @annotation 细粒度,方法
    - 通知
        - @Before
        - @AfterReturning
        - @AfterThrowing
        - @After
        - **@around**
#### mybatis
- assocation
    - property 对应实体类属性
    - select 对应dao/mapper查询方法
    - cloumn 两个表用哪个字段进行关联
- collection
    - 同上
- 动态SQL <if..test...>/<sql>/<where>/<foreach>/<trim>...
#### shiro框架
- 两个配置文件：ShiroConfig和WebConfig
- realm:身份认证和权限认证
- subject:提交用户信息给securityManager

#### 动吧系统


```
graph LR
动吧系统-->部门管理
动吧系统-->用户管理
动吧系统-->角色管理
动吧系统-->菜单管理
动吧系统-->日志管理
```
```
graph LR
部门-->|1对N| 用户
用户-->|N对1| 角色
角色-->|1对N| 菜单
```

```
graph TB
A[用户登录]-->B[修改]
B[修改]-->D[进入模块]
A[用户登录]-->C[查询]
C[查询]-->D[进入模块]
D[进入模块]-->E{是否包含子模块}
E{是否包含子模块}-->|是|F[修改子模块]
E{是否包含子模块}-->|否|G[修改当前模块]
F[修改子模块]-->E{是否包含子模块}
G[修改当前模块]-->H[END]
```
