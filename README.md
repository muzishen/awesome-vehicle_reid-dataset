# awesome-vehicle_reid-dataset
Collection of public available person re-identification datasets 

**[NOTE]** It looks like some dataset links are expired. I'm trying my best to recover them. If you happen to know the latest links, PRs are welcomed. 
# The Awesome Vehicle Re-Identification Datasets
Vehicle re-identification has drawn intensive attention in the computer vision society in recent decades. As far as we know, this page collects all public datasets that have been tested by Vehicle re-identification algorithms. If you use any of them, please refer to the original licence. If you have any suggestions or you want to include your dataset here, please open an issue or pull request. 


车辆数据库
1.VERI-Wild: A Large Dataset and a New Method for Vehicle Re-Identification in the Wild (2019-CVPR)
数据库名称：VERI-Wild
论文：[链接](http://openaccess.thecvf.com/content_CVPR_2019/papers/Lou_VERI-Wild_A_Large_Dataset_and_a_New_Method_for_Vehicle_CVPR_2019_paper.pdf)
数据库描述：
车辆图像由一个包含174个摄像机，拍摄范围覆盖超过200平方公里的市区CCTV系统拍摄。摄像机是24小时连续拍摄30天，其长时间的连续拍摄考虑了车辆真实的各种天气和光照问题。包含了40万张图片，4万种车辆标签。该数据集提供了摄像机ID，时间戳，摄像机之间的跟踪关系。
（从论文的述说对于大多数车辆数据集只是拍摄车辆的前视图和后视图来看，该数据集收集时，应该是多角度的）
项目地址：[链接](https://github.com/PKU-IMRE/VERI-Wild)
下载地址：[链接](https://pan.baidu.com/s/1FzvR5iRQgh8ZbSYZPbi9aQ) 密码：kob9

2.Vehicle Re-identification in Aerial Imagery: Dataset and Approach
(2019-arXiv)
数据库名称：VRAI
论文：[链接](https://arxiv.org/pdf/1904.01400v1.pdf)
数据库描述：
使用无人机上的摄像头进行拍摄车辆图像，该数据集包含了137613张图像，包括13022中车辆类别，为了增加车内差异，每辆车至少有两个无人机在不同位置，不同视角和飞行高度(15m至80m)进行拍摄，同时作者手动标记了各种车辆的属性，包括车辆的类别、颜色、天窗、保险杠、备用轮胎和行李架。同时，对于每个车辆图像，还注释标记有差异的部分，用来将特定车辆与其他车辆进行区分。
提交者联系方式：bingliang.jiao@mail.nwpu.edu.cn 

3.HATS: Histograms of Averaged Time Surfaces for Robust Event-Based Object Classification (CVPR 2018)
数据库名称：N-CARS
论文：[链接](https://arxiv.org/pdf/1803.07913.pdf)
数据库说明：
该数据集是基于现实事件的数据集，它由从市区和高速公路环境中的汽车驾驶中获取的约24000个样本组成。用安装在汽车挡风玻璃后面的ATIS摄像机拍摄了80分钟，并将其转换为常规的灰度图像，并标记样本。该数据集有12336个汽车样本和11693非汽车样本组成的两类数据集。其中训练集分为7940个汽车和7482个背景样本，测试集包含4396个汽车样本和4211个背景测试样本。
下载地址：[链接](https://www.prophesee.ai/dataset-n-cars-download/)

4.Exploiting Multi-Grain Ranking Constraints for Precisely Searching Visually-Similar Vehicles (ICCV 2017)
数据库名称：PKU-VD
论文：[链接](http://openaccess.thecvf.com/content_ICCV_2017/papers/Yan_Exploiting_Multi-Grain_Ranking_ICCV_2017_paper.pdf)
数据集描述：
该数据集包含了两个大型车辆数据集（VD1和VD2），它们分别从两个城市的真实世界不受限制的场景拍摄图像。其中VD1是从高分辨率交通摄像头获得的，VD2中的图像则是从监视视频中获取的。作者对原始数据执行车辆检测，以确保每个图像仅包含一辆车辆。由于隐私保护的限制，所有车牌号码都已被黑色覆盖遮挡。所有车辆图像均从前视图进行拍摄。
数据集中为每个图像提供了多样化的属性注释，包括身份编号，精确的车辆模型和车辆颜色。具体来说，身份证号码（ID）是唯一的，并且属于同一车辆的所有图像都具有相同的ID（我们确保每个车辆ID的数据集中至少有两个图像）。我们提供最精确的模型类型，包括详细的车辆类型和不同的生产年份。例如，奥迪A6L-2012＆2015，奥迪A6-2004，奥迪A4-2006＆2008和奥迪A4-2004＆2005是数据集中的四个不同的车辆模型。至于颜色信息，我们的数据集中标注了11种常见颜色。细节如下：
VD1：原先包含1097649张图像，1232种车俩模型，11种车辆颜色，但删除图像里面有多辆车辆以及从车辆后方拍摄的图片，该数据集仅剩846358张图像，141756辆车辆。
VD2：原先包含807260张图像，79763辆车辆，1112种车辆模型，11种车辆颜色。与VD1进行同样的操作后690518张图像。具体训练和测试分割如下表所示。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20191211141228324.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzE3NDAzNjE3,size_16,color_FFFFFF,t_70)数据库链接：[链接](http://pkuml.org/resources/pku-vds.html)
下载链接：填写协议，后下载

5.百度阿波罗3D汽车数据集
数据库名称：百度阿波罗3D汽车数据集
项目网址：http://apolloscape.auto/car_instance.html
数据库描述：
数据集中，camera文件夹中储存相机固有参数、car_model文件夹中储存汽车模型集，保存格式为pkl、ca_poses文件夹中存储图片中标记为汽车的位置、imags文件夹中存储汽车图像、split文件夹中存储着训练和验证图像的索引。
下载地址：[链接](http://apolloscape.auto/car_instance.html)

6.3D Object Representations for Fine-Grained Categorization
数据库名称：Cars Dataset
论文：[链接](http://ai.stanford.edu/~jkrause/papers/3drr13.pdf)
数据库描述：
Cars Dataset包含196种汽车的16,185张图像。数据分割为8,144张训练图像和8,041张测试图像，其中每个类别大致分被分割为50-50。通常类别被标记为Make，Model，Year等级，例如2012特斯拉Model S或2012 BMW M3轿跑车。
项目链接：[链接](http://ai.stanford.edu/~jkrause/cars/car_dataset.html)
训练数据：[链接](http://imagenet.stanford.edu/internal/car196/cars_train.tgz)
测试数据：[链接](http://imagenet.stanford.edu/internal/car196/cars_test.tgz)
7. A Large-Scale Car Dataset for Fine-Grained Categorization and Verification （CVPR 2015）
数据库名称：CompCars
论文：[链接](https://www.cv-foundation.org/openaccess/content_cvpr_2015/papers/Yang_A_Large-Scale_Car_2015_CVPR_paper.pdf)
数据库描述：
CompCars数据集包含来自网络和监视的两个途径的图像。网络图像是汽车收集论坛、公共网张等途径进行获取；监视图像是通过监视摄像机收集的。车辆类型仅包含轿车和SUV，网络图像包含163种车辆品牌，1,716种车型，共有136,726张整个汽车的图像，27,618张汽车零件图像。完整汽车的图像标有边界框和视点。监视性质数据包含在前视图角度中拍摄的50,000个汽车图像，每个监视图像都注释这型号和颜色。每个车型都标有五个属性，包括最大速度，排量，车门数量，座椅数量和汽车类型。对于每个车辆模型，也标注了5个拍摄视角，包括前面、后面、侧面、正面和背面。
项目连接：[链接](http://mmlab.ie.cuhk.edu.hk/datasets/comp_cars/index.html)
下载链接：得填写承诺书，然后发邮件，获取下载链接

8.Vehicle Type Classification Using a Semisupervised Convolutional Neural Network （IEEE Transactions on Intelligent Transportation Systems 2015）
数据库名称：BIT -Vehicle
论文：[链接](https://ieeexplore.ieee.org/abstract/document/7055873)
数据库描述：
包含9580个车辆图像和6种车型：轿车、运动型多用途车（SUV）、小型客车、卡车、公共汽车和小型货车。每种类型图像数目分别为5922、1392、883、558和476。该数据集中包含白天和夜间场景，且都是晴天场景，并且不存在噪声背景，雨、雪、人，其他车辆等。
下载地址：[链接](https://pan.baidu.com/s/1pKCr72V) 密码：29cf

9.Unsupervised Processing of Vehicle Appearance for Automatic Understanding in Traffic Surveillance [DICTA 2015]
数据库名称：VehicleGrouping
论文：[链接](https://medusa.fit.vutbr.cz/traffic/data/papers/2015-DICTA-VehiclesGrouping.pdf)
数据库描述:
监督监督收集数据并用于车辆的细粒度识别以及包括比例尺在内的摄像头校准，数据集包含大约140万张图片，包括多个摄像头进行拍摄，每个摄像头都用边框进行注释，论文很简略的介绍了数据，具体其概况得看数据怎么样。
项目网址：[链接](https://medusa.fit.vutbr.cz/traffic/research-topics/fine-grained-vehicle-recognition/unsupervised-processing-of-vehicle-appearance-for-automatic-understanding-in-traffic-surveillance/)
10. BoxCars: Improving Fine-Grained Recognition of Vehicles Using 3-D Bounding Boxes in Traffic Surveillance [IEEE T-ITS 2019]
数据库名称：BoxCars116k
论文：[链接](https://ieeexplore.ieee.org/document/8307405)
数据库描述：
该数据集由多个监控摄像头从各个角度拍摄116K车辆图像。具体信息在项目没介绍，明天我看论文
项目网址：[链接](https://medusa.fit.vutbr.cz/traffic/research-topics/fine-grained-vehicle-recognition/boxcars-improving-vehicle-fine-grained-recognition-using-3d-bounding-boxes-in-traffic-surveillance/)


