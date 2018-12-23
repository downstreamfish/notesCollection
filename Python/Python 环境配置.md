# Python 环境配置

* Windows 环境配置：

* Linux 环境配置：

  Linux 下使用 ipython, 使用 tab 键实现命令提示功能。

  ```bash
  sudo apt-get install ipython
  ```

* Python 运行过程： 首先 Python 源文件被 Python 解释器解释，生成字节码文件，该文件不能直接被运行，还要通过 Python解释器解释，生成计算机可执行的二进制文件，然后调入计算机内存中运行。

* .pyc 与 .pyo 文件：

  .py 文件转换为 .pyc 字节码文件，提高程序的加载速度，运行速度不变。

  ```python
  python -m py_compile hello.py
  ```

  .py 文件转换为 .pyo 字节码文件，优化编译，提高运行效率

  ```python
  python -O -m py_compile hello.py
  ```
