## Git Submodule

- 常用命令

        git clone <repository> --recursive 递归的方式克隆整个项目
        git submodule add <repository> <path> 添加子模块
        git submodule init 初始化子模块
        git submodule update 更新子模块
        git submodule foreach git pull 拉取所有子模块
        
        # 备注: clone本地后 git pull 或者 git submodule foreach git pull 更新是没有指向分支需要 带 <repository> <branch>参数
        git pull origin master
        git submodule foreach git pull origin master

- Submodule的应用

        # 添加git repository子模块
        git submodule add http://172.16.75.12:3000/HiThink/ylh-v2.git src/assets
        
        # 查看结果
        git status
        
        Changes to be committed:
          (use "git reset HEAD <file>..." to unstage)
        
                new file:   .gitmodules
                new file:   src/assets
        备注:) src/assets 为 框架代码, submodule是不能在被依赖的应用中修改提交git服务器,只能在ylh-v2中修改提交

- Submodule的修改更新


> 情况一: 在主模块中修改时, 子模块先提交再提交主模块

        # 子模块
        git add .
        git commit -m "lib update"
        git push
        
        # 主模块中
        git add .
        git commit -m "lib update"
        git push

> 情况一: 在子模块中修改提交后, 主模块更新后提交

        # 主模块中
        git submodule foreach git pull
        git add .
        git commit -m "lib update"
        git push


- Submodule的项目clone

> 方法一(推荐): 采取递归克隆

        git clone http://172.16.75.12:3000/HiThink/ylh-v2-portal.git --recursive

        http://172.16.75.12:3000/HiThink/ylh-v2.git
        
> 方法二: 先clone父项目，再初始化Submodule

        # clone父项目
        git clone http://172.16.75.12:3000/HiThink/ylh-v2-portal.git
        cd src/assets
        
        # 子模块初始化
        git submodule init
        
        # 子模块更新
        git submodule update
        
        # 之后的更新
        git submodule foreach git pull 或
        git pull origin master