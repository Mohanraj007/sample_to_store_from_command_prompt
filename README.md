
# AmberFuels Backend

## 1. Requirements
1) PHP >= 7.2
2) Postgresql >= 10.4
3) Supervisor. If you don't have it download it from [here](http://supervisord.org)

## 2. Installation

1) Run `composer install`. If you don't composer install it from [here]( https://getcomposer.org/download/).
2) Create the `.env` file. Copy the contents of `.env.example` file and change configurations of the `.env` according the your configuration
3) Run `php run migrate`
4) Run `php artisan make:seeder UsersTableSeeder`
5) Give 777 permission to the `storage` folder

## 3. Cron Jobs
1) Paste the following code on the crontab
```
* * * * * cd /home/kuya/Workspace/php/amber_fuel/ServerApi/ && php artisan schedule:run >> /dev/null 2>&1
```
**Note:** Change project location

## 4. Supervisor configuration

1) Create `/etc/supervisor/conf.d/amberfuel-worker.conf` file
2) Copy & paste the following content
```
[program:amberfuel-worker]
process_name=%(program_name)s_%(process_num)02d
command=php /home/kuya/Workspace/php/amber_fuel/ServerApi/artisan queue:work redis --sleep=3 --tries=3
autostart=true
autorestart=true
user=root
numprocs=8
redirect_stderr=true
stdout_logfile=/home/kuya/Workspace/php/amber_fuel/ServerApi/storage/logs/worker.log
```
3) Run the following commands
```php
sudo supervisorctl reread

sudo supervisorctl update

sudo supervisorctl start amberfuel-worker:*
```"# sample_to_store_from_command_prompt" 
