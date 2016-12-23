## 应用声明支持HiDPI
Project proptery -> Manifest Tool -> Input and Output -> DPI Awareness  设置为下面的值之一
* High DPI Aware
* Per Monitor High DPI Aware



## DPI和缩放对应关系
* 96 DPI = 100% scaling
* 120 DPI = 125% scaling
* 144 DPI = 150% scaling
* 168 DPI = 175% scaling
* 192 DPI = 200% scaling


## 图片资源  
` <Button name="maxbtn" width="27" height="21" normalimage="file='sys_btn_max.png' source='0,0,26,21'" hotimage="file='sys_btn_max.png' source='27,0,53,21'" pushedimage="file='sys_btn_max.png' source='54,0,80,21'"/> `  
例如这一个最大化按钮，需要准备5套大小的图片,对应不同的DPI.在xml 里面只需要指明100% 的图片名称，其他的 DPI 的图片会自动获取.
* sys_btn_max.png   
81 x 22 像素
* sys_btn_max@125.png  
99 x 27 像素
* sys_btn_max@150.png  
122 x 33 像素
* sys_btn_max@175.png  
142 x 39 像素
* sys_btn_max@200.png  
162 x 44 像素


## 修改Duilib
有些控件或者属性可能还没有提供DPI适配,需要自己修改，修改时需要注意下面几点


* `m_cXY m_rcPadding m_cxyFixed m_cxyMin`  
类似这些保存 xml 里面的声明的值的变量，里面放的是 100% 的值。

* `m_rcItem`  保存的是缩放后的值

* 调用 `GetManager()->GetDPIObj()->Scale` 进行缩放的时候需要判断  `if(GetManager()==NULL`

* ` m_sImageModify.SmallFormat(_T("dest='%d,%d,%d,%d'"), d1, d2, d3,d4);  
`  
d1 d2 d3 d4 需要是100% 的值  
