对PETA数据集的人体属性预测

PETA数据集的Label处理有点麻烦，它不像DukeMTMC-relD那样直接给出了所有数据的label的mat文件，而是在每一个文件夹里面有一个Label.txt文件来给出该文件夹里面所有图片的label，而且label还不是直接用数字表示，而是用具体的属性英文表示的。一共有十个文件夹，而且每个文件夹里图片和Label的命名格式还不太一样。这就给自定义DataSet造成了一些麻烦。

我的做法是先把所有文件夹里面图片的路径存到一个数组里，把这个数组作为DataSet的一个参数。然后把每个文件夹里的Label.txt整合成一个字典，字典格式为：{'name of folder' : {'id of image' : [attributes of image]}}，然后把它保存到一个mat文件里方便后续使用。然后在自定义的DataSet里面可以根据图片的路径解析出name of folder 和 id of image，这样就可以得到对应的attributes了。还有一个问题是每张图片的attributes 数组的长度都是不一样的，因为该数组里面只给出了图片有的属性（后面用1表示），而没有的属性（后面用0表示）则没有给出。我的做法是创建一个所有的属性（共105个）的数组PETA_Keys，每个image的label也都是105维的张量，遍历attributes数组，对其中的每一个attribute，找到它在PETA_Keys里的index，然后把张量label里对应index的位置的元素设为1。

最后使用了没有预训练resnet18和resnet50作为基础网络进行训练，最后两者在测试集上的准确率分别为91.37%和91.69%。