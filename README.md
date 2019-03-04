# Spellcorrection
搜索引擎多候选词推荐


系统主要分为三个部分：离线、服务器端、客户端；
一、离线
1.读取配置文件，进行初始化配置；
2.分析原始数据，建立词典；
3.建立词典的索引表；


二、服务器端
1.单例模式读取配置文件、词典和索引表；
2.缓冲区初始化，得到已在磁盘中的缓冲区内容，得到计时器后，以一定周期更新缓冲区内容；
3.主要服务器类初始化，开启线程池，开启定时器，注册回调函数；
4.查询单词时在线程池内完成，如果不在线程的缓冲区中，则去索引表里查找，索引表查找到后同时加入缓冲区；
5.查询完成后发送给客户端；


三、客户端
1.epoll监听消息和发送消息给服务器；
2.收到消息后用jsonParse分析，得到推荐的关键词。