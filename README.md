# MacShell脚本

在Mac电脑上最常用的**批处理脚本**就是Shell了，就像在Windows电脑上常用的Batch文件。收集开发中常用到的Shell脚本，如下：

+ Mac使用Shell处理图片
   - 一键缩放图片生成App所有尺寸icon图标
   - 一键缩放图片生成App所需启动图
   - 一键将文件夹内图片生成1x/2x/3x图片并自动重命名
   - 一键将文件夹内所有图片转为PNG格式
+ 利用Shell脚本自动化打ipa包
+ 将.app文件转换为.ipa文件

## 一、Shell脚本简要用法:

在Mac的终端中，cd打开图片文件夹—>拖入Shell文件到终端—>回车-->输入1或2或3或4即可进行对应操作,如图

![这里写图片描述](https://github.com/muzipiao/GitHubImages/blob/master/CreateiPhoneIconShellBlogImages/1.png)

## 二、Shell脚本用法示例(以CreateiPhoneIconShell.sh为例):

### 2.1、例如你要处理的图片文件放在桌面上的`images`文件中

![这里写图片描述](https://github.com/muzipiao/GitHubImages/blob/master/CreateiPhoneIconShellBlogImages/2.png)

### 2.2、把要作为图标的图片命名为icon

![图片展示图片源自网络](https://github.com/muzipiao/GitHubImages/blob/master/CreateiPhoneIconShellBlogImages/3.png)

### 2.3、需要在终端中用cd命令先进入此文件夹，终端输入cd空格(cd后面有一个空格)，然后拖入你桌面的`images`文件夹

![这里写图片描述](https://github.com/muzipiao/GitHubImages/blob/master/CreateiPhoneIconShellBlogImages/4.png)
![这里写图片描述](https://github.com/muzipiao/GitHubImages/blob/master/CreateiPhoneIconShellBlogImages/5.png)

### 2.4、同理，再拖入所用到的Shell文件，然后回车确认

![这里写图片描述](https://github.com/muzipiao/GitHubImages/blob/master/CreateiPhoneIconShellBlogImages/6.png)

### 2.5、显示界面如下，如果需要生成AppIcon图标，则输入数字1，回车

![这里写图片描述](https://github.com/muzipiao/GitHubImages/blob/master/CreateiPhoneIconShellBlogImages/7.png)

### 2.6、JPG与PNG注意点：

由于我在网上找到的是`JPG`图片，转为`PNG`图片后，`Alpha通道`颜色异常，所以有`CGColor`颜色警告，正常`PNG`图片处理是没有<...>部分的，有警告但不影响使用。
![这里写图片描述](https://github.com/muzipiao/GitHubImages/blob/master/CreateiPhoneIconShellBlogImages/8.png)


## 三、注意点

### 3.1、生成AppIcon注意点(苹果官方要求`PNG`格式)

* 图片名称需要为**icon.png**；
* 尺寸目前包括40×40 58×58 60×60 80×80 87×87 120×120 180×180；
* 如果需要特殊尺寸，在下方的for循环处添加相应的数字即可。

![这里写图片描述](https://github.com/muzipiao/GitHubImages/blob/master/CreateiPhoneIconShellBlogImages/9.png)

### 3.2、生成App启动图片LaunchImage注意点(苹果官方要求`PNG`格式)

>  iPhone屏幕尺寸一览
>  * **iPhone 6Plus/6SPlus/7Plus (Retina HD 5.5 @3x): 1242 x 2208**
>  * **iPhone 6/6S/7 (Retina HD 4.7 @2x): 750 x 1334**
>  * **iPhone 5/5S(Retina 4 @2x): 640 x 1136**
>  * **iPhone 4/4S(@2x): 640 x 960**

* 要作为启动图片的名称需要为LaunchImage.png；
* 目前按照屏幕尺寸默认生成尺寸为960x640，1134x640，1334x750，2208x1242；
* 如果需要其他尺寸，方法同上，自己到Shell文件中修改相应尺寸数字即可。

```Shell

#>>>>>>>>>>一键生成App启动图片LaunchImage<<<<<<<<<<<<<
#自动生成LaunchImage
LaunchWithSize() {
case $1 in
"960")
sips -z 960 640 LaunchImage.png --out LaunchImageFolder/LaunchImage_960x640.png
;;

"1136")
sips -z 1136 640 LaunchImage.png --out LaunchImageFolder/LaunchImage_1134x640.png
;;

"1334")
sips -z 1334 750 LaunchImage.png --out LaunchImageFolder/LaunchImage_1334x750.png
;;

"2208")
sips -z 2208 1242 LaunchImage.png --out LaunchImageFolder/LaunchImage_2208x1242.png
;;
esac
}

```

### 3.3、批量生成1x，2x，3x图片

* 将当前文件夹下所有图片缩放为1x，2x，3x图片，并自动命名；
* 注意：如果icon.png和LaunchImage.png也在当前图片文件下，也会生成1x，2x，3x图片。

### 3.4、批量将图片转为PNG格式

* 会将当前文件夹下所有图片转换为PNG格式；
* 注意，用Shell脚本和用苹果图片预览工具另存为转换，都是仅仅转换图片格式，简单的将缺失Alpha通道色都补为1，体积会变大；
* 例如JPEG图片格式，只包含RGB通道颜色，体积小，适合网络传输和打印；而PNG图片格式，除了包含RGB颜色外，还包含Alpha透明通道；
* PNG图片格式是苹果官方推荐的格式，因为iOS系统会用到大量的透明效果，而且PNG图片支持硬解码，使界面更流畅。

----------

如果您觉得有所帮助，请在[GitHub](https://github.com/muzipiao/MacShell)上赏个Star ⭐️，您的鼓励是我前进的动力。
