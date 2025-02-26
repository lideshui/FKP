### 目录结构

在Java开发中，根据阿里巴巴的开发规范，对实体类（Entity）进行包结构的设计时，通常会根据它们的职责和用途进行分层和分类。在典型的Spring Boot或Spring MVC项目中，你可能会遇到不同类型的实体类，如Domain（领域模型）、DTO（数据传输对象，Data Transfer Object）、VO（值对象，Value Object）等。

以下是一个建议的包结构，可以帮助你组织这些不同类型的实体类：

```
src
├── main
│   ├── java
│   │   └── com
│   │       └── yourcompany
│   │           └── yourproject
│   │               ├── config          # Spring配置类，如数据源、拦截器
│   │               ├── controller      # 控制器类，HTTP请求处理层，仅保留接口入口逻辑
│   │               ├── domain          # 领域模型，业务核心实体，与数据库解耦，仅关注业务行为，承载业务逻辑，如户权限体系
│   │               ├── model           # 数据库实体映射，包含与业务相关的数据结构，如User表映射类或前端交互的数据包装
│   │               ├── dto             # 数据传输对象，用于跨层数据传递，如Feign接口参数
│   │               ├── vo              # 视图对象，专供前端展示，如前端页面渲染专用数据结构
│   │               ├── mapper          # MyBatis接口定义，需与resources/mapper/XML文件对应
│   │               ├── dao             # 数据访问层
│   │               ├── service         # 服务接口层，interface定义
│   │               ├── service/impl/   # 服务实现层，具体逻辑实现
│   │               └── util            # 全局工具类
│   ├── resources
│   │   ├── application.yml			   # 应用配置
│   │   └── mapper                      # MyBatis Mapper XML文件
│   └── test
│       └── java
│           └── com
│               └── yourcompany
│                   └── yourproject
│                       └── YourTestClass.java  # 测试类，命名格式如UserServiceTest
```


