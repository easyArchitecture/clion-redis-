导入源代码后需要进入deps中
每个目录下执行make
唯独jemelloc先执行一下./config 然后在make
hiredis还需要sudo make install一下
然后加入本例子的cmake就可以运行了

用clion读redis代码方便多了！！

另外server的启动文件是server.c 从这开始跟就好了
