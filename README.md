Smartctl_exporter Dashboard for Grafana  
========

Данный dashbord позволяет просматривать метрики, собранные smartctl_exporter  
https://github.com/prometheus-community/smartctl_exporter 

<img src="https://github.com/goblin039/Smartctl_Dashboard/blob/main/Dashboard.JPG?raw=true" />

Дополнительно отображаются температурные метрики, собранные node_exporter  
https://github.com/prometheus/node_exporter  

Настройка  
------

Для сбора метрик в prometheus.yml добавлены следующие строчки:  
```
  - job_name: 'exporter_linux'
    file_sd_configs:
     - files:
        - '/etc/prometheus/target/linux_ws.json'

  - job_name: 'exporter_smartctl'
    file_sd_configs:
     - files:
        - '/etc/prometheus/target/smartctl_ws.json'
    metric_relabel_configs:
      - source_labels: [device]
        target_label: __tmp_dev
      - source_labels: [__tmp_dev]
        target_label: device_2
```  
Где файл /etc/prometheus/target/linux_ws.json содержит список хостов, с которых собираются метрики node_Exporter:  
```
[
 { "targets":[ "192.168.1.11:9100"], "labels": {"cab": "Klad"} },
 { "targets":[ "192.168.1.12:9100"], "labels": {"cab": "Klad"} } 
]
```  
файл /etc/prometheus/target/smartctl_ws.json для хостов с установленным smartctl_exporter:
```
[
 { "targets":[ "192.168.1.11:9633"], "labels": {"cab": "Klad"} },
 { "targets":[ "192.168.1.12:9633"], "labels": {"cab": "Klad"} }
]
```  

Установка  
------  

Для установки необходимо инпортировать в Grafana файл Smartctl_Comp.json  
