JSON
===
* 第一种类型是标量(scalar), 也就是一个单独的字符串(string)或数字(number)
* 第二种类型是序列(sequence),也就是若干个相关的数据按照一定顺序并列在一起, 又叫做数组(array)或列表(list)
* 第三种类型是映射(mapping), 也就是一个名/值对(name/value), 即数据有一个名称,还有一个与之相对应的值,这又称作散列(hash)或字典(dictionary)
* JSON的四个基本规则:
   1. 并列的数据之间用逗号(,)分割
   2. 映射用冒号(:)表示
   3. 并列数据的集合(数组)用方括号([])表示
   4. 映射的集合(对象)用大括号({})表示

* 数据结构: object, array
* 基本类型: string, number, true, false, null
* 数据结构-object:
  1. `key`必须是string类型, `value`为任何基本类型或数据结构
* 数据结构-array:
  1. 使用`中括号[]`来起始, 并用`逗号,`来分割元素
