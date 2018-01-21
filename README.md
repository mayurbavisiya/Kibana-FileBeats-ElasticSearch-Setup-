# Kibana-FileBeats-ElasticSearch-Setup for Window machine
Setup of Kibana for running applications log visualization using filebeats and ElasticSearch


Note : Once we configure below setup Filebeats automatically read logs file from your log file and will saved in elasticsearch registery.


Hi guys , Lets have a small dive for enable kibana for your haevay logs management using Elastic search and filebeats.



Download required tools from below respectives urls.

https://www.elastic.co/blog/elasticsearch-5-3-0-released 

https://www.elastic.co/downloads/beats/filebeat

https://www.elastic.co/downloads/kibana

Download and just unzip it and follow steps for setup.

1)   Start Elasticsearch with follow coomand from cmd
    <elasticSearchHome>/bin : elasticsearch
  
    you can create your cluster and node network by configuting elasticsearch.yml placed at <elasticsearch-6.1.2>/config    
    You can check running elasticsearch using http://127.0.0.1:9200
    For getting output based on some query use http://127.0.0.1:9200/_search?q=ABC
    
  
2)  Start Kibana with follow coomand from cmd
 
    <kibana-6.1.2-windows-x86_64>/bin : kibana.bat
    you can change configuration like startup timeout time etc by changing  kibana.yml placed at  <kibana-6.1.2-windows-x86_64>/config         folder.
    
    Access running Kibana with http://127.0.0.1:5601
    You can see Dashboard, Customize as per you requirement
    Check Dashboard/Discover in left Menu
    And you can see all the logs from your log file with timestamp. Filebeat automatically push new log at evry 30 Sec(You can customie     that time).
      
  
3)  Setup Dashboards and start filebeats

    Configure your elasticsearch and kibana url in filebeat.yml placed at <filebeat-6.1.2-windows-x86_64>.
    Ex. For local enviornment it would be localhost it will be like
    
    setup.kibana:
    host: "localhost:5601"
    
    
    output.elasticsearch:
    hosts: ["127.0.0.1:9200"]
    
    
    Also configure 
    
    =========================== Filebeat prospectors =============================

    filebeat.prospectors:
    - input_type: log
      paths: ["D:/u01/app/oracle/ISAdmin.log"]                              #Give your logs path
      #include_lines: ['^ERR', '^WARN' , 'exception']
      json.message_key: event
      json.keys_under_root: true     
      tags: [
        "OCCUREDEVENT" 
      ]
    
      You can give your tag name.
    

    After above updatetion start filebeat using below commands.
    
    <filebeat-6.1.2-windows-x86_64> : filebeat setup --dashboards
    <filebeat-6.1.2-windows-x86_64> : start filebeat
    
    
    
    
    
  
