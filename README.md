## GitHub-ArtemE91 HTTPServer_OTUS

### HTTP server умеет:
* Маштабироваться на несколько worker'ов (задается аргументом)
* Отвечать 200, 403 или 404 на GET-запросы и HEAD-запросы
* Отвечать 405 на прочие запросы
* Возращать файлы по произвольному пути в DOCUMENTS_ROOT (задается аргументом)
* Вызов /file.html возращает содержимое DOCUMENTS_ROOT/file.html
* Возращает index.html как индекс директории
* Вызов /directory/ возращает DOCUMENTS_ROOT/directory/index.html
* Отвечает следующими загаловками для успешных GET-запросов:
  * Date
  * Server
  * Content-Length
  * Content-Type
  * Connection
* Понимает проблемы и %XX в именах файлов

### Требования
Python 3+ version

### Аргументы для запуска
* host (default=localhost): __-hs__, __--host__
* port (default=9090): __-p__, __--port__
* workers (default=5): __-w__, __--workers__
* DOCUMENTS_ROOT (default=doc_root): __-d__, __--dir_root__
* log (default=log.log): __-l__, __log__

### Запуск сервера
* __%path_to_modile_dir%__ - путь до директории проекта
* __%amount_workers%__ - количество work'ов

```
cd %path_to_modile_dir%
python3 httpd.py -hs %host% -p %port% -w %amount_workers% -d %DOCUMENTS_ROOT%
```
### Нагрузочное тестирование
```
ab -n 50000 -c 100 -r 'http://localhost:8080/'
This is ApacheBench, Version 2.3 <$Revision: 1826891 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking localhost (be patient)
Completed 5000 requests
Completed 10000 requests
Completed 15000 requests
Completed 20000 requests
Completed 25000 requests
Completed 30000 requests
Completed 35000 requests
Completed 40000 requests
Completed 45000 requests
Completed 50000 requests
Finished 50000 requests


Server Software:        otus@gmail.com
Server Hostname:        localhost
Server Port:            8080

Document Path:          /
Document Length:        163 bytes

Concurrency Level:      100
Time taken for tests:   135.600 seconds
Complete requests:      50000
Failed requests:        0
Non-2xx responses:      50000
Total transferred:      15500000 bytes
HTML transferred:       8150000 bytes
Requests per second:    368.73 [#/sec] (mean)
Time per request:       271.199 [ms] (mean)
Time per request:       2.712 [ms] (mean, across all concurrent requests)
Transfer rate:          111.63 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0  197 1875.3     44   26209
Processing:     1   73  61.9     60    1169
Waiting:        1   48  49.8     40    1143
Total:          2  270 1876.0    110   26258

Percentage of the requests served within a certain time (ms)
  50%    110
  66%    140
  75%    155
  80%    164
  90%    191
  95%    209
  98%    328
  99%    541
 100%  26258 (longest request)
```
