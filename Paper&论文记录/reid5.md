<html lang="en"><head>
    <meta charset="UTF-8">
    <title></title>
<style id="system" type="text/css">h1,h2,h3,h4,h5,h6,p,blockquote {    margin: 0;    padding: 0;}body {    font-family: "Helvetica Neue", Helvetica, "Hiragino Sans GB", Arial, sans-serif;    font-size: 13px;    line-height: 18px;    color: #737373;    margin: 10px 13px 10px 13px;}a {    color: #0069d6;}a:hover {    color: #0050a3;    text-decoration: none;}a img {    border: none;}p {    margin-bottom: 9px;}h1,h2,h3,h4,h5,h6 {    color: #404040;    line-height: 36px;}h1 {    margin-bottom: 18px;    font-size: 30px;}h2 {    font-size: 24px;}h3 {    font-size: 18px;}h4 {    font-size: 16px;}h5 {    font-size: 14px;}h6 {    font-size: 13px;}hr {    margin: 0 0 19px;    border: 0;    border-bottom: 1px solid #ccc;}blockquote {    padding: 13px 13px 21px 15px;    margin-bottom: 18px;    font-family:georgia,serif;    font-style: italic;}blockquote:before {    content:"C";    font-size:40px;    margin-left:-10px;    font-family:georgia,serif;    color:#eee;}blockquote p {    font-size: 14px;    font-weight: 300;    line-height: 18px;    margin-bottom: 0;    font-style: italic;}code, pre {    font-family: Monaco, Andale Mono, Courier New, monospace;}code {    background-color: #fee9cc;    color: rgba(0, 0, 0, 0.75);    padding: 1px 3px;    font-size: 12px;    -webkit-border-radius: 3px;    -moz-border-radius: 3px;    border-radius: 3px;}pre {    display: block;    padding: 14px;    margin: 0 0 18px;    line-height: 16px;    font-size: 11px;    border: 1px solid #d9d9d9;    white-space: pre-wrap;    word-wrap: break-word;}pre code {    background-color: #fff;    color:#737373;    font-size: 11px;    padding: 0;}@media screen and (min-width: 768px) {    body {        width: 748px;        margin:10px auto;    }}</style><style id="custom" type="text/css"></style></head>
<body><pre><code>    导语：这是一篇金字塔+分块的结合论文，Horizontal Pyramid Matching (HPM), AAAI2019接收。</code></pre>
<p><strong>Paper：</strong> <a href="https://www.aaai.org/ojs/index.php/AAAI/article/view/4842">Horizontal Pyramid Matching for Person Re-identification</a>
<strong>Code：</strong><a href="https://github.com/OasisYang/HPM">代码</a>

</p>
<h3>Abstract</h3>
<p>尽管近年来取得了显著的进展，但仍有一些失败的案例，如缺少鉴别性的身体部位。为了减少这种情况，我们提出了一种简单而有效的水平金字塔匹配(Horizontal Pyramid Matching, HPM)方法来充分利用给定人员的各种部分信息，这样即使缺少某些关键部分，仍然可以识别正确的人员候选。在HPM中，我们做出了以下贡献来为Re-ID任务生成更健壮的特征表示:
1)我们学会了在不同的水平金字塔尺度上使用部分特征表示进行分类，这成功地增强了各个人员部分的识别能力;
2)我们利用平均汇集策略和最大汇集策略，以全局-局部的方式考虑个体特异性的歧视信息。
为了验证建议的HPM的有效性，我们在三个流行的基准上进行了大量的实验，包括Market-1501、DukeMTMC-ReID和CUHK03。特别是，我们在这些基准上取得了83.1%、74.5%和59.7%的SOTA。

</p>
<h3>Introduction</h3>
<p>现有的DL 只利用全局人员特性，而全局人员特性对缺少的关键部分非常敏感。为了解决这一问题，近年来许多研究方法都侧重于学习部分判别特征表示。这些方法通常利用像身体大小这样的全局特性和像衣服标志这样的局部特征结合起来ReID。
根据区域生成方案，可以将它们分为三种类型。在第一种类型中，通过估计和提取像姿势或身体标志这样的先验知识来定位识别区域。然而，在这种情况下，reid的性能高度依赖于姿态或landmark估计模型的鲁棒性。姿态估计误差等非预期误差对识别结果有很大影响。
第二种是基于注意力的方法，重点通过对特征图中高激活区域的定位，自适应地提取感兴趣区域。然而，所选区域缺乏语义解释。
第三种方法通过假设图像完全对齐，将深度特征图裁剪成预定义的斑块或条纹因此很容易被异常值引入错误。
<strong>为了有效的学习有鉴别力的特征</strong>，我们提出了一种简单而有效的方法，即水平金字塔匹配(HPM)，以消除未预料到的正面和未对齐情况所带来的负面影响。我们的HPM旨在以更健壮和更有效的方式同时利用一个人的全局和部分信息来完成reid任务。具体而言，我们的贡献如下:
1.我们将深度特征图水平切片到多个multiple spatial bins中，使用不同的金字塔尺度进行池化操作，即水平金字塔池(HPP)，并学习对不同金字塔尺度的multiple spatial bins输出的特征进行独立分类。直观地说，使用多个尺度的bins将包含一个松弛距离，以减轻偏差导致的离群值问题。同时，多尺度信息的独立学习将增强在各个尺度特定的人身上所习得的识别性信息。
2.我们将每个分区中的平均池和最大池化功能结合起来。特别是平均池能够感知每个空间bin的全局信息，并考虑背景上下文。而最大池化目标则提取出最具鉴别性的信息，而忽略那些干扰信息，主要来自相似的服装或背景。将它们结合起来，从而在全局-局部方式上平衡这两种战略的有效性。我们评估了我们提出的方法在三个主流的人重新识别数据集，market1501,DukeMTMC-ReID和CUHK03(新的协议)。实验结果表明，我们的模型通过端到端可训练的方法击败了大多数现有的方法。

</p>
<p><img src="https://img-blog.csdnimg.cn/2019121720085872.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzE3NDAzNjE3,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述">
我们用图1中所示的一个示例来说明我们的HPM。我们首先提取具有多个卷积层的给定图像的特征表示，然后对不同金字塔尺度的特征图进行水平切片。然后利用每个部分的全局平均池和最大池生成的特征表示分别进行reid。通过以这种方式学习HPM，可以更有效地增强部分鉴别能力，克服现有解决方案的不足(如对关键部件的缺失或偏差敏感)

</p>
<h3>Network</h3>
<p><img src="https://img-blog.csdnimg.cn/20191217201034130.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzE3NDAzNjE3,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述">
</p>
<h3>训练细节</h3>
<p>为了获得足够的人物图像信息和合适的水平金字塔池大小的特征图，我们将所有的图像大小调整为384x128。对于骨干网，我们使用在ImageNet上预先训练的权值初始化的Resnet50 。我们删除了最后的全连接层和平均池化层，并设置了最近的conv4 1从2到1的步长。通过水平翻转和归一化增强训练图像。批量大小设置为64，我们训练模型为60 epoch。设置基础学习率为0.1，在40个epoch后衰减为0.01。注意，所有预训练的Resnet层的学习率都设置为0.1 x基本学习率。采用0.9动量的随机梯度下降法(SGD)对每个小批数据进行更新。在推理时，我们将经过1x1卷积运算后的特征向量拼接在一起，生成查询图像的特征表示。将原始图像和水平翻转图像的特征相加，归一化特征进行检索评价。我们的模型在Pytorch平台上实现，并使用两个NVIDIA TITAN X gpu进行训练。
</p>
<h3>Compare SOTA</h3>
<p><img src="https://img-blog.csdnimg.cn/20191217201115819.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzE3NDAzNjE3,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述">
</p>
<h4>w/o HPM的ablation结果，R1 有6个点的提升</h4>
<p><img src="https://img-blog.csdnimg.cn/20191217201225244.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzE3NDAzNjE3,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述">
</p>
<h4>Ablation study</h4>
<p><img src="https://img-blog.csdnimg.cn/20191217201338736.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzE3NDAzNjE3,size_16,color_FFFFFF,t_70" alt="PS代表下图的">
<img src="https://img-blog.csdnimg.cn/2019121720142090.png" alt="在这里插入图片描述"><strong>能看出来4个尺度最好，分别是24 X8,12X8, 6X8, 3X8。 然后GAP+GMP最好。</strong>
</p>
</body></html>