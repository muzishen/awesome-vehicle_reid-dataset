<html lang="en"><head>
    <meta charset="UTF-8">
    <title></title>
<style id="system" type="text/css">h1,h2,h3,h4,h5,h6,p,blockquote {    margin: 0;    padding: 0;}body {    font-family: "Helvetica Neue", Helvetica, "Hiragino Sans GB", Arial, sans-serif;    font-size: 13px;    line-height: 18px;    color: #737373;    margin: 10px 13px 10px 13px;}a {    color: #0069d6;}a:hover {    color: #0050a3;    text-decoration: none;}a img {    border: none;}p {    margin-bottom: 9px;}h1,h2,h3,h4,h5,h6 {    color: #404040;    line-height: 36px;}h1 {    margin-bottom: 18px;    font-size: 30px;}h2 {    font-size: 24px;}h3 {    font-size: 18px;}h4 {    font-size: 16px;}h5 {    font-size: 14px;}h6 {    font-size: 13px;}hr {    margin: 0 0 19px;    border: 0;    border-bottom: 1px solid #ccc;}blockquote {    padding: 13px 13px 21px 15px;    margin-bottom: 18px;    font-family:georgia,serif;    font-style: italic;}blockquote:before {    content:"C";    font-size:40px;    margin-left:-10px;    font-family:georgia,serif;    color:#eee;}blockquote p {    font-size: 14px;    font-weight: 300;    line-height: 18px;    margin-bottom: 0;    font-style: italic;}code, pre {    font-family: Monaco, Andale Mono, Courier New, monospace;}code {    background-color: #fee9cc;    color: rgba(0, 0, 0, 0.75);    padding: 1px 3px;    font-size: 12px;    -webkit-border-radius: 3px;    -moz-border-radius: 3px;    border-radius: 3px;}pre {    display: block;    padding: 14px;    margin: 0 0 18px;    line-height: 16px;    font-size: 11px;    border: 1px solid #d9d9d9;    white-space: pre-wrap;    word-wrap: break-word;}pre code {    background-color: #fff;    color:#737373;    font-size: 11px;    padding: 0;}@media screen and (min-width: 768px) {    body {        width: 748px;        margin:10px auto;    }}</style><style id="custom" type="text/css"></style></head>
<body><p><strong>CSDN:</strong> <a href="https://blog.csdn.net/qq_17403617">欢迎关注</a>
    导语：这是腾讯的一篇行人ReID，由粗到细的金字塔重识别框架。收录于2019CVPR。

</p>
<p><strong> Paper:</strong> <a href="http://openaccess.thecvf.com/content_CVPR_2019/html/Zheng_Pyramidal_Person_Re-IDentification_via_Multi-Loss_Dynamic_Training_CVPR_2019_paper.html">Pyramidal Person Re-IDentification via Multi-Loss Dynamic Training</a>
<strong>Code:</strong>还没有开源

</p>
<h3>Abstract</h3>
<p>大多数现有的重新识别(Re-ID)方法高度依赖于能够使图像彼此对齐的精确边界框。然而，由于现实场景的挑战，现有的检测模型往往产生不准确的边界框，不可避免地会降低现有的reid算法的性能。在本文中，我们提出了一个新颖的由粗到细的金字塔模型来放宽边界盒的需求，它不仅整合了局部和全局信息，而且整合了它们之间的渐进线索。金字塔模型能够在不同的尺度上匹配，然后搜索相同身份的正确图像，即使图像对没有对齐。此外，为了学习识别性身份表示，我们探索了一种<strong>动态训练方案</strong>来无缝地统一两个损失并提取它们之间适当的共享信息。实验结果表明，该方法在三组数据集上取得了较好的效果。特别地，我们的方法在最具挑战性的CUHK03数据集上比目前最好的方法高出9:5%。

</p>
<h3>Introduction</h3>
<p>由于基于部件的模型存在问题，且在培训中存在困难，现有方法的性能改进空间有限. 众所周知，在许多计算机视觉任务中，基于部分的模型通常可以获得很好的性能，因为这些模型对一些不可避免的挑战(如遮挡和部分变化)具有潜在的健壮性。实际上，person Re-ID在实际应用中的性能受到这些挑战的严重影响。因此，最近提出的基于部件的卷积基线(PCB)[24]可以达到最先进的结果。PCB是简单但非常有效，甚至可以超越其他学习零件模型。然而，在PCB中，直接将骨干网映射成固定数量的部件，严格限制了进一步提高性能的能力。它至少有两个主要的缺点，但不限于:<strong>1)整体性能严重依赖于一个强大而健壮的行人检测模型输出一个精确的边界框，否则零件不能很好的对齐。然而，在大多数具有挑战性的场景中，现有的检测模型不足以做到这一点。2)全局信息作为识别和识别的重要线索，在该模型中被完全忽略，而全局特征通常对细微的视图变化和内部变化具有很强的鲁棒性。</strong>

</p>
<h4>图片证明缺陷</h4>
<p><img src="https://img-blog.csdnimg.cn/20191229120111213.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzE3NDAzNjE3,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述">最近的研究[10,9]表明，多任务学习能够通过提取任务之间适当的共享信息来实现高级性能。在不损失一般性的情况下，术语“损失”和“任务”将交替使用。事实上，许多现有的reid方法[26]也受益于多损耗方案来提高性能。通常情况下，大多数多任务方法选择在整个训练过程中使用固定的平衡参数来权衡损失。<strong>1)性能高度依赖于合适的参数，而选择合适的参数无疑是一项劳动密集型、技巧性强的工作。2)当模型逐步更新时，不同任务的难度实际上是变化的，导致不同迭代的适当参数确实存在差异。3)更重要的是，由于具体的考虑，不同损失的抽样策略通常是不同的。例如，对三重态损耗的硬采样会抑制识别损耗的另一任务的作用。</strong>
    针对上述问题，本文提出了一种基于骨干网提取的特征图的coarse-to-fine pyramidal modle，用于人的再识别。首先，金字塔实际上是一组三维的子地图，具有特定的由粗到精的架构，其中每个成员捕获不同空间尺度的区别信息。然后，使用卷积层来减少金字塔中每个分支的特征维数。第三，对于每个分支，将一个softmax函数的识别损失独立地应用于一个将特征作为输入的全连接层。此外，所有分支的特征将被连接起来形成一个身份表示，定义一个三重损失来学习更多的鉴别特征。为了使这两种损失能够平滑地融合在一起，研究了一种具有两种采样策略的动态训练方案来优化深度神经网络的参数。最后，将该方法应用于人脸图像的匹配、检索和再识别。
</p>
<h4>本文的主要贡献：</h4>
<p>1)为了放宽对强检测模型的要求，我们提出了一种新颖的由粗到细的金字塔模型，该模型不仅融合了局部和全局信息，而且融合了局部和全局信息之间的渐进线索。
2)为了最大限度地利用不同的损失，我们探索了一种动态训练方案，将两个损失无缝地统一起来，提取它们之间适当的共享信息，以学习区别身份表示。
3)所提出的方法在三个数据集上都达到了最新的结果，最重要的是，我们的方法在CUHK03数据集上超过了目前最好的方法9:5%

</p>
<h3>方法</h3>
<h4>首先看一下模型</h4>
<p><img src="https://img-blog.csdnimg.cn/20191229120454893.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzE3NDAzNjE3,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述">作者说：这个模型不仅整合了地方和全球的信息，而且还整合了它们之间的<strong>逐步过渡</strong>过程.
</p>
<h4>1. 金字塔分支</h4>
<p>首先,我们将特征图映射到n个部分根据H, 因此每个基本部分是我大小C,(H /n),  w .假设H/n可以整除。因此,我们的模型根据以下规则:
1)在底部水平(l = 1)的金字塔,有n个数量的分支对应于一个基本部分。
2)这一级的分支比上一级的分支多一个相邻的基本部分。
3)所有层的滑动步长设置为1。这意味着当前级别的分支数量只比前一级别少一个。
4)在金字塔的顶层(l = n)，只有一个分支，即原始的特征图 M。
因此，我们假设P是金字塔模型P{l,k}第l层的第k个子图，定义为：
<img src="https://img-blog.csdnimg.cn/20191229120941235.png" alt="在这里插入图片描述">其中1:C表示从索引1到索引C的所有元素都被选中。显然，P是一组具有特定的由粗到精架构的三维子映射，其中每个成员捕获不同空间尺度的区别信息。此外，金字塔模型包含全局特征和基于部件的model: 原始PCB（看之前论文分享）。而我们很容易知道，在P中总共有<img src="https://img-blog.csdnimg.cn/20191229121131800.png" alt="在这里插入图片描述">个分量，第l层有(n - l  + 1)个分量，其中的水平指数是由细到粗的。提出的体系结构的细节如图2所示。

</p>
<h4>2. 基本模块</h4>
<p><img src="https://img-blog.csdnimg.cn/20191229121310810.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzE3NDAzNjE3,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述">
提出GAP+GMP 的操作单元。
总的loss = soft loss + triplet loss

</p>
<h4>3.动态weight 更新（下一次单独开一篇细说）</h4>
<p><img src="https://img-blog.csdnimg.cn/20191229121518190.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzE3NDAzNjE3,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述">
</p>
<h3>Exp:</h3>
<h4>Compare SOTA</h4>
<p><img src="https://img-blog.csdnimg.cn/20191229121712691.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzE3NDAzNjE3,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述"><img src="https://img-blog.csdnimg.cn/20191229121720962.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzE3NDAzNjE3,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述">
<img src="https://img-blog.csdnimg.cn/20191229121738942.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzE3NDAzNjE3,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述">

</p>
<h4>Ablation Exp</h4>
<p><img src="https://img-blog.csdnimg.cn/20191229121811345.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzE3NDAzNjE3,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述">
</p>
<h4>实验貌似没有说这个动态更新提点多少。这块我再仔细研究一下。</h4>
<h3>点个赞 支持下，谢谢！！！！</h3>
</body></html>