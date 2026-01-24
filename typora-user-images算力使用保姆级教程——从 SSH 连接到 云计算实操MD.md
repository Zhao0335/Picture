# 算力使用保姆级教程：从 SSH 连接到 云计算实操

整理人：赵晨旭		时间：2026/1/23

## 引言



​	本文档是面向深度学习入门者的实操指南，核心目标是帮助新手打通 “远程服务器操作→系统基础指令→代码版本管理→AI 模型实操” 的全流程，解决从 “本地开发” 到 “远程高性能计算” 的衔接难题。文档整体遵循 “基础铺垫→工具应用→实操落地” 的逻辑，先教会远程连接服务器的核心方法，再补充 Linux 系统操作、Git 代码管理等必备技能，最后结合 VSCode 插件实现高效远程云计算（如 AI 模型训练），全程配套具体命令、操作步骤和避坑技巧，无需复杂前置知识即可上手。



为方便快速把握文档架构，以下是核心内容概览表，读者可以按需进行阅读：



| 章节 |             核心主题             |                           关键内容                           |
| :--: | :------------------------------: | :----------------------------------------------------------: |
|  一  |          远程连接服务器          | SSH 终端连接、VSCode Remote-SSH 插件连接、免密配置、常见问题解决 |
|  二  |        Linux 核心基础指令        | 目录操作（cd/ls/pwd）、文件操作（mkdir/touch/rm/cp/mv）、内容查看（cat/vim）、系统监控（top/nvidia-smi） |
|  三  |        Git 与 GitHub 操作        | Git 安装配置、本地仓库管理、远程仓库联动（推送 / 拉取）、冲突解决、VSCode 可视化操作 |
|  四  | 远程云计算实操 & VSCode 插件应用 | 远程模型训练流程、核心插件（Remote-SSH/GitLens/Python）用法、资源监控、避坑要点 |



一部分关于具体环境配置、具体实操过程中的教程，请见姊妹篇《深度学习保姆级入门教程》



## 目录

### 第一章：远程连接服务器

**必学*

1.1 SSH 连接（常用）

- 1.1.1 终端登录（基础操作）

- 1.1.2 VSCode Remote-SSH 插件连接（推荐）

  - 安装插件

  - 验证本地 SSH 环境

  - 打开远程连接面板

  - 添加 SSH 连接目标

  - 发起连接并验证

  - 确认连接成功

  - 断开连接

- 1.1.3 扩展教学：SSH 配置文件

  - 简化连接命令

  - 多服务器统一管理

  - 免密连接配置

  - 自定义连接规则

- 1.1.4 常见问题解决

  - 权限拒绝（Permission denied）

  - 连接超时（Connection timed out）

  - SSH 断开导致进程终止

1.2 Web UI 登录（有图形化界面，不推荐）

### 第二章：Linux 核心基础指令

**本章节用于进一步了解Linux指令。对于使用图形化界面或用VScode进行远程管理的读者，可暂时跳过*

2.1 前置知识：相对路径 vs 绝对路径

2.2 目录操作指令

- 2.2.1 cd 指令：切换目录
- 2.2.2 ls 指令：列出目录内容
- 2.2.3 pwd 指令：查看当前工作目录
- 2.2.4 mkdir / rmdir 指令：创建 / 删除目录

2.3 文件操作指令

- 2.3.1 touch 指令：创建空文件 / 修改时间
- 2.3.2 rm 指令：删除文件 / 目录
- 2.3.3 cp 指令：复制文件 / 目录
- 2.3.4 mv 指令：移动 / 重命名文件 / 目录

2.4 内容查看与编辑指令

- 2.4.1 cat 指令：查看 / 拼接文件内容
- 2.4.2 vim 指令：终端文本编辑器（仅供了解）

2.5 数据流控制指令

- 2.5.1 redir 指令：重定向 / 管道辅助工具（简要说明）

2.6 系统监控常用指令（简要了解）

- top：实时监控 CPU / 内存
- df -h：查看磁盘使用情况
- nvidia-smi：查看 GPU 信息
- free -h：查看内存 / 交换分区使用
- ps -ef：查看所有运行进程

### 第三章：Git 与 GitHub 操作

**必须了解，但具体指令可以按需跳过阅读，直接使用VScode进行管理*

3.1 Git 安装（不同系统）

- 3.1.1 Ubuntu/Debian（Linux 服务器）
- 3.1.2 Windows 系统
- 3.1.3 Mac 系统

3.2 Git 初始化配置

3.3 本地仓库核心操作

- 3.3.1 创建本地仓库（git init）
- 3.3.2 添加文件与提交修改（git add/git commit）
- 3.3.3 辅助指令（查看历史、撤销操作、版本回滚）

3.4 远程仓库联动（与 GitHub 互通）

- 3.4.1 GitHub 远程仓库创建
- 3.4.2 本地仓库关联远程仓库（git remote add）
- 3.4.3 本地代码推送到 GitHub（git push）
- 3.4.4 从 GitHub 拉取代码（git clone/git pull）
- 3.4.5 推送冲突解决

3.5 Git 避坑小技巧

3.6 补充重点：VSCode 可视化管理 Git/GitHub

- 3.6.1 前期准备
- 3.6.2 VSCode 绑定 GitHub 账号（HTTPS/SSH 协议）
- 3.6.3 VSCode 中 Git 核心操作（初始化、暂存、提交、查看日志）

### 第四章：远程云计算实操 & VSCode 插件高效应用

**该章节为简要介绍，详细操作见姊妹篇《深度学习保姆级入门教程》*

4.1 远程云计算核心逻辑

4.2 远程云计算实操步骤（以跑 AI 模型为例）

- 4.2.1 SSH 连接远程服务器
- 4.2.2 服务器环境与代码准备
- 4.2.3 运行代码与资源监
- 4.2.4 训练结果拉回本地

4.3 VSCode 核心插件应用

- 4.3.1 Remote-SSH（远程连接核心）
- 4.3.2 GitLens（Git 增强）
- 4.3.3 Python（Python 开发必备）
- 4.3.4 Code Runner（快速运行代码）
- 4.3.5 NVIDIA GPU Monitor（GPU 监控）

4.4 远程云计算避坑要点



## 第一章：远程连接服务器

**引入**

我们平时用电脑习惯了鼠标点图标、开窗口的图形界面，但远程操控服务器时，这种方式特别耗流量和性能——就像视频通话比发文字费网一样，所以服务器操作大多用“终端”（即“Terminal”，类似Windows的命令提示符、Linux的bash）输命令。本文讲带着大家手把手的从SSH远程服务器，避免这些不必要的开销。

### 1.1 SSH连接（只有终端界面，常用）

 **SSH（Secure Shell）** 是一种加密的网络传输协议，用于在不安全的网络中为网络服务提供安全的传输环境，是远程登录Linux服务器最常用的方式。

#### 1.1.1 用终端登录（基础操作，不推荐）

*Windows，Mac，Linux操作相同*

- 基本语法：`ssh [用户名]@[服务器IP地址]`

示例：`ssh root@192.168.1.100`

- 首先我们先打开自己电脑的终端，然后我们可以在命令行里输入`ssh [用户名]@[服务器IP地址]` 进行连接。首次连接时会提示验证服务器指纹，输入`yes`后按回车，再输入服务器对应用户名的密码即可登录。在输入过程中发现自己看不到输入的密码很正常，这是一种保护机制——避免别人从你屏幕上看到密码长度或内容。输完密码后，直接按回车就行，系统会自动验证你输入的内容是否正确。如果密码错误，重新输入，再按上面的步骤来一次就好啦～
- 若服务器SSH端口非默认22，需指定端口：`ssh -p [端口号] [用户名]@[服务器IP地址]`

示例：![image-20260122174107256](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260122174107256.png)

#### 1.1.2 其他方法：这里以用Remote-SSH连接服务器为例

1. **安装Remote-SSH插件**：
       打开VS Code，点击左侧菜单栏“扩展”，或按快捷键 **Ctrl+Shift+X**。

   ![联想截图_20260122220331](C:\Users\Lenovo\Pictures\联想截图\联想截图_20260122220331.jpg)

2. **验证本地SSH环境**（可选）：
       Windows系统：打开VS Code内置终端（Ctrl+\`），输入`ssh -V`，若显示版本信息则正常；若无，需开启系统内置OpenSSH（设置→应用→可选功能→添加功能，搜索“OpenSSH客户端”安装）。

   ​    Mac/Linux系统：自带SSH客户端，直接在终端输入 `ssh -V` 即可验证.

   ![image-20260122221020070](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260122221020070.png)

3. **打开远程连接面板的方法**

   方式1：点击VS Code左下角绿色状态栏图标（显示“Open a Remote Window”，中文“打开远程窗口”）。

   ​								![image-20260122224832670](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260122224832670.png)

   方式2：点击左侧“远程资源管理器”→“SSH Targets”→右上角“+”号。

   ![image-20260122231524704](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260122231524704.png)

   

   4.**添加 SSH 连接目标**

   点击 “+” 号后，VS Code 的内置终端会弹出输入框，提示 “Enter SSH connection command”（输入 SSH 连接命令），你需要在这里输入适配服务器的 SSH 命令：

   - 若服务器 SSH 端口为默认 22：直接输入 `ssh [用户名]@[服务器IP地址]`

   - 若服务器 SSH 端口非默认：输入 `ssh -p [端口号] [用户名]@[服务器IP地址]`

     ![image-20260123010920365](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260123010920365.png)

   输入完成按回车后，会提示选择 SSH 配置文件的保存路径：

   - Mac/Linux 系统：默认路径是 `/Users/你的用户名/.ssh/config`，直接按回车确认即可；

   - Windows 系统：默认路径是 

     ```
     C:\Users\你的用户名\.ssh\config
     ```

     ，同样直接回车确认。

     ![image-20260123011040251](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260123011040251.png)

     这一步会把你的连接信息保存到配置文件，后续无需重复输入完整命令。

   5.**发起服务器连接并验证**

   1. 回到 VS Code 左侧的 “SSH Targets” 面板，能看到刚添加的服务器地址，鼠标移到该地址上，右键会出现 “在当前窗口连接主机” 的箭头图标，点击它；

   2. 首次连接时，VS Code 会弹出提示让你选择服务器操作系统类型，直接选**Linux**即可；

      ![image-20260123012506920](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260123012506920.png)

   3. 接着会弹出服务器指纹验证提示（和终端登录逻辑一致），点击 “Continue”（继续）确认信任该服务器；

   4. 随后 VS Code 的终端面板会弹出密码输入框，提示 “Enter password for [用户名]@[服务器 IP]”，输入服务器对应用户名的密码（输入时看不到任何字符是正常的安全保护机制），输完按回车。

      ![image-20260123012537591](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260123012537591.png)

   6.**确认连接成功**

   - 密码验证通过后，VS Code 会自动下载并安装服务器端的 Remote-SSH 组件（首次连接耗时约 10-30 秒，耐心等待即可）；
   - 连接成功的标志：VS Code 窗口标题会显示 `[SSH: 服务器IP]`，左下角绿色状态栏会显示 `SSH: 服务器IP`；
   - 此时你可以点击左侧 “资源管理器”→“打开文件夹”，选择服务器上的任意目录（比如 `/root` 或 `/home/你的用户名`），就能像操作本地文件一样编辑服务器文件，也能打开内置终端执行 Linux 命令。

   7.**断开连接**

   ![image-20260123012022792](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260123012022792.png)

   #### 1.1.3  扩展教学：配置文件（选择性学习）

   简单来说，SSH 配置文件就是一个 **“SSH 连接的快捷方式 + 个性化规则管理器”** —— 它把你每次连接服务器需要输入的 IP、端口、用户名、私钥路径等参数提前保存好，不用每次手动敲冗长的命令，还能统一管理多台服务器的连接规则。1. 最核心：简化连接命令，告别记复杂参数

   原本你连接服务器需要输完整命令，比如：

   ```bash
   ssh -p 2222 root@192.168.1.100  # 非默认端口的情况
   ```

   如果把这些参数写进配置文件，只需要给服务器起个 “别名”（比如`myserver`），之后无论在终端还是 VS Code 里，只用输`ssh myserver`就能连接，完全不用记 IP、端口、用户名。

   **配置示例**（打开`.ssh/config`文件添加以下内容）：
   *注：Linux和Mac一般为 ~/.ssh/config；Windows一般为C:\Users\你的用户名\\.ssh\config*
   
   ```bash
   # 给服务器起别名：myserver
   Host myserver
     HostName 192.168.1.100  # 服务器实际IP
     User root               # 登录用户名
     Port 2222               # SSH端口（默认22可省略）
   ```
   
   保存后，终端输入`ssh myserver`就能直接连接；VS Code 的 “SSH Targets” 面板也会显示`myserver`这个别名，点击就能连，不用再手动输入 IP / 端口。
   
   ##### 统一管理多台服务器，避免混乱
   
   如果你的工作中需要连接多台服务器（比如测试服务器、生产服务器、开发服务器），每台的 IP、端口、用户名可能都不一样，记起来很麻烦。
   
   配置文件可以把所有服务器的信息集中管理，一目了然，比如：
   
   ```json
   # 测试服务器
   Host test-server
     HostName 192.168.1.101
     User admin
     Port 22
   
   # 生产服务器
   Host prod-server
     HostName 10.0.0.5
     User ops
     Port 2223
   
   # 开发服务器
   Host dev-server
     HostName 172.16.0.8
     User developer
     Port 22
   ```
   
   之后连接任意服务器，只用输`ssh test-server`/`ssh prod-server`，VS Code 面板里也会按别名分类显示，不用再翻找服务器信息。
   
   **免密连接配置**
   
   免密连接的核心是**本地生成 SSH 密钥→公钥上传服务器→配置 config 指向私钥**
   
   1. 本地生成密钥（终端执行）
   
   ```bash
   ssh-keygen -t ed25519
   ```
   
   *注：在这里 -t 是 type 的意思，表示选择密钥算法，其中“ed25519”指的是一种密钥算法。*
   
   *有时我们也会添加注释信息：用 `-C` 参数加标签，比如 `-C "ubuntu-server-2026"`，方便区分多组密钥*
   
   示例：*Linux/Mac/Windows 操作相同*
   
   ![image-20260123192152154](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260123192152154.png)
   
   2. 公钥传到服务器（替换成你的信息）
   
      **方法 1：一键部署（macOS/Linux）**
   
      ```bash
      ssh-copy-id -i ~/.ssh/id_ed25519.pub [用户名]@[服务器IP地址] 
      ```
   
      最后输入一次密码后，自动完成公钥写入、权限设置，最省事。
   
      **方法 2：手动上传（Windows / 无 ssh-copy-id）**
   
      1. 本地复制公钥：cat ~/.ssh/id_ed25519.pub → 复制输出内容
   
         ![image-20260123194822748](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260123194822748.png)
   
      2. 登录服务器：ssh -p [端口号] [用户名]@[服务器IP地址]（输密码）
   
         ![image-20260123194849036](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260123194849036.png)
   
      3. 服务器操作：
   
      ```bash
      mkdir -p ~/.ssh && chmod 700 ~/.ssh
      echo "粘贴公钥内容" >> ~/.ssh/authorized_keys
      chmod 600 ~/.ssh/authorized_keys  # 权限错误会导致免密失败
      exit
      ```
   
   ![image-20260123195404793](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260123195404793.png)
   
   ​	在完成上述操作后，每次登录就不用重复输入密码了。
   
   ##### 自定义连接规则，适配特殊需求
   
   除了基础的连接参数，配置文件还能设置很多个性化规则，让连接更稳定、更贴合你的使用习惯，这些规则会自动生效，不用每次加命令行参数：
   
   - 指定非默认私钥文件（比如你生成的密钥不是默认路径）
   
     ```json
     Host myserver
       HostName 192.168.1.100
       User root
       IdentityFile ~/.ssh/my_custom_key  # 自定义私钥路径
     ```
   
   - 保持连接存活（避免长时间不操作断开）：
   
     ```json
     Host *  # 对所有服务器生效
       ServerAliveInterval 30  # 每30秒发一次心跳包，保持连接
     ```
   
   - 首次连接不弹指纹验证提示（简化操作）：
   
     ```json
     Host myserver
       HostName 192.168.1.100
       User root
       StrictHostKeyChecking no  # 跳过首次指纹验证
     ```
   

#### 1.1.4 常见问题解决

1. 输入密码后提示 “Permission denied”（权限拒绝）：

   - 核对用户名是否正确（比如部分服务器禁用 root 账户 SSH 登录，需用普通账户）；
   - 检查密码是否输入错误（Linux 系统密码严格区分大小写）；
   - 确认连接命令中的端口号是否和服务器实际 SSH 端口一致。

2. 提示 “Connection timed out”（连接超时）：

   - 先验证服务器 IP 是否正确、服务器是否开机且联网；
   - 检查服务器防火墙 / 安全组是否放行 SSH 端口（默认 22，非默认则放行对应端口）；
   - 本地终端输入 `ping 服务器IP`，能收到回复说明网络通路正常，收不到则排查网络问题。

3. **SSH 连接退出（断开）后，远程服务器上正在运行的模型训练进程也跟着终止：**

   核心问题：SSH 会话关闭（退出 / 断网）时，系统会向该会话下的所有进程发送 `SIGHUP`（挂起）信号，进程收到这个信号后就会终止运行。解决思路是让模型进程**脱离当前 SSH 会话**，不受会话关闭的影响。

   - 方法 1：nohup 
      nohup（即**no** **h**ang **up**）的核心作用就是让进程忽略`SIGHUP`信号，即使 SSH 断开也能后台持续运行。

     ```bash
     nohup 你的模型运行命令 > 日志文件名.log 2>&1 &
     ```

     - `nohup`：核心指令，保护进程不被挂起信号终止；

     - `>`：将命令的正常输出写入指定日志文件（避免输出丢失）；

     - `2>&1`：将错误输出也重定向到同一个日志文件（方便排查报错）；

     - `&`：让进程在后台运行，不占用当前终端。

     - 补充操作：

       - 查看进程是否在运行：

       ```bash
       ps aux | grep train.py  # 找到进程ID（PID），确认是否存活
       ```

       - 实时查看训练日志：

         ```bash
         tail -f train_model.log  # 实时刷新日志内容，按Ctrl+C退出查看
         ```

       - 手动终止进程（如需停止训练）：

         ```bash
         kill -9 进程ID  # 替换为ps查到的PID
         ```

   - 方法 2 : tmux

     tmux 的本质是终端多路复用器（Terminal Multiplexer），它允许你在一个终端窗口中管理多个会话、窗口和面板，并且能在断开连接后保持进程运行，非常适合长期管理远程进程。

     1. 安装:

        ```bash
        # Ubuntu/Debian
        sudo apt install tmux -y
        # CentOS/RHEL
        sudo dnf install tmux -y
        ```

        如图：

        ![image-20260123225918357](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260123225918357.png)

     2. 核心操作步骤：

        1. 创建新会话：

           ```bash
           tmux new -s model_train  # -s 指定会话名
           ```

           回车后，进入新的会话界面。示例：![image-20260123225947303](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260123225947303.png)
        
   
   ![image-20260123230155039](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260123230155039.png)
   
2. 运行模型命令（和正常操作一样）：
        
   ```bash
           python train.py
   ```
   
3. 分离会话（仍然保留进程）：按快捷键 `Ctrl + B` 松开，再按 `D`。
        
   ![image-20260123230010638](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260123230010638.png)
   
4. 重新连接会话：
        
   ```bash
           tmux attach -t model_train  # -t 指定会话名
   # 查看所有会话：tmux ls
   ```

        5. 关闭会话：
        
           进入会话后输入`exit`，或：
   
   ```bash
           tmux kill-session -t model_train # -t 指定会话名
   ```
   
   检查是否关闭会话：![image-20260123230409233](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260123230409233.png)

### 1.2  Web UI 登录（有图形化界面，不推荐）

通过 **URL 访问网页界面** 登录，按访问场景（校内、工创中心内、校外）提供了不同的 HTTP/HTTPS 地址，且明确关联 “Realm（领域）: Proxmox VE authenticator”（Proxmox VE 专属身份验证领域）

- 直接连接网站![image-20260124000741910](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260124000741910.png)

- 输入账号密码![image-20260122232003878](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260122232003878.png)






## 第二章：Linux核心基础指令（选择性学习）

**引入**

为了让我们能够在使用 Linux 终端的时候也能游刃有余，我们需要掌握以下指令。掌握这些指令，就能灵活操作服务器文件和系统。

注：实际上我们在这里主要是装上 VScode 的插件后直接在 VScode里 面操作（如**第四步**所示），以下指令可以选择性学习。

### 2.1 前置知识：相对路径 vs 绝对路径

- 相对路径：从你当前所在的“位置”（当前目录）出发的路线；

- 绝对路径：从“根目录”（Linux的`/`）开始的完整地址；

如图1.1 ：

![image-20260122174338981](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260122174338981.png)

​													图1.1

白色的 “ (base) ” 是目前所使用的 Conda 环境，详情请看《深度学习保姆级入门教程》；

蓝色的 “~”、“~/Documents”、“~/Documents/document1” 都表示 “当前目录” ；

关于 “cd”，“ls”，“mkdir”等等常用的Linux指令，我们会在接下来展开讲解。

**核心内容**：

```bash
ls [选项/目录] # 列出文件或目录内容  
cd [目标目录] # 切换工作目录 
pwd # 显示当前工作目录完整路径 
mkdir [目录名] # 创建新目录 
rm -rf [文件/目录] # 强制删除文件或目录（慎用） 
cp [源文件] [目标路径] # 复制文件 / 目录 
mv [源文件] [目标路径] # 移动 / 重命名文件 / 目录 
cat [文件名] # 查看文件全部内容 
grep [关键词] [文件名] # 在文件中搜索关键词 
sudo [命令] # 以管理员权限执行命令 
ssh [用户名@服务器IP] # 远程登录服务器 
tar -zxvf [压缩包名.tar.gz] # 解压 tar.gz 格式压缩包 
top # 实时监控系统资源和进程 
man [命令] # 查看命令的详细帮助手册
```

### 2.2 目录操作指令

#### 2.2.1 cd 指令 —— 切换目录

cd 即 **C**hange **D**irectory，用于切换当前工作目录，是Linux终端最常用的指令之一。

- 进入当前目录下的指定文件夹：`cd [文件夹名]`

![image-20260122233136651](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260122233136651.png)



- 进入绝对路径指定的文件夹：`cd [绝对路径]`

![image-20260122233612702](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260122233612702.png)



- 返回上级目录：`cd ..`

![image-20260122233350555](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260122233350555.png)



- 返回当前用户的主目录（家目录）：`cd ~` 或直接`cd`

![image-20260122233424827](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260122233424827.png)



- 返回上一次所在的目录：`cd -`![image-20260122233749507](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260122233749507.png)

​													



#### 2.2.2 ls 指令 —— 列出目录内容

ls 即 **L**i**s**t，用于查看当前目录或指定目录下的文件和文件夹。

**常用用法**

- 基础用法：`ls` —— 列出当前目录的可见文件/文件夹（不显示隐藏文件）。

- 列出详细信息（权限、所有者、大小、修改时间等）：`ls -l`（**l**ong长格式）

- 显示隐藏文件（Linux中以`.`开头的文件为隐藏文件）：`ls -a`（**a**ll）
- 组合使用：`ls -la` —— 列出所有文件（含隐藏）的详细信息

![image-20260122235726789](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260122235726789.png)





#### 2.2.3 pwd 指令 —— 查看当前工作目录

pwd 即 **P**rint **W**orking **D**irectory，用于输出当前所在目录的绝对路径，解决“不知道自己在哪”的问题。

![image-20260122235923645](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260122235923645.png)





#### 2.2.4 mkdir 指令 —— 创建目录

mkdir 即 **M**a**k**e **Dir**ectory，用于创建新的文件夹。

- 基础用法：`mkdir [文件夹名]`

![image-20260123101516138](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260123101516138.png)



- 递归创建多级目录（父目录不存在时自动创建）：`mkdir -p [多级路径]`

​	如图所示 当创建`test/test1/test2` 前 `test1`尚不存在，会自动创建test1

![image-20260123101639475](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260123101639475.png)

​										

- 创建多个目录：`mkdir [目录1] [目录2]`

![image-20260123101928447](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260123101928447.png)

​													

- **rmdir** 指令——删除目录

  用法同理



### 2.3 文件操作指令

#### 2.3.1 touch 指令 —— 创建空文件

touch 指令主要用于创建空文件，也可修改文件的访问/修改时间（若文件已存在）。

- 基础用法：`touch [文件名]` —— 创建空文件（若文件不存在）；若文件已存在，更新其修改时间。

示例：当前在`/home/user`，执行`touch test.txt`，会创建空的`test.txt`文件；若该文件已存在，会把文件的修改时间更新为当前时间，不会修改文件内容。



- 创建多个空文件：`touch [文件1] [文件2]`

![image-20260123200231810](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260123200231810.png)



- 指定文件的修改时间：`touch -t [时间格式] [文件名]`
  ![image-20260123200417964](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260123200417964.png)



#### 2.3.2 rm 指令 —— 删除文件/目录

rm 即 **R**e**m**ove，用于删除文件或目录，使用时需谨慎（Linux无回收站，删除后难恢复）。

- 删除文件：`rm [文件名]`

![image-20260123201838537](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260123201838537.png)



- 强制删除文件（无确认提示）：`rm -f [文件名]`

示例：`rm -f test.txt`，即使文件为只读权限，也会直接删除，无任何确认提示。

- 删除空目录：`rm -d [目录名]`

`rm -d empty_dir`，仅能删除空的`empty_dir`目录，若目录有内容会报错。
![image-20260123202226574](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260123202226574.png)

- 删除目录（需加`-r`递归删除）：`rm -r [目录名]`

![image-20260123202125215](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260123202125215.png)

- 强制删除目录（无确认提示）：`rm -rf [目录名]`

例：`rm -rf test`，直接删除`test`目录及所有内容，无任何提示，**务必谨慎使用**（避免误删系统文件）。



#### 2.3.2 cp 指令 —— 复制文件/目录

cp 即 **C**o**p**y，用于复制文件或目录。

- 复制文件：`cp [源文件路径] [目标路径]`

示例：`cp test.txt Documents/test1/test2` —— 将当前目录的`test.txt`复制到`Documents/test1/test2`目录；

​	若目标路径是文件名（如`cp test.txt Documents/test1/test2/new_test.txt`），会复制并改名。
![image-20260123202746687](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260123202746687.png)

- 复制多个文件到同一目录：`cp [文件1] [文件2] [目标目录]`

示例：`cp file1.txt file2.log /home/user/backup`，将`file1.txt`和`file2.log`同时复制到`backup`目录。

- 复制目录（需加`-r`递归）：`cp -r [源目录路径] [目标路径]`

示例：`cp -r test /home/user/backup` —— 将`test`目录及所有内容复制到`/home/user/backup`，生成`/home/user/backup/test`。

- 复制时保留文件属性（权限、时间等）：`cp -p [源文件] [目标路径]`

示例：`cp -p test.txt /home/user/backup`，复制后`test.txt`的权限、修改时间与原文件一致。



#### 2.3.3 mv 指令 —— 移动/重命名文件/目录

mv 即 **M**o**v**e，可用于移动文件/目录，也可用于重命名，是Linux中高频使用的指令之一。

- 重命名文件/目录：`mv [原名称] [新名称]`

示例1（重命名文件）：`mv test.txt new_test.txt` —— 将当前目录的`test.txt`重命名为`new_test.txt`；

示例2（重命名目录）：`mv test new_test` —— 将当前目录的`test`目录重命名为`new_test`。
![image-20260123203141152](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260123203141152.png)



- 移动文件/目录到指定路径：`mv [源路径] [目标路径]`

示例1（移动文件）：`mv test.txt /home/user/backup` —— 将当前目录的`test.txt`移动到`/home/user/backup`目录；

示例2（移动目录）：`mv test /home/user/backup` —— 将当前目录的`test`目录移动到`/home/user/backup`目录。

![image-20260123203701518](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260123203701518.png)



- 强制移动（覆盖目标同名文件无提示）：`mv -f [源路径] [目标路径]`

示例：`mv -f test.txt /home/user/backup`，若`backup`目录已有`test.txt`，会直接覆盖，无确认提示。

- 移动时提示覆盖（安全模式）：`mv -i [源路径] [目标路径]`

示例：`mv -i test.txt /home/user/backup`，若目标路径有同名文件，会提示`是否覆盖？`，输入`y`才会覆盖。

![image-20260123203823371](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260123203823371.png)



### 2.4 内容查看与编辑指令

#### 2.4.1 cat 指令 —— 查看/拼接文件内容

cat 即 **Cat**enate（拼接），核心用于查看文件内容，也可拼接多个文件、创建新文件。

- 查看单个文件内容：`cat [文件名]`

示例：`cat test.txt`，会在终端直接输出`test.txt`里的所有内容（适合小文件，大文件建议用`less`/`more`）。



- 查看多个文件内容（按顺序拼接输出）：`cat [文件1] [文件2]`

示例：`cat file1.txt file2.txt`，会先输出`file1.txt`的内容，再输出`file2.txt`的内容。

![image-20260123204331480](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260123204331480.png)



- 查看文件内容并显示行号：`cat -n [文件名]`

示例：`cat -n test.txt`，输出内容时每行开头会显示行号。
![image-20260123204656026](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260123204656026.png)



- 创建新文件并写入内容（按`Ctrl+D`结束输入）：`cat > [新文件名]`

示例：执行`cat > new.txt`后，终端进入输入模式，输入`hello linux`，按`Ctrl+D`会保存内容并创建`new.txt`。



- 追加内容到已有文件：`cat >> [文件名]`

示例：`cat >> test.txt`，输入`new line`后按`Ctrl+D`，会把`new line`追加到`test.txt`的末尾（不会覆盖原有内容）。





#### 2.4.2 vim 指令 —— 终端文本编辑器（仅供了解）

*这个部分无配图演示，目前我们建议使用其他容易上手的编辑器，如 VScode。如果感兴趣可以在之后自己了解。* 



vim 是Linux终端中功能强大的文本编辑器（vi的增强版），可用于编辑代码、配置文件等，无需图形界面。



##### 核心操作：vim的三种模式

- **普通模式**：打开文件后默认进入，用于移动光标、复制/删除内容（按`Esc`可切回此模式）；

- **插入模式**：用于输入文字，按`i`/`a`/`o`可进入（`i`=光标前插入，`a`=光标后插入，`o`=光标下一行插入）；

- **命令行模式**：按`:`进入，用于保存、退出、查找替换等操作。

  

##### 常用用法 

- 打开/创建文件：`vim [文件名]`

示例：`vim test.txt`，若`test.txt`存在则打开，不存在则创建并打开。

- 插入模式操作：

打开文件后按`i`进入插入模式，即可像记事本一样输入文字（如`print("hello linux")`）。

- 普通模式常用操作：
  - 移动光标：`↑↓←→`方向键（或`h/j/k/l`对应左/下/上/右）；
  - 复制行：`yy`（复制当前行）、`3yy`（复制当前行及以下2行，共3行）；
  - 粘贴：`p`（粘贴到光标下一行）；
  - 删除行：`dd`（删除当前行）、`3dd`（删除当前行及以下2行）；
  - 撤销操作：`u`；
- 命令行模式常用操作（先按`Esc`切回普通模式，再按`:`）：
  - 保存文件：`:w`（仅保存，不退出）；
  - 退出vim：`:q`（文件未修改时）；
  - 保存并退出：`:wq`（或`:x`）；
  - 强制退出（不保存修改）：`:q!`；
  - 查找内容：`:/关键词`（如`:/linux`，按`n`找下一个，`N`找上一个）。





### 2.5 数据流控制指令

#### 2.5.1 redir 指令 —— 重定向/管道辅助工具

*这里不做详细演示*

redir 用于处理命令的输入/输出重定向、管道传输，是Linux中“数据流控制”的核心工具，常与`>`/`>>`/`<`/`|`配合使用。

- 标准输出重定向（覆盖文件）：`[命令] > [文件]`

示例：`ls -la > dir_list.txt`，将`ls -la`的输出内容覆盖写入`dir_list.txt`（文件原有内容会被清空）。

- 标准输出追加重定向：`[命令] >> [文件]`

示例：`echo "new line" >> dir_list.txt`，将`echo`输出的`new line`追加到`dir_list.txt`末尾（保留原有内容）。

- 标准输入重定向：`[命令] < [文件]`

示例：`cat < test.txt`，等价于`cat test.txt`；`wc -l < test.txt`，统计`test.txt`的行数。

- 错误输出重定向（捕获错误信息）：`[命令] 2> [错误文件]`

示例：`rm non_exist_file 2> error.log`，将`rm`删除不存在文件的错误提示写入`error.log`。

- 混合输出重定向（正常+错误信息都写入）：`[命令] > [文件] 2>&1`

示例：`python test.py > run.log 2>&1`，将`test.py`运行的正常输出和错误信息都写入`run.log`。

- 管道传输（将一个命令的输出作为另一个命令的输入）：`[命令1] | [命令2]`

示例：`ls -la | grep ".txt"`，将`ls -la`的输出传给`grep`，只显示包含`.txt`的行；`cat test.txt | wc -l`，统计`test.txt`的行数。







### 2.6 系统监控常用指令（后续在进行环境配置等活动会用到）

```Bash
top          # 实时查看CPU、内存占用（按q退出）
df -h        # 查看磁盘使用情况（-h=人性化显示大小，如GB/MB）
nvidia-smi   # 查看GPU信息（有GPU才有用，后续跑模型会用到）
free -h      # 查看内存/交换分区使用情况
ps -ef       # 查看所有运行的进程
```







## 第三步：Git与GitHub操作（需要了解）

*这里关于 终端使用 git 的操作仅提供文字描述，这里认为可以先看该节的补充重点，快速实现更简单的管理操作*

**引入**

Git是**本地代码版本控制工具**，可以记录代码的每一次修改、回滚错误版本；GitHub是**远程代码托管平台**，可以把本地代码上传保存，方便多人协作、跨设备开发，还能下载别人的开源项目（比如AI模型代码）。

推荐视频：【【GeekHour】一小时Git教程】https://www.bilibili.com/video/BV1HM411377j?vd_source=11bbb301f9897551c0ba0d129acd9dfd



### 3.1 先装Git（不同系统安装方法）

- **Ubuntu/Debian（Linux服务器）**：

  - ```Bash
    sudo apt update  # 更新软件源（先做这步避免安装失败）
    sudo apt install git -y  # 安装Git，-y表示自动确认
    ```

- **Windows**：

去Git官网（https://git-scm.com/）下载安装包，一路默认下一步即可（记得勾选“Add Git to PATH”，方便终端调用）。

- **Mac**：

方法1：`brew install git`（需先装Homebrew）；

方法2：App Store装Xcode，自带Git。





### 3.2 Git初始化配置

安装后第一步要配置“身份信息”，让Git知道“谁在修改代码”：

```Bash
# 配置用户名（建议替换成你的GitHub用户名）
git config --global user.name "YourGitHubName"
# 配置邮箱（建议替换成你的GitHub绑定邮箱）
git config --global user.email "your_email@xxx.com"
# 验证配置是否成功（会输出你刚配置的信息）
git config --list
```

- `--global`：表示全局配置，所有本地Git仓库都会用这个身份；如果想给单个仓库配不同身份，去掉`--global`，进入仓库目录再执行。



### 3.3 本地仓库核心操作

“本地仓库”就是你电脑里的一个文件夹，被Git管理起来，能记录代码修改记录。

#### 步骤1：创建本地仓库（把文件夹变成Git可管理的）

```Bash
# 1. 先创建一个文件夹
mkdir my_ai_project
# 2. 进入这个文件夹
cd my_ai_project
# 3. 初始化Git仓库（执行后会生成隐藏的.git文件夹）
git init
```

执行`git init`后，文件夹就变成了Git仓库，`.git`文件夹是Git的“账本”，记录所有修改，不要手动删！

#### 步骤2：添加文件&提交修改（记录代码变化）

假设你在`my_ai_project`里创建了`test.py`文件，现在要记录这个文件：

```Bash
# 1. 查看文件状态（红色表示“未跟踪”，即Git没记录）
git status
# 2. 把文件加入“暂存区”（准备提交，‘.’表示所有文件）
git add test.py  # 只加test.py
git add .       # 加当前目录所有修改/新增的文件（常用）
# 3. 再次查看状态（绿色表示“已暂存”，可以提交了）
git status
# 4. 提交到本地仓库（写清楚“做了什么”，必须加-m和说明）
git commit -m "新增test.py，写了hello linux代码"
```

- 提交说明要通俗（比如“修复test.py的语法错误”“新增AI模型训练代码”），方便后续找记录。
- 若忘记写`-m`，会自动打开vim编辑器，输入说明后按`Esc`+`:wq`保存退出即可。

#### 步骤3：常用辅助指令（查记录、撤销操作）

```Bash
# 查看提交历史（所有修改记录，按q退出）
git log  # 简洁版：git log --oneline
# 撤销暂存区的文件（比如加错了文件）
git reset HEAD test.py
# 撤销工作区的修改（恢复到上一次提交的状态，慎用！会丢未提交的修改）
git checkout -- test.py
# 回滚到某个版本（先git log找版本号，比如abc123）
git reset --hardabc123
```



### 3.4 远程仓库联动（和GitHub互通）

“远程仓库”就是GitHub上的仓库，能把本地代码传上去，也能拉下来别人的修改。

#### 步骤1：在GitHub创建远程仓库

1. 打开GitHub官网，登录后点击右上角“+”→“New repository”；
2. 填仓库名（比如和本地一致my_ai_project）；
3. 可选：加README（仓库说明）、选开源协议；
4. 点击“Create repository”，创建后会看到仓库的URL（比如https://github.com/[github用户名]/[仓库名].git）。

#### 步骤2：本地仓库关联远程仓库

回到本地终端，进入`my_ai_project`目录，执行：

```Bash
# 关联远程仓库（origin是远程仓库的别名，可自定义，默认用origin）
git remote add origin https://github.com/YourGitHubName/my_ai_project.git
# 验证关联是否成功（会输出远程仓库URL）
git remote -v
```

#### 步骤3：把本地代码推送到GitHub（第一次推送）

```Bash
# 第一次推送要加-u，把本地main分支和远程main分支绑定
git push -u origin main
# 后续推送不用加-u，直接：
# git push
```

- 推送时会弹登录验证：
  - 旧版Git：输GitHub用户名+密码（现在密码无效，要用PAT）；
  - 新版Git：推荐用PAT（个人访问令牌），创建方法：
    - GitHub右上角头像→Settings→Developer settings→Personal access tokens→Tokens (classic)；
    - 点击“Generate new token”，勾选`repo`权限（仓库相关），设置有效期；
    - 生成后复制令牌（只显示一次！存好），推送时密码栏填这个令牌即可。

#### 步骤4：从GitHub拉取代码（下载/更新）

```Bash
# 1. 克隆别人的仓库（下载整个项目到本地，第一次用）
git clone https://github.com/ultralytics/yolov5.git  # 比如克隆YOLOv5代码
# 2. 自己的仓库更新（拉取GitHub最新代码，多人协作必用）
cd my_ai_project  # 先进入仓库目录
git pull  # 拉取远程main分支的最新代码
```

#### 步骤5：解决简单的推送冲突（多人协作常见）

如果别人改了同一个文件并推送到GitHub，你再推送会失败，需要先拉取合并：

```Bash
# 1. 先拉取远程代码
git pull
# 2. 打开冲突文件（里面会有<<<<<<< HEAD、=======、>>>>>>> xxx标记）
# 3. 手动修改冲突部分（保留需要的代码，删掉标记）
# 4. 重新添加、提交、推送
git add .
git commit -m "解决冲突，合并代码"
git push
```



### 3.5 Git避坑小技巧

1. 不要把大文件（比如模型权重、视频）推到GitHub，会报错且慢，用Git LFS或网盘存；
2. 新建`.gitignore`文件，写要忽略的文件（比如`__pycache__/`、`*.log`、`venv/`），Git会自动跳过这些文件；
3. 提交前先`git status`看状态，避免漏加/错加文件；
4. 定期`git pull`拉取最新代码，减少冲突。



### 3.6 补充重点：借助 VScode 使用 git/github 管理仓库

#### 3.6.1 前期准备

 1. 安装 Git、VScode，注册了 github 账号；

 2. 配置 Git 身份同上 3.2 

    

#### 3.6.2 VScode 绑定 Github 账号

**方法1：HTTPS协议**

​	**触发 VSCode 登录流程**

​	打开 VSCode，按下快捷键 `Ctrl+Shift+P`（Windows/Linux）或 `Cmd+Shift+P`（Mac）唤起命令面	板，输入并选择 `GitHub: Sign in`。

​	**浏览器授权登录**

​	此时会自动弹出浏览器，跳转到 GitHub 的授权页面。登录你的 GitHub 账号后，点击授权按钮，允许 	VSCode 获取账号权限。

​	**处理登录验证（关键）**

​	由于 GitHub 已不再支持密码登录，首次推送 / 拉取仓库时，VSCode 会提示输入 “密码”，这里需要填	写**GitHub 个人访问令牌（Personal Access Token）**：

- 令牌获取路径：GitHub 官网 → 点击头像 → `Settings` → `Developer settings` → `Personal access tokens` → `Tokens (classic)` → 点击 `Generate new token (classic)`。

- 生成时需勾选 `repo` 等仓库相关权限，复制并保存好生成的令牌（仅显示一次）。

  验证绑定：回到 VSCode，若左下角状态栏显示你的 GitHub 用户名，或克隆 HTTPS 地址的仓库可正常拉取，即绑定成功。

**方法2：SSH协议**（更安全，推荐）
*此部分的内容和截图主要来自https://blog.csdn.net/qq_41923622/article/details/103207158*

​	**1. 创建公钥**——**复制公钥**
​	*注：详情与前面第一步--扩展部分--免密连接--生成公钥*
​		示例：（建议直接回车，不更改保存路径、密码等）

​	**2. 登录github账号**

​	点击 “Settings” 设置

 ![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/e4ae2c9698d469dab841b34e344edb60.png)

然后左侧菜单选中 SSH and GPG keys

![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/c32f4dddbe52b6fea49fb2ff13c952f9.png)

点新建 SSH key

![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/dd4ec68fe8db7cb1e4907a3350446147.png)

粘贴复制的内容

![在这里插入图片描述](https://i-blog.csdnimg.cn/blog_migrate/20938a092cbfd7965ba1319ae4e501e0.png)

最后点 add ssh key 就完成了 本地链接与远端仓库关联确认



#### 	3.6.3 VScode 中 Git 核心操作

#### 		![image-20260123213658551](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260123213658551.png)

这里我们主要讲VScode如何简化git操作，下面仅具几例：

1. 当我们打开了一个未初始化的文件夹时，我们可以直接点击 “初始化仓库” 进行`git init`

   ![image-20260123214122957](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260123214122957.png)

   2.可视化的状态`git status`；直接点击“+”，存放到暂存区`git add`；直接点击消息框和提交，进行`git commit`

   ![image-20260123214653059](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260123214653059.png)

   3. 可视化的`git log`

      ![image-20260123214829978](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20260123214829978.png)





## 第四章：远程云计算实操 & VSCode插件高效应用

**引入**

前面学了SSH连服务器、Linux指令、Git管理代码，现在结合这些做“远程云计算”（比如在服务器上跑AI模型、训练数据），VSCode插件能让这个过程更丝滑，更详细的教程见《深度学习保姆级入门教程》



### 4.1 远程云计算核心逻辑

远程云计算就是“用本地电脑操作远程服务器（有高性能CPU/GPU）”：

1. 本地通过SSH连接远程服务器（拿到服务器的“操作权”）；

2. 在服务器上用Linux指令管理文件、配置环境；

3. 用Git拉取/推送代码（本地写代码，服务器跑代码）；

4. 用VSCode插件简化操作，不用频繁切终端。

   



### 4.2 远程云计算实操步骤（跑AI模型为例）

#### 步骤1：SSH连接远程云计算服务器

用前面学的“Remote-SSH”方法连接服务器（推荐VSCode的Remote-SSH插件，图形化操作更简单）：

1. 确保服务器有GPU（执行`nvidia-smi`验证）；
2. VSCode打开Remote-SSH面板，输入`ssh 用户名@服务器IP`，连接成功后，VSCode状态栏会显示“SSH: 服务器IP”。

#### 步骤2：在服务器上准备环境&代码

```Bash
# 1. 安装Python/conda（跑AI模型必备）
sudo apt install python3 python3-pip
# 2. 克隆你的AI代码仓库（比如从GitHub拉）
git clone https://github.com/[用户名]/[仓库名.git]
# 3. 进入仓库，安装依赖
cd [仓库名]
pip install -r requirements.txt  # 假设你有依赖清单，详细的环境配置见Anaconda篇
```

#### 步骤3：运行代码&监控资源

```Bash
# 1. 运行模型训练代码
python train.py
# 2. 新开终端，监控GPU使用（实时看显存/利用率）
nvidia-smi -l 2  # 每2秒刷新一次
# 3. 监控CPU/内存（看是否资源不够）
top
```

#### 步骤4：把训练结果拉回本地

```Bash
# 方法1：服务器上用Git提交结果，本地拉取
# 服务器端：
cd my_ai_project
git add train_result/  # 把训练结果文件夹加入暂存
git commit -m "添加模型训练结果"
git push
# 本地端：
cd my_ai_project
git pull  # 拉取结果到本地

# 方法2：用scp指令（直接传文件）
scp 用户名@服务器IP:/home/用户名/my_ai_project/train_result/model.pth ./
```





### 4.3 VSCode插件在远程云计算中的妙用

#### 4.3.1 Remote-SSH（核心插件）

- 作用：直接在VSCode里操作远程服务器的文件/终端，不用单独开SSH终端；

- 进阶用法：
  - 打开服务器文件：连接后，点击“文件→打开文件夹”，选择服务器上的`my_ai_project`，就能像编辑本地文件一样改代码；
  
  - 内置终端：VSCode底部终端直接是服务器的终端，不用手动输SSH命令；
  
  - 保存自动同步：修改服务器文件后，按`Ctrl+S`直接保存到服务器，不用手动上传。
  
    

#### 4.3.2 GitLens（Git增强插件）

- 作用：可视化Git操作，不用记复杂指令；

- 用法：
  - 看每行代码的修改人/时间：鼠标移到代码行，会显示“谁在什么时候改的”；
  
  - 一键提交/推送：左侧Git面板能看到修改的文件，勾选后一键提交、推送，不用输`git add`/`git commit`；
  
  - 对比版本：右键文件→“GitLens→Compare with Previous Version”，直观看到代码修改差异。
  
    

#### 4.3.3 Python（Python开发必备）

- 作用：远程服务器上的Python代码调试、运行；

- 用法：
  - 配置解释器：按`Ctrl+Shift+P`，输入“Python: Select Interpreter”，选择服务器上的Python/conda环境；
  
  - 一键运行：打开`train.py`，右上角点击“运行按钮”，直接在服务器上运行代码；
  
  - 调试代码：加断点后，点击“调试按钮”，逐步执行代码，看变量/报错（比终端打印更直观）。
  
    

#### 4.3.4 Code Runner（快速运行代码）

- 作用：支持一键运行多种语言（Python/Shell/Java），不用手动输`python xxx.py`；

- 用法：在服务器上打开代码文件，右键→“Run Code”，直接运行，结果显示在VSCode终端。

  

#### 4.3.5 NVIDIA GPU Monitor（监控GPU）

- 作用：VSCode侧边栏直接显示服务器GPU使用率、显存占用，不用频繁输`nvidia-smi`；
- 用法：安装后，连接远程服务器，侧边栏会显示GPU信息，实时更新。





### 4.4 远程云计算避坑要点

1. 服务器连接超时：检查服务器是否开机、IP是否正确、端口是否开放（默认22）；
2. 代码运行卡顿：用`top`/`nvidia-smi`看资源，关掉没用的进程，或申请更高配置的服务器；
3. 依赖安装失败：服务器换国内源（比如pip用清华源`pip install -i https://pypi.tuna.tsinghua.edu.cn/simple xxx`）；
4. 大文件传输慢：用`rsync`指令（比scp快），或压缩后传输（`tar -zcvf result.tar.gz train_result/`）。
