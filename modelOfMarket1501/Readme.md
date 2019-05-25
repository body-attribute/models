Market1501数据集的属性预测

Market1501的Label的格式与DukeMTMC-ReID基本相同，不同的是Market1501的Label中的Age属性是用1、2、3、4分别代表young、teenager、adult、old的，而其他的属性都是用1和2代表是或者不是的，所以我决定为了方便预测我把Age属性删除，然后添加young、teenager、adult、old四个属性。最后和之前一样也是用Cross-entropy作为损失函数，同样使用没有预训练的ResNet。

最后结果ResNet18和ResNet50分别达到了90.52%和90.18%的正确率。
