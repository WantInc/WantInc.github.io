---
layout: post
title: "Elasticsearch环境部署"
date: 2015-05-04T18:05:24+08:00
---
### mac环境下部署

  第一步，安装elasticsearch服务

~~~~~~~
  brew install elasticsearch
~~~~~~~

  第二步，设置登录自动加载服务

~~~~~~~
  ln -sfv /usr/local/opt/elasticsearch/*.plist ~/Library/LaunchAgents
~~~~~~~

  第三步，添加搜索引擎插件elasticsearch-analysis-ik

~~~~~~~    
  git clone https://github.com/medcl/elasticsearch-analysis-ik
  cd elasticsearch-analysis-ik
  mvn compile
  mvn package
  plugin —install analysis-ik —url file:///#{project_path}/elasticsearch-analysis-ik/target/releases/elasticsearch-analysis-ik-1.3.0.zip
  vi /usr/local/opt/elasticsearch/config/elasticsearch.yml
  index:
    analysis:                   
      analyzer:      
        ik:
          alias: [ik_analyzer]
          type: org.elasticsearch.index.analysis.IkAnalyzerProvider
        ik_max_word:
          type: ik
          use_smart: false
        ik_smart:
          type: ik
          use_smart: true
~~~~~~~
 
 第四步，加载elasticsearch

~~~~~~~~~~~~~
  launchctl load ~/Library/LaunchAgents/homebrew.mxcl.elasticsearch.plist
~~~~~~~~~~~~~
