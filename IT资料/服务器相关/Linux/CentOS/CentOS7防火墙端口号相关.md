```powershell
# firewall-cmd --list-all-zones    #查看所有的zone信息
# firewall-cmd --get-default-zone     #查看默认zone是哪一个
# firewall-cmd --zone=internal --change-zone=p3p1  #临时修改接口p3p1所属的zone为internal
# firewall-cmd --add-service=http    #暂时开放http
# firewall-cmd --permanent --add-service=http  #永久开放http
# firewall-cmd --zone=public --add-port=80/tcp --permanent  #在public中永久开放80端口
# firewall-cmd --permanent --zone=public --remove-service=ssh   #从public zone中移除服务
# firewall-cmd --reload   #重新加载配置
```

