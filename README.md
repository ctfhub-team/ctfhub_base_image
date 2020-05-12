# CTFHUB 基础环境

## Summary

- Pwn
    - Native - [Example/Demo](https://github.com/ctfhub-team/challenge_bsidessf_2019_pwn_slowfire)
        - [x] [base_pwn_native_1604](https://github.com/ctfhub-team/base_pwn_native_1604)
        - [x] [base_pwn_native_1804](https://github.com/ctfhub-team/base_pwn_native_1804)
    - Xinetd - [Example/Demo](https://github.com/ctfhub-team/challenge_bctf_2018_pwn_begentle)    
        - [x] [base_pwn_xinetd_1604](https://github.com/ctfhub-team/base_pwn_xinetd_1604)
        - [x] [base_pwn_xinetd_1804](https://github.com/ctfhub-team/base_pwn_xinetd_1804)
- Web
    - Nginx - Alpine
        - General
            - [x] [base_web_nginx](https://github.com/ctfhub-team/base_web_nginx)
        - PHP-FPM - [Example/Demo](https://github.com/ctfhub-team/challenge_pwnhub_2017_web_open_weekday)
            - [x] [base_web_nginx_php_56](https://github.com/ctfhub-team/base_web_nginx_php_56)
            - [x] [base_web_nginx_php_74](https://github.com/ctfhub-team/base_web_nginx_php_74)
        - PHP-FPM & MySQL - [Example/Demo](https://github.com/ctfhub-team/challenge_gyctf_2020_web_babyphp)
            - [x] [base_web_nginx_mysql_php_56](https://github.com/ctfhub-team/base_web_nginx_mysql_php_56)
            - [x] [base_web_nginx_mysql_php_74](https://github.com/ctfhub-team/base_web_nginx_mysql_php_74)
    - Httpd - Debian
        - General & CGI
            - [x] [base_web_httpd](https://github.com/ctfhub-team/base_web_httpd)
        - PHP-MOD
            - [x] [base_web_httpd_php_56](https://github.com/ctfhub-team/base_web_httpd_php_56)
            - [x] [base_web_httpd_php_74](https://github.com/ctfhub-team/base_web_httpd_php_74)
        - PHP-MOD & MySQL
            - [x] [base_web_httpd_mysql_php_56](https://github.com/ctfhub-team/base_web_httpd_mysql_php_56)
            - [x] [base_web_httpd_mysql_php_74](https://github.com/ctfhub-team/base_web_httpd_mysql_php_74)
    - Python - Alpine
        - Gunicron - [Example/Demo](https://github.com/ctfhub-team/challenge_ddctf_2019_web_homebrew_event_loop_base)
            - [x] [base_web_gunicorn_python_27](https://github.com/ctfhub-team/base_web_gunicorn_python_27)
            - [x] [base_web_gunicorn_python_36](https://github.com/ctfhub-team/base_web_gunicorn_python_36)
        - Supervisor
            - [x] [base_web_supervisor_python_27](https://github.com/ctfhub-team/base_web_supervisor_python_27)
            - [x] [base_web_supervisor_python_36](https://github.com/ctfhub-team/base_web_supervisor_python_36)
    - Tomcat - Alpine - [Example/Demo](https://github.com/ctfhub-team/challenge_wangdingbei_2020_web_qinglong_filejava)
        - [x] [base_web_tomcat_8u121](https://github.com/ctfhub-team/base_web_tomcat_8u121)
        - [x] [base_web_tomcat_8u171](https://github.com/ctfhub-team/base_web_tomcat_8u171)
        - [x] [base_web_tomcat_8u191](https://github.com/ctfhub-team/base_web_tomcat_8u191)
        - [x] [base_web_tomcat_8u212](https://github.com/ctfhub-team/base_web_tomcat_8u212)
    - NodeJs - Debian
        - General - [Example/Demo](https://github.com/ctfhub-team/challenge_wangdingbei_2020_web_qinglong_notes)
            - [x] [base_web_nodejs_pm2](https://github.com/ctfhub-team/base_web_nodejs_pm2)
        - XSSBot
            - [x] [base_web_nodejs_koa_xssbot](https://github.com/ctfhub-team/base_web_nodejs_koa_xssbot)

## 目录结构及说明

### Web 类

```
/  
├── docker-compose.yml  
├── Dockerfile  
├── _files  
│   ├── docker-entrypoint* 环境入口文件  
│   ├── flag.sh 动态 Flag 处理文件  
│   └── supervisord.conf (非必须,仅base_web_supervisor_*)  
├── meta.yml 元数据文件，题目名称及相关说明  
└── src  
    └── index.php  
```

### Pwn

Native 环境为基础 Ubuntu 环境，仅预装 tcpdump、lib32stdc++6 等库（详情请看源码），利用 socat 将容器暴露端口转发至题目监听端口。适用于自监听类题目。

Xinetd 在 Native 的基础上(无socat)安装了 xinetd，并以此运行题目。

```
/  
├── docker-compose.yml  
├── Dockerfile  
├── _files  
│   ├── start.sh 环境入口文件  
│   └── flag.sh 动态 Flag 处理文件  
├── meta.yml 元数据文件，题目名称及相关说明  
├── source (非必须,源代码文件夹)  
│   └── xxx.c  
└── src  
    ├── pwn 题目可执行文件  
    └── pwn.xinetd.conf (非必须,xinetd配置)  
```