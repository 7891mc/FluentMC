================================================================================
                        FluentMC 面板 - 项目介绍
================================================================================

项目名称: FluentMC
版本号:   1.0.0
作者:     FluentMC
仓库地址: https://github.com/7891mc/FluentMC.git
构建工具: Maven (pom.xml)
运行环境: Java 21+, Minecraft 1.21.8 (Paper/Spigot)
官网：有.雨.top

================================================================================
一、项目概述
================================================================================

FluentMC 是一款 Minecraft 服务器 Web 管理面板插件, 提供公网可访问的 Win11
风格 Web 管理界面。管理员只需在浏览器中输入服务器地址和端口, 即可远程管理
服务器, 无需登录游戏客户端。

核心特点:
  - 零外部依赖: 使用 JDK 内置 HttpServer, 打包后仅一个轻量 jar
  - WinUI 风格界面: 深色/浅色主题切换, Win11 级别交互体验
  - 公网远程访问: 绑定 0.0.0.0 即可从公网管理服务器
  - Token 认证: 登录后颁发令牌, 支持配置有效期
  - 插件桥接架构: 通过反射检测可选依赖, 未安装时自动隐藏对应功能
  - 纯反射 Hook: 所有可选插件集成均使用反射, 不会因缺少依赖而崩溃


================================================================================
二、项目结构
================================================================================

mc-server-panel/
|
|-- pom.xml                          Maven 构建配置
|-- src/main/java/com/mcpanel/
|   |-- ServerPanel.java             插件主类 (入口)
|   |-- config/
|   |   |-- PanelConfig.java         配置包装器
|   |-- core/
|   |   |-- MinecraftService.java     Bukkit API 线程安全桥接
|   |   |-- LuckPermsHook.java       LuckPerms 权限组集成
|   |   |-- DeluxeTagsHook.java      DeluxeTags 称号集成
|   |   |-- TabHook.java             TAB 列表/计分板集成
|   |   |-- PlaceholderAPIHook.java  PlaceholderAPI 云拓展集成
|   |   |-- MiniMOTDHook.java        MiniMOTD 渐变色 MOTD 集成
|   |   |-- MultiverseHook.java      Multiverse-Core 多世界集成
|   |   |-- PlanHook.java            Plan 玩家数据分析集成
|   |   |-- EssentialsHook.java      EssentialsX 基础功能集成
|   |   |-- DailyRewardHook.java     每日奖励集成
|   |-- util/
|   |   |-- AuthManager.java         登录令牌管理
|   |   |-- Json.java                JSON 序列化工具
|   |-- web/
|       |-- WebServer.java           内嵌 HTTP 服务器
|       |-- ApiHandler.java          REST API 路由处理器
|
|-- src/main/resources/
    |-- plugin.yml                   插件描述文件
    |-- config.yml                   默认配置文件
    |-- web/                         前端静态资源
        |-- index.html               面板主页面
        |-- css/panel.css            样式表
        |-- js/api.js                API 客户端
        |-- js/panel.js              面板核心逻辑


================================================================================
三、核心功能模块
================================================================================

1. 仪表盘 (Dashboard)
   - 实时显示 TPS (1分钟)、在线人数、内存使用、运行时长
   - 5 秒自动刷新 (可配置)
   - 显示 Minecraft 版本和服务器类型

2. 玩家管理 (Players)
   - 在线玩家列表: 显示名称、UUID、健康、游戏模式、坐标
   - 操作: 踢出、封禁、发送消息、切换游戏模式、OP 权限管理

3. 白名单管理 (Whitelist)
   - 一键开关白名单
   - 添加/移除白名单成员
   - 实时同步至服务器白名单文件

4. 世界管理 (Worlds)
   - 控制游戏时间 (设为白天/黑夜/正午)
   - 控制天气 (晴朗/降雨/雷暴)
   - 设置世界难度 (和平/简单/普通/困难)

5. 控制台 (Console)
   - 在浏览器中直接执行服务器命令
   - 命令黑名单过滤 (防止越权执行危险命令)
   - 实时回显命令输出

6. 权限管理 (LuckPerms)
   - 查看所有权限组
   - 创建/删除权限组
   - 为权限组添加/移除权限节点
   - 查看权限组成员列表
   - 管理玩家所属权限组 (添加/移除/设为主组)

7. 称号管理 (DeluxeTags)
   - 查看所有称号定义
   - 创建/编辑/删除称号 (支持颜色代码)
   - 开关聊天栏称号显示
   - 管理称号与权限组的关联

8. TAB 列表 (TAB)
   - 编辑 Tab 列表页眉页脚 (支持 MiniMessage 渐变色)
   - 创建/删除 Tab 分组 (前缀/后缀/自定义名称)
   - 编辑计分板 (标题/行内容/开关/隐藏默认)

9. 外观自定义 (Appearance)
   - 上传服务器图标 (自动转换为 server-icon.png)
   - 自定义 MOTD 描述文本
   - MiniMOTD 渐变色 MOTD 编辑 (MiniMessage 格式)
   - MOTD 实时预览 (模拟服务器列表显示效果)
   - 最大玩家数/假玩家数设置

10. PAPI 云拓展 (PlaceholderAPI)
    - 查看已安装的云拓展列表
    - 浏览 PlaceholderAPI 云端拓展市场
    - 一键安装/卸载云拓展
    - 刷新云端缓存

11. 多世界管理 (Multiverse-Core)
    - 查看所有 Multiverse 管理的世界列表
    - 创建新世界 (指定环境和生成器)
    - 导入已有世界文件夹
    - 删除世界
    - 修改世界属性 (难度/游戏模式/PVP 开关)

12. 数据分析 (Plan)
    - 查看注册玩家总数
    - 显示 Plan 版本和 Web 端口
    - 一键跳转 Plan 自带 Web 分析面板
    - 支持在线时长趋势、地理分布等深度分析

13. 基础功能 (EssentialsX)
    - Warp 传送点管理 (列表/删除)
    - Kit 礼包管理 (列表/发放)
    - 玩家状态查询 (余额/Home 数量/Jail/Mute 状态)
    - 设置玩家余额
    - 切换玩家 Jail/Mute 状态

14. 每日奖励 (DailyReward)
    - 查看所有奖励定义 (ID/显示名称/冷却/权限/命令数)
    - 编辑奖励配置 (显示名称/冷却时间/奖励命令)
    - 强制为玩家发放奖励 (忽略冷却)
    - 重置玩家领取记录

15. 系统设置 (Settings)
    - 全服广播
    - 深色/浅色主题切换
    - 自动刷新间隔设置
    - 重启/停止服务器 (二次确认)


================================================================================
四、插件桥接机制
================================================================================

FluentMC 采用纯反射 Hook 架构集成可选插件, 确保零依赖冲突:

检测流程:
  1. 启动时依次尝试加载所有 Hook
  2. 每个 Hook 通过 Bukkit.getPluginManager().getPlugin() 检测目标插件
  3. 若插件存在且已启用, 缓存反射句柄, 标记 isAvailable() = true
  4. 若插件不存在, 标记 isAvailable() = false, 不影响面板运行

侧边栏动态显隐:
  - 所有插件相关侧边栏入口默认 display:none
  - 登录成功后调用 /api/hooks 接口获取所有插件可用性
  - 仅有可用插件的入口才显示, 未检测到的自动隐藏

已适配插件清单:
  +-------------------+------------------+----------------------------------+
  | 插件名称          | Hook 类           | 集成方式                        |
  +-------------------+------------------+----------------------------------+
  | LuckPerms         | LuckPermsHook    | 反射 API +LuckPerms Java API    |
  | DeluxeTags        | DeluxeTagsHook   | 直接读写 config.yml +命令重载   |
  | TAB               | TabHook          | 反射 API +配置文件读写          |
  | PlaceholderAPI    | PlaceholderAPIHook| 反射 API (eCloud)              |
  | MiniMOTD          | MiniMOTDHook     | 反射 API +配置文件读写          |
  | Multiverse-Core   | MultiverseHook   | 纯反射 (MVWorldManager)        |
  | Plan              | PlanHook         | 反射 API +配置文件读取          |
  | Essentials        | EssentialsHook   | 纯反射 (IEssentials)           |
  | DailyReward       | DailyRewardHook  | 配置文件直读直写 +命令派发      |
  +-------------------+------------------+----------------------------------+


================================================================================
五、API 接口一览
================================================================================

所有接口需登录后携带 Bearer Token 访问 (除登录接口外)。
基础路径: http://<服务器IP>:<端口>/api/

认证:
  POST /api/auth/login            登录获取 Token
  POST /api/auth/logout           注销当前会话

服务器:
  GET  /api/server/status        获取服务器状态
  GET  /api/server/icon           获取服务器图标
  POST /api/server/icon           上传服务器图标
  GET  /api/server/motd           获取 MOTD
  POST /api/server/motd           设置 MOTD
  POST /api/server/restart         重启服务器
  POST /api/server/stop            停止服务器

玩家:
  GET  /api/players               获取在线玩家列表
  POST /api/players/kick          踢出玩家
  POST /api/players/ban           封禁玩家
  POST /api/players/message       发送消息
  POST /api/players/gamemode      切换游戏模式
  POST /api/players/op            设置 OP 权限

白名单:
  GET  /api/whitelist              获取白名单
  POST /api/whitelist/toggle      开关白名单
  POST /api/whitelist/add          添加白名单成员
  POST /api/whitelist/remove      移除白名单成员

世界:
  POST /api/worlds/time           设置时间
  POST /api/worlds/weather         设置天气

控制台:
  POST /api/console               执行命令

权限 (LuckPerms):
  GET  /api/perms                 获取权限组列表
  POST /api/perms/group           创建权限组
  DELETE /api/perms/group/<name>  删除权限组
  POST /api/perms/group/<g>/perm  添加权限
  DELETE /api/perms/group/<g>/perm  移除权限
  GET  /api/perms/group/<g>/members  获取组成员
  GET  /api/perms/player/<p>      获取玩家权限
  POST /api/perms/player/<p>/add    加入权限组
  POST /api/perms/player/<p>/remove 离开权限组
  POST /api/perms/player/<p>/primary 设为主组

称号 (DeluxeTags):
  GET  /api/tags                  获取称号列表
  POST /api/tags                  保存称号
  DELETE /api/tags/<id>           删除称号
  POST /api/tags/chat             开关聊天显示
  GET  /api/tags/<id>/groups      获取称号关联组
  POST /api/tags/<id>/groups     设置称号关联组

TAB 列表:
  GET  /api/tab                   获取 TAB 配置
  POST /api/tab/header-footer     保存页眉页脚
  POST /api/tab/group             创建/更新分组
  DELETE /api/tab/group/<name>    删除分组
  GET  /api/tab/scoreboard        获取计分板配置
  POST /api/tab/scoreboard        保存计分板配置

PAPI 云拓展:
  GET  /api/papi/status           获取 PAPI 状态
  GET  /api/papi/expansions      浏览云端拓展
  GET  /api/papi/installed       获取已安装拓展
  GET  /api/papi/local           获取本地拓展
  POST /api/papi/install         安装拓展
  POST /api/papi/uninstall       卸载拓展
  POST /api/papi/refresh         刷新云端缓存

MiniMOTD:
  GET  /api/minimotd              获取 MOTD 配置
  POST /api/minimotd             保存 MOTD 行
  POST /api/minimotd/players     保存玩家数设置

多世界 (Multiverse-Core):
  GET  /api/multiverse             获取世界列表
  POST /api/multiverse/create      创建世界
  POST /api/multiverse/delete      删除世界
  POST /api/multiverse/import      导入世界
  POST /api/multiverse/property    修改世界属性

数据分析 (Plan):
  GET  /api/plan                   获取分析概要
  GET  /api/plan/url               获取 Plan Web 地址

基础功能 (EssentialsX):
  GET  /api/essentials/warps       获取 Warp 列表
  DELETE /api/essentials/warp/<n> 删除 Warp
  GET  /api/essentials/kits       获取 Kit 列表
  POST /api/essentials/kit        发放 Kit
  GET  /api/essentials/player/<p> 查询玩家信息
  POST /api/essentials/balance    设置余额
  POST /api/essentials/jail        切换 Jail 状态
  POST /api/essentials/mute        切换 Mute 状态

每日奖励 (DailyReward):
  GET  /api/dailyreward            获取奖励列表
  POST /api/dailyreward/save      保存奖励配置
  POST /api/dailyreward/reset     重置玩家领取记录
  POST /api/dailyreward/claim     强制发放奖励

插件检测:
  GET  /api/hooks                  获取所有插件可用性

配置:
  GET  /api/config                 获取面板配置


================================================================================
六、配置说明
================================================================================

配置文件位于 plugins/MCServerPanel/config.yml, 修改后使用 /panelreload 重载。

web:
  port: 8765                      # Web 服务监听端口
  host: "0.0.0.0"                  # 绑定地址 (0.0.0.0 = 公网可访问)

auth:
  password: "admin123"            # 登录密码 (请务必修改!)
  token-expire-hours: 24          # 令牌有效期 (小时)

security:
  require-auth: true              # 是否强制认证
  blocked-commands:               # 控制台命令黑名单
    - "stop"
    - "restart"
    - "reload"
    - "op"
    - "deop"

ui:
  theme: "system"                 # 默认主题 (light/dark/system)
  refresh-interval: 5             # 仪表盘自动刷新间隔 (秒)


================================================================================
七、游戏内命令
================================================================================

/panel                           打开面板信息
/panel reload                    重载面板配置
/panel status                    查看面板状态
/panel url                       查看面板访问地址
/panel password                  查看/修改密码
/panelreload                     重载面板配置 (快捷命令)

权限节点: mcpanel.admin (默认 OP 拥有)


================================================================================
八、构建与部署
================================================================================

环境要求:
  - JDK 21+
  - Maven 3.6+

构建步骤:
  cd mc-server-panel
  mvn clean package

构建产物:
  target/FluentMC-1.0.0.jar

部署步骤:
  1. 将 FluentMC-1.0.0.jar 放入服务器的 plugins/ 目录
  2. 启动服务器, 自动生成 plugins/MCServerPanel/config.yml
  3. 修改 config.yml 中的密码和端口
  4. 执行 /panelreload 重载配置
  5. 浏览器访问 http://<服务器IP>:<端口>

软依赖 (可选安装以获得更多功能):
  LuckPerms        - 权限组管理
  DeluxeTags       - 称号管理
  TAB              - Tab 列表/计分板
  PlaceholderAPI   - 变量云拓展
  MiniMOTD         - 渐变色 MOTD
  Multiverse-Core  - 多世界管理
  Plan             - 玩家数据分析
  Essentials       - 基础功能套件
  DailyReward      - 每日奖励


================================================================================
九、技术架构
================================================================================

后端:
  - Java 21 + Paper API 1.21.8
  - 内嵌 com.sun.net.httpserver.HttpServer (零外部依赖)
  - Gson (Paper 内置) 用于 JSON 序列化
  - 纯反射 Hook 架构集成可选插件
  - Token 认证 (UUID 令牌 + 过期管理)
  - BukkitScheduler 线程调度 (主线程安全)

前端:
  - 原生 HTML/CSS/JavaScript (无框架依赖)
  - WinUI 风格设计系统 (深色/浅色主题)
  - 响应式布局 (桌面/平板/手机适配)
  - 实时数据轮询 + WebSocket 式更新体验
  - MiniMessage 渲染预览
  - 动态侧边栏 (基于插件可用性)


================================================================================
十、安全机制
================================================================================

  - Token 认证: 所有 API 接口需携带 Bearer Token
  - 密码保护: 登录需配置密码, 默认 admin123 (建议修改)
  - 令牌过期: 可配置令牌有效期, 过期自动失效
  - 命令黑名单: 控制台接口过滤危险命令
  - 二次确认: 重启/停止/删除等危险操作需前端确认
  - 权限隔离: 仅 mcpanel.admin 权限可使用管理命令


================================================================================
                              FluentMC v1.0.0
                          Generated: 2026-08-19
================================================================================
