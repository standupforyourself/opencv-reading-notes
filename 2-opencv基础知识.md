# image结构
  每个opencv image对象是一个numpy.array数据结构，可以通过image[0,0]或者image[0,0,0]来访问像素值。
  第一个索引是像素的y坐标或者行，第二个索引是像素的x坐标或者列，第三个索引则是颜色通道值。

  假设a为numpy.array对象，则a.shape输出图像的行列数(同时也是高度和宽度值)，或者行、列以及颜色通道数。譬如：（5，3）表示5行3列，或者（5，3，3）表示5行3列以及3种颜色的通道; a.size输出数组元素的个数，灰度图中此数值与像素个数相同，BGR图中此数值等于像素个数乘以3。
  

# numpy基本函数
  
  - numpy.arange(n).reshape(a, b)    依次生成n个自然数，并且以a行b列的数组形式显示
    np.arange(16).reshape(2,8) #生成16个自然数，以2行8列的形式显示
	# Out: 
	# array([[ 0,  1,  2,  3,  4,  5,  6,  7],
	#       [ 8,  9, 10, 11, 12, 13, 14, 15]])

  - mat(or array).reshape(c, -1)     将此矩阵或者数组以c行d列（d为自动计算的数值）的形式表示出来
        arr.shape              # output: (a, b)
        arr.reshape(m, -1)     # output: 改变维度为m行、d列 （-1表示列数自动计算，d= a*b /m ）
	arr.reshape(-1, m)     # output: 改变维度为d行、m列 （-1表示行数自动计算，d= a*b /m ）
        arr.reshape(-1, n)     # output：将数组转成n列
        arr.reshape(n, -1)     # output：将数组转成n行
 

  - numpy.arange(a,b,c)    从 数字a起, 步长为c, 到b结束，生成array
  - numpy.arange(a,b,c).reshape(m,n)  ：将array的维度变为m 行 n列
    
	numpy.arange(1,12,2)#间隔2生成数组，范围在1到12之间
	# Out: array([ 1,  3,  5,  7,  9, 11])

        
# 图像基本操作
## 图像读取
   - 坐标系
     ![coordinate system](./images/coordinate_system.png)     
     左上角为坐标原点，原点水平向右为x轴，原点垂直向下为y轴。
   
     row == height == point.y
     col == width == point.x

   - cv2.imread
     此函数返回二维数组或者三位数组; 
     img = cv2.imread(path, option)
     option=cv2.IMREAD_GRAYSCALE, img为二维数组
     option=cv2.IMREAD_COLOR, img为三维数组, 其中z轴表示颜色通道数据，默认为BGR配色

   - 读取某坐标点的像素值或者颜色值
     img = cv2.imread(path, option)
     z = img[x, y], 读取(x, y)处的数值

   - 设置像数值
     img = cv2.imread(path, option)
     img.itemset((150,120,0), 255) # 将点(150, 120)处的绿色通道（BGR[0]）数值更改为255
     img[:,:,1] = 0  # 将所有点的绿色通道数值更改为0

# 视频基本操作
## 视频读写
   - 视频读取
     videoCapture = cv2.VideoCapture(filename)
     fps = videoCapture.get(cv2.CAP_PROP_FPS)  
     size = (int(videoCapture.get(cv2.CAP_PROP_FRAME_WIDTH)),
            int(videoCapture.get(cv2.CAP_PROP_FRAME_HEIGHT)))
     videoWriter = cv2.VideoWriter(
            copyfile, cv2.VideoWriter_fourcc(*"MPEG"),
            fps, size)
