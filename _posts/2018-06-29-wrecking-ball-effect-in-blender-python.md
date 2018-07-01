---
layout: post
title: 【译】在Blender用Python制作3D破坏球效果
date: 2018-06-29 00:00:00 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: pohuaiqiu.jpg # Add image post (optional)
tags: [Blender, Python] # add tag
---

![破坏gif图](https://i.imgur.com/9OUdwNR.gif)

以下是您创建上述酷炫动画所需的所有代码：
---
{% highlight ruby %}
import bpy
bpy.ops.mesh.primitive_plane_add(radius=100, location=(0, 0, 0)) # create Plane
bpy.ops.rigidbody.object_add()
bpy.context.object.rigid_body.type = 'PASSIVE'
for x in range(1,19): # create Toruses
    bpy.ops.mesh.primitive_torus_add(location=(0, x*4.3, 110), rotation=(0,1.5708*(x%2), 0), major_radius=3.5, minor_radius=.5, abso_major_rad=1.25, abso_minor_rad=0.75)
    bpy.ops.rigidbody.object_add()
    bpy.context.object.rigid_body.collision_shape = 'MESH'
    if x==1:
        bpy.context.object.rigid_body.enabled = False
    for z in range (0,9): # create Cubes
        bpy.ops.mesh.primitive_cube_add(radius=3, location=(x*6-60,2,2.8+z*6))
        bpy.ops.rigidbody.object_add()        
        bpy.context.object.rigid_body.mass = 0.0001
{% endhighlight %}
---
###### （如果您对Blender Python完全不熟悉， [请单击此处以了解如何复制粘贴代码.](http://slicker.me/blender/3d_mandelbrot.htm)
  我们需要三组刚体（当您在Blender的对象上打开一个刚体的属性时，Blender将模拟与其它刚体的碰撞）

### 1.平面
第2行代码创建一个简单的平面，多维数据集将在该平面上展开。为了防止它因重力而掉落，我们将其作为被动受体（第4代码）。
### 2. 圆环
x循环5-12行代码创建由18个圆环组成的链条，它们将撞击墙体：
6-8行确定它们的坐标并沿Y轴依次旋转90°。旋转是通过x除以2的余数（获得“0-1-0-1-0...”序列）乘以90度（弧度1.5708）实现的。
第10行将它们的碰撞形状设置为“MESH”。如果设置为默认的"Convex Hull"，Blender就不会考虑到中间的孔洞，链条就会脱落。
第11-12行将第一个圆环的"Enabled"属性设置为false，防止由于重力而坠落。这样它就固定在那牵住整个链条。
### 3. 立方体
在13-16行代码中，我们创建了一个由10个立方体组成的列，重量非常轻，以便在撞击时飞得更远。
因为z循环第13行嵌套在x循环第5行中，我们将得到一个18X10的立方体组成的墙。
好了！当您点击时间线上的“播放”时，链条就会掉下来，撞上立方体并让它们飞起来！

![](https://i.imgur.com/BhJdnCe.gif)

现在让我们把最后一个圆环做大一点让它看起来更像一个真正的毁灭球而不是用链条打破墙壁。当我们在它的时候，让我们也旋转链条，使它以一个角度撞击墙壁，从而导致更冷的碰撞。改变第6行代码为:

---
{% highlight ruby %}
bpy.ops.mesh.primitive_torus_add(location=(x*2, x*4.3, 110), rotation=(0,1.5708*(x%2), 0), major_radius=3.5+1*(x==18), minor_radius=.5+1*(x==18), abso_major_rad=1.25, abso_minor_rad=0.75)
{% endhighlight %}
![](https://i.imgur.com/9OUdwNR.gif)
---
[点击此处下载包含代码的.blend文件](https://web.opendrive.com/api/v1/download/file.json/OF8xMzk3MDkxODVf?inline=0)

准备好打破别的东西而不是墙？让我们粉碎这个坏男孩：

![](https://i.imgur.com/JqqHkMp.gif)

将第13-16行代码替换为：
---
{% highlight ruby %}
for z in range(1,10):
    bpy.ops.mesh.primitive_cube_add(radius=3, location=(z*6-60,0,x*6-3))
    bpy.ops.transform.resize(value=(1, .5+10*math.cos(x/3.14)*math.sin(z/3.14),1), constraint_axis=(False, True, False))
    bpy.ops.rigidbody.object_add()
    bpy.context.object.rigid_body.mass=0.0001
{% endhighlight %}
---

并在代码的最开头添加以下行，以便我们可以使用三角函数sin和cos：
---
{% highlight ruby %}
import math
{% endhighlight %}
---
##### 尽情享受破坏吧！

原文地址：http://slicker.me/blender/wreck.htm
