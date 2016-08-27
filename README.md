# seeia.github.io
seeia的CSDN博客

#1、刚解决了一个问题，在虚拟机里面启动express，一切都正常，app也开始监听3000端口，但是主机就是不能访问站点；我关掉了selinux，iptables也没有开启服务。然后一切都是那么正常，但却就是不通~~ 查了好久，忽视了一个问题，centos的默认防火墙竟然不是iptables！！！ 这就是根源！centOS默认防火墙是firewall，所以关掉firewell就OK了~~
#2、在使用mongoose中间件的时候，发现一直查找不到数据，检查完数据库名和表名均正确，但是依然不成功。
我使用的方式是： var UserInfo = mongoose.model('UserInfo',userSchema);
最后尝试插入数据，看是否插入成功，神奇的发现，数据时插入成功了，但是表名却多了一个s，尝试几次发现都是这种情况。最后去查找mongoose的API文档，才发现，原来是方法使用错误。
Mongoose#model(name, [schema], [collection], [skipInit]) 
  name <String> model name
  [schema] <Schema>
  [collection] <String> name (optional, induced from model name)
  [skipInit] <Boolean> whether to skip initialization (defaults to false)
  
  原来第一个参数并不是集合名，而是第三个参数，若缺省，则会自动根据name值以复数的形式生成collection，所以会出现多个s的情况。
  所以我们改下：var UserInfo = mongoose.model('UserInfo',userSchema,'user')即可。
