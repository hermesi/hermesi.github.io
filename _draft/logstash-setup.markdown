---
layout: post
title:  "Logstash setup"
date:   2017-01-25 16:21:32 +0900
categories: jekyll update
typora-root-url: ..
---
**Logstash configuration**

문제점 : configuration 디렉토리 ./conf.d 에 여러개의 설정 파일을 넣을 경우, 실제 각 설정 파일들이 독립적으로 동작하지 않고, 각 설정 파일의  input의 데이타들이 output에 들어가게 된다. 즉 데이타가 원하는 형태대로 인덱싱되지 않는다.

>  Logstash has a single pipeline. All filters and outputs will apply to all input events unless you use conditionals to select how they apply. If you use multiple configuration files they will effectively be concatenated and treated as a single big file

여러개의 configuration file들을 적용하려고 할 때, input, output, filter에 태그를 달아서, 해당 스트림만 처리하게 해야 한다.

```
input {
file {
path => "BatchData\Batch_Raw_Data.csv"
tags => [ "batchdata" ]
start_position => "beginning"
}
}
output {
if "batchdata" in [tags]{
elasticsearch {
action => "index"
index => "IndexName"
}
}}
```

문제점 : 한번 logstash로 읽어 들인 로드 데이타들은 다시 읽어들이지 못한다. 이에 대한 해결책은 iput 필터에 sincedb_path => "/dev/null"  설정한다.

```
input {
  file {
    path => "/var/log/httpd/access_log-20161010"
    start_position => "beginning"
    sincedb_path => "/dev/null"
  }
}
```

로그스태시를 통해서 읽어들이는 문서의 타입과 인덱스를 정의하는 방법은 다음과 같다.

```
output {
  elasticsearch {
    hosts => ["192.168.1.22:9200"]
    index => "logstash-web-%{+YYYY.MM.dd}"
    document_type => "alog"
  }
  stdout { codec => rubydebug }
}
```

![](/imgs/e_head1.jpg)

[jekyll-docs]: http://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
