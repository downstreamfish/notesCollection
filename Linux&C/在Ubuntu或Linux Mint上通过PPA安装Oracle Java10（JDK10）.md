##   在Ubuntu或Linux Mint上通过PPA安装Oracle Java10（JDK10）

* 添加LinuxUprising Java PPA 仓库到软件源，然后通过命令安装：

  ```bash
  sudo add-apt-repository ppa:linuxuprising/java
  sudo apt update
  sudo apt install oracle-java10-installer
  ```

* 添加软件源和安装java之后，设置Oracle Java10位默认。在Ubuntu中，Java10会自动设置为默认的。但在Linux Mint，需要以下命令：

  ```bash
  sudo apt install oracle-java10-set-default
  ```

  

* 如果安装了Oracle Java10之后，不想将它设置为默认的Java，确认`oracle-java10-set-default`包已卸载或没有被安装。

  ```bash
  sudo apt remove oracle-java10-set-default
  ```

* 安装和设置完默认Java之后，可以通过如下命令检查当前Java版本

  ```bash
  java -version
  ```

* 如果Oracle Java10是默认的，显示结果应如下：

  ```bash
  java version "10" 2018-03-20
  Java(TM) SE Runtime Environment 18.3 (build 10+64)
  Java HotSpot(TM) 64-Bit Server VM 18.3 (build 10+46, mixed mode)
  ```

  

* 也可以尝试使用`javac`:

  ```bash
  javac -version
  ```

* 显示结果如下：

  ```bash
  javac 10
  ```

* 在安装Oracle Java过程中，需要接受Oracle Java许可，可以使用如下命令自动接受许可：

  ```bash
  echo oracle-java10-installer shared/accepted-oracle-license-vl-l select true | sudo /usr/bin/debconf-set-selections
  ```

* 如果不行，可以尝试另一个：

  ```bash
  echo oracle-java10-installer shared/accepted-oracle-licence-vl-l boolean true | sudo /usr/bin/debconf-set-selections
  ```

  