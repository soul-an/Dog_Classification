# Dog_Classification
百度西交大宠物狗识别比赛baseline【keras】
【没有机器只有笔记本的同学可以看看、高富帅可以路过了】
【数据预处理】
首先根据官方给的txt对训练集和验证集进行分类，这里有两个地方需要注意一下，训练集的txt行数要不训练集的图片数量多，这是因为txt里面有几十个图片有两个label，要删除一个label，验证集的txt行数要比验证集的图片数量少。分好类之后得到train_class/0、1、2、3...133和val_class/0、1、2、3...133。test训练集直接构建一个二级目录就可以，得到test/test。
【数据增强】用keras自带的图片生成器进行了数据增强，有裁剪、缩放和旋转。对训练集进行了2倍增强。测试集进行了2倍增强。
【整体思路】
这里挂上杨培文大佬主页：https://ypw.io/
整个思路就是按照主页里面的猫狗大战的那个代码的思路，利用训练好的模型生成特征文件，然后把特征文件拼接，直接进行分类预测。猫狗大战里面用个三个模型ResNet50、InceptionV3、Xception。这里使用了两个模型，即InceptionV3和Xception，因为加上ResNet50之后分类的效果变差了，所以最后去掉了。由于增强了2倍测试集，所以用模型对三个测试集分别预测，最后对三个预测矩阵求和取平均。这里也试过投票但是效果不好。
【新手踩坑】
这是第一次接触深度学习，第一次接触计算机视觉，第一次接触keras。所以从最初的搭建环境和调试代码都踩过不少坑。这里由衷感谢一下大队长，作为新手没事就会骚扰一下大队长请教问题，谢谢大队长耐心指教。
1、环境搭建，keras搭建环境比较简单，按照网上的教程即可容易的搭建成功，keras要基于tensorflow使用，安装tensorflow的时候安装gpu版本时，使用keras自动会调用gpu，不用在程序里写调用代码了。
2、整改开源代码、大佬开源的代码需要仔细研究，读懂之后才能加以修改，因为有些模块已经更新过，有的参数有的方法会删除或者改名。
3、对齐label、刚开始本以为图片生成器的读取图片顺寻就是本地图片的保存顺寻，只怪自己太傻太天真，后来请教qq群的前辈，是有一个生成器的label字典的，读取的顺寻其实是1，10，110，这种，所以一定要对其label，不然就会出现0.98类似的成绩。
【总结】
现在这个比赛初赛已经进入到尾声了，如果继续按照这个思路做下去的话可以加模型，但是keras库的其他模型太老，所以要自己搭好模型，导入imagenet的权重，然后生成特征文件。