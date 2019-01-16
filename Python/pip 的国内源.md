# pip 的国内源

* 修改 pip 源为豆瓣源

  1. 在用户目录中编辑 .pip/pip.conf (没有就创建一个)

  2. 添加如下内容：

     ```
     [global]
     index-url = http://pypi.douban.com/simple
     [install]
     trusted-host=pypi.douban.com
     ```

     