#### redis配置

1. 查看6379（或者自定义redis端口）时候打开
   - firewall-cmd --query-port=6379/tcp 如果返回no则端口没有开启
   - firewall-cmd --add-port=6379/tcp （加 --permanent 永久有效），返回success说明开启成功

