## 搭建教程
```
yum update -y
yum install -y curl vim wget unzip git
timedatectl set-timezone Asia/Shanghai
在PHP禁用函数一栏删除 system proc_open proc_get_status putenv
```

## Shell 上执行以下命令：
```
cd /www/wwwroot/你的文件夹名
git clone https://github.com/galaxychuck/ss-panel-v3-mod_UIChanges.git tmp && mv tmp/.git . && rm -rf tmp && git reset --hard
git config core.filemode false
wget https://getcomposer.org/installer -O composer.phar
php composer.phar
php composer.phar install
chmod -R 755 ${PWD}
chown -R www:www ${PWD}
ln -s ${PWD}/sql/glzjin_all.sql /www/backup/database/
```
在 伪静态 中填入下面内容：
```
location / {
    try_files $uri /index.php$is_args$args;
    }
```

导入初始数据库
点击删库塔菜单的 数据库 按钮，找到你刚 Link 的数据库，点击导入glzjin_all.sql


## Shell 上执行以下命令：
```
cd /www/wwwroot/你的文件夹名/
cp config/.config.example.php config/.config.php
cp config/appprofile.example.php config/appprofile.php
nano config/.config.php
```

## 创建管理员并同步用户
```
依次执行以下命令：
php xcat User createAdmin
php xcat User resetTraffic
php xcat Tool initQQWry
php xcat Tool initdownload
```

## 配置定时任务
```
执行 crontab -e 命令，添加以下四条：
30 22 * * * php /www/wwwroot/你的文件夹名/xcat SendDiaryMail
0 0 * * * php -n /www/wwwroot/你的文件夹名/xcat Job DailyJob
*/1 * * * * php /www/wwwroot/你的文件夹名/xcat Job CheckJob
*/1 * * * * php /www/wwwroot/你的文件夹名/xcat syncnode

30 22 * * * php /www/wwwroot/你的站点域名/xcat sendDiaryMail
0 0 * * * php -n /www/wwwroot/你的站点域名/xcat dailyjob
*/1 * * * * php /www/wwwroot/你的站点域名/xcat checkjob  
*/1 * * * * php /www/wwwroot/你的站点域名/xcat synclogin
*/1 * * * * php /www/wwwroot/你的站点域名/xcat syncvpn  
*/1 * * * * php -n /www/wwwroot/你的站点域名/xcat syncnas
```
