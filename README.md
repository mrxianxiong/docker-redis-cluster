docker pull grokzen/redis-cluster

docker run  -e "IP=0.0.0.0" -e STANDALONE=true -e SENTINEL=true  -p 7000-7005:7000-7005 -d grokzen/redis-cluster:latest
参数介绍：

-e "IP=0.0.0.0" 将内部IP环境变量添加到docker run命令中,这里的规则映射了 0.0.0.0，意味着将接受主机来自所有接口的流量。使用此容器在Mac计算机上运行Redis集群，则需要将容器配置为使用另一个IP地址进行集群发现，因为它无法使用硬编码到容器中的默认发现IP。
-e SENTINEL=true 默认情况下，未启用Sentinel实例。表示启用哨兵实例。如果-e "STANDALONE=true"通过该标志，则默认情况下在端口7006和7007上运行2个独立实例。但是，您可以将此变量设置为所需的多个独立节点，例如-e "STANDALONE=1"。请注意，独立端口在最后一个从属设备之后立即启动。如果-e "SENTINEL=true"传递了该标志，则在与群集的主实例匹配的端口5000到5002上运行3个Sentinel节点。
-p 7000-7005:7000-7005 端口映射，左边是宿主机也就是win 的端口号，右边是容器内的端口号，这里是映射了6个端口哦，包括：7000,7001,7002，7003,7004,7005 这6个端口，我也是第一次听说这样子的，完成后底下会回显一个容器ID如图：

docker exec -ti XXXX redis-cli -c -p 7000 


cluster info 来查询集群信息，如图：




部署文档
https://www.cnblogs.com/Solomon-Kane-zm/p/14468136.html
