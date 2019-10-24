1. pm2(node进程管理工具)

   ```
   pm2 start app.js
   pm2 list
   pm2 monit
   pm2 reload all
   pm2 stop all
   NODE_ENV=value pm2 start app.js --update-env
   ```

   

2. n（node版本管理）

   ```shell
   // 安装某个版本
   n 0.8.14
   // 安装最新版本
   n lastest
   // 安装最新稳定版本
   n stable
   // 列出所有版本
   n ls
   // 选择已经安装版本
   n
   // 删除某个版本
   n rm xx.xx.x
   ```


3. forever

   ```shell
   // 环境变量
   NODE_ENV=staging forever start nantong.js
   forever list
   forever stopall
   forever restartall
   ```
   
   
   

