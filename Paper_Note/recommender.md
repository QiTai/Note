### Recommending What Video to Watch Next-A Multitask Ranking System-google-19Recsys
+ 基本框架沿用16年YouTube那篇经典推荐文章的框架
+ focus on ranking stage in a two-stage recommending system (retrival + ranking)
+ whole architecture
  ![whole architecture](https://github.com/QiTai/Note/Paper_Note/blob/master/img/Recommending What Video to Watch Next-A Multitask Ranking System-Figure1.PNG)
+ main points : Multitask & Position Bias
+ 针对Multitask(engagement, satifaction)引入了Multi-Gate Mixture-of-Experts;线上融合多个task的prediction score,权重文章提到手动调节(???);
  ![Multitask]https://github.com/QiTai/Note/Paper_Note/blob/master/img/RRecommending What Video to Watch Next-A Multitask Ranking System-Figure2.PNG)
+ 针对Position Bias，仿照Wide&Deep架构，这里引入Shallow Side Tower(这个Tower使用Position相关的特征)，在线上预测时，position设为missing;如下图
  ![Position Bias](https://github.com/QiTai/Note/Paper_Note/blob/master/img/RRecommending What Video to Watch Next-A Multitask Ranking System-Figure3.PNG)