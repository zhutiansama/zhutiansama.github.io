## Matplotlib简介

- 是专门用于开发2D图表(包括3D图表)

- 使用起来及其简单

- 以渐进、交互式方式实现数据可视化

总结：就是为了方便数据可视化

### Maplotlib图像结构

<img src="C:\Users\asus\AppData\Roaming\Typora\typora-user-images\1572484529983.png" alt="1572484529983" style="zoom:60%;" />

主要组件：Figure-Axes-Grid ；Plot-Scatter-bar-historgram-pie；Legend-Title-X/Y axis Label-Minor/Major tick label

（学会对知识进行分类然后记忆）

Axes:（让图像更容易被用户理解，但不会对图像产生影响）  

- 外观facecolor  
- 边框spines  
- 坐标轴axis 
- 坐标轴刻度tick   
- 坐标抽刻度标签tick label  
- 网格线grid  
- 图例legend  
- 标题title

总结：Axes内：通过plot，scatter，bar，histogram，pie绘制出图像

 细节：**plt.show()会释放figure资源**，如果在显示图像之后保存图片将只能保存空图片

---

### Matplotlib操作

导入模块：import matplotlib.pyplot as plt

**需求：展示一周的天气情况 并设置dpi为80，保存图像在当前目录**

```python
# 1.创建画布(容器层)
plt.figure(figsize=(10, 10))
# 2.绘制折线图(图像层)
plt.plot([1, 2, 3, 4, 5, 6 ,7], [17,17,18,15,11,11,13])
# 3.保存图像
plt.savefig('./image1')
# 4.显示图像
plt.show()
```

错误：导入模块为matplotlib.pyplot !!!

**需求：画出城市一个小时内温差的变化，并重新设置刻度，还有标题和x与y轴名称**

```python
# 0.准备x, y坐标的数据
x = range(60)
y_shanghai = [random.uniform(15, 18) for i in x]

# 1.创建画布
plt.figure(figsize=(20, 8), dpi=80)

# 2.绘制折线图
plt.plot(x, y_shanghai)

# 3.构造x轴刻度标签
x_ticks_label = ["11点{}分".format(i) for i in x]
# 构造y轴刻度
y_ticks = range(40)

# 修改x,y轴坐标的刻度显示
plt.xticks(x[::5], x_ticks_label[::5])
plt.yticks(y_ticks[::5])

# 标签设置
plt.title("temp change")
plt.xlabel("time")
plt.ylabel("tempure")

# 4.显示图像
plt.show()
```

细节：必须先plt.plot数据加载后才能设置x和y的刻度

细节：random.uniform(15,18) for i in x 可以看作前面那句话执行x词，i在这里没有用到

细节：[::5]是python特有的切片机制

**需求：要求在上面的基础上，在添加另一个城市的温度变化,并且显示图例和网格**

```python
# 增加北京的温度数据
y_beijing = [random.uniform(1, 3) for i in x]

# 绘制折线图
plt.plot(x, y_shanghai, label="上海")
# 使用多次plot可以画多个折线
plt.plot(x, y_beijing, color='r', linestyle='--', label="北京")
# 显示图例
plt.legend(loc="best")

# 显示网格
plt.grid(linestyle="--", alpha=0.5)
```

细节：只有给图像加上label在能使用图例哦

**需求：要求分开两个折线图到不同的坐标系中**

```python
axes = plt.subplots(nrows=1, ncols=2, figsize=(20, 8), dpi=100)
axes[0].plot(x, y_shanghai, label="上海")
axes[1].plot(x, y_beijing, label="北京", linestyle="--", color="r")
```

总结：axes用数组的形式映射为多个画布，然后就实现了不同的坐标系

**需求：画出sin函数图像**

```python
import numpy as np
x=np.linspace(-10,10,1000)
y=np.sin(x)

plt.figure(figsize=(20,8),dpi=80)
plt.plot(x,y)
plt.grid()

plt.show()
```

**需求：画出一个饼图**

```python
x_data=[1,2,3,4,5,6]
labels = ['娱乐','育儿','饮食','房贷','交通','其它']
plt.figure(figsize=(10,10),dpi=80)
plt.pie(x_data,labels=labels,autopct='%1.1f%%')
plt.show()
```





