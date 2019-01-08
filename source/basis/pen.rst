.. index:: ! pen

画笔
====

有画笔才能画线条、三角形、圆形等各种复杂的形状。

GMT中的画笔有三个属性：笔宽、颜色和线型，三者用逗号分隔，即::

    <width>,<color>,<style>

在 GMT 模块的语法介绍中，一般用 ``<pen>`` 表示画笔属性，读者在见到 ``<pen>``
时应自行脑补成 ``<width>,<color>,<style>``\ 。

在指定画笔属性时，可以指定三个属性中的任意一个或多个属性，但要保证属性的相对顺序。

画笔线宽
--------

可以通过两种方式指定画笔宽度：

1. 宽度值+单位，即 ``<width>c|i|p``

   线宽的单位可以取 ``p``\ 、 ``c`` 或 ``i`` （见\ :doc:`unit`\ 一节）。
   若不显式指定线宽单位，则默认线宽单位为 ``p``\ 。

   推荐只使用 ``p`` 作为线宽单位，毕竟多数情况下线条的宽度都比较小，用“小”单位
   ``p`` 作为单位更方便些。

   建议总是显式指定线宽单位，以使得命令的参数更加易读，比如 ``1p``\ 、\ ``0.25p``\ 。

2. 预定义画笔宽度名

   对于一些常用的画笔宽度，GMT将其定义为特定的名字，以方便用户使用。
   下表中列出了GMT预定义画笔宽度名及其对应的线宽。

   .. table:: GMT预定义画笔宽度名

      +---------------+---------+---------------+--------+
      | 线宽名        | 线宽    | 线宽名        | 线宽   |
      +===============+=========+===============+========+
      | ``faint``     | 0       | ``thicker``   | 1.5p   |
      +---------------+---------+---------------+--------+
      | ``default``   | 0.25p   | ``thickest``  | 2p     |
      +---------------+---------+---------------+--------+
      | ``thinnest``  | 0.25p   | ``fat``       | 3p     |
      +---------------+---------+---------------+--------+
      | ``thinner``   | 0.50p   | ``fatter``    | 6p     |
      +---------------+---------+---------------+--------+
      | ``thin``      | 0.75p   | ``fattest``   | 12p    |
      +---------------+---------+---------------+--------+
      | ``thick``     | 1.0p    | ``obese``     | 18p    |
      +---------------+---------+---------------+--------+

.. note::

   最细的画笔宽度可以通过设置笔宽为 ``0p`` 或 ``faint`` 来实现，但画笔的实际
   宽度由具体的设备来决定。通常情况下，当你放大图片时，线宽总是保持最小值。

画笔颜色
--------

见 :doc:`color` 一节。

画笔线型
--------

画笔线型属性控制了线条的外观，可以用四种方式表示：

1. 预定义线型名

   GMT预定义了几种线型名，包括 ``solid`` （实线）、 ``dashed`` （虚线）和
   ``dotted`` （点线）和 ``dashdot`` （虚线-点线）。

2. 简单符号

   - 句点号 ``.`` 表示点线
   - 破折号 ``-`` 表示虚线

3. 组合符号

   通过对简单符号的任意组合可以获得更多的线型，比如 ``.-`` 表示点划线，
   ``..-`` 表示两个点号与一个破折号交替出现。

4. 复杂线型

   可以通过 ``string:offset`` 的形式自定义更复杂的线型。其中 ``string`` 是一系列
   由下划线 ``_`` 分隔的数字组成。这一系列数字中，第奇数个数字表示实线的长度，
   第偶数个数字表示空白的长度。通过实线和空白的长度的不同组合，即可构成多种
   复杂的线型。 ``offset`` 表示线段开始处整个线型的初始相位移动。

   例如， ``4_8_5_8:2`` 表示线型首先是长度为 ``4p`` 的实线，然后是长度为 ``8p``
   的空白，紧接着长度为 ``5p`` 的实线和长度为 ``8p`` 的空白，然后按照该模式不断
   重复。此处的 ``offset`` 值为 ``2p``\ ，因而线段的最开始处，第一条实线的长度
   ``4p`` 经过相移后长度为 ``2p``\ 。线型中的这些数值，默认单位是 ``p``\ ，也可以
   使用 ``c`` 或 ``i``\ 。

.. note::

   ``.`` 和 ``-`` 的绝对长度由画笔宽度来决定。
   ``.`` 的长度等于画笔宽度； ``-`` 的长度为8倍画笔宽度；
   点线或虚线中段间空白的长度为4倍画笔宽度。

画笔小结
--------

画笔包含三个属性：宽度、颜色、线型。通过不同的组合方式，可以定义无穷多种画笔。

下图中展示了不同风格的画笔，读者可以将下面命令里 ``-W`` 选项中的 ``<pen>``
修改成不同的值来理解这一节的内容::

    gmt psxy -R0/10/0/5 -JX10c/5c -W<pen> > pens.ps << EOF
    0 2
    10 2
    EOF

.. gmt-plot:: /scripts/GMT_pens.sh
    :show-code: false
    :caption: GMT画笔示例

其他属性
--------

除了上面提到的三个画笔属性之外，GMT中还有一些参数可以影响线条的外观。这些参数包括：

- :ref:`PS_LINE_CAP <PS_LINE_CAP>`\ ：控制线段顶端的绘制方式
- :ref:`PS_LINE_JOIN <PS_LINE_JOIN>`\ ：控制线段拐点/交点的绘制方式
- :ref:`PS_MITER_LIMIT <PS_MITER_LIMIT>`\ ：控制线段拐点在 ``miter`` 模式下的阈值