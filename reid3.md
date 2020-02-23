<html lang="en"><head>
    <meta charset="UTF-8">
    <title></title>
<style id="system" type="text/css">h1,h2,h3,h4,h5,h6,p,blockquote {    margin: 0;    padding: 0;}body {    font-family: "Helvetica Neue", Helvetica, "Hiragino Sans GB", Arial, sans-serif;    font-size: 13px;    line-height: 18px;    color: #737373;    margin: 10px 13px 10px 13px;}a {    color: #0069d6;}a:hover {    color: #0050a3;    text-decoration: none;}a img {    border: none;}p {    margin-bottom: 9px;}h1,h2,h3,h4,h5,h6 {    color: #404040;    line-height: 36px;}h1 {    margin-bottom: 18px;    font-size: 30px;}h2 {    font-size: 24px;}h3 {    font-size: 18px;}h4 {    font-size: 16px;}h5 {    font-size: 14px;}h6 {    font-size: 13px;}hr {    margin: 0 0 19px;    border: 0;    border-bottom: 1px solid #ccc;}blockquote {    padding: 13px 13px 21px 15px;    margin-bottom: 18px;    font-family:georgia,serif;    font-style: italic;}blockquote:before {    content:"C";    font-size:40px;    margin-left:-10px;    font-family:georgia,serif;    color:#eee;}blockquote p {    font-size: 14px;    font-weight: 300;    line-height: 18px;    margin-bottom: 0;    font-style: italic;}code, pre {    font-family: Monaco, Andale Mono, Courier New, monospace;}code {    background-color: #fee9cc;    color: rgba(0, 0, 0, 0.75);    padding: 1px 3px;    font-size: 12px;    -webkit-border-radius: 3px;    -moz-border-radius: 3px;    border-radius: 3px;}pre {    display: block;    padding: 14px;    margin: 0 0 18px;    line-height: 16px;    font-size: 11px;    border: 1px solid #d9d9d9;    white-space: pre-wrap;    word-wrap: break-word;}pre code {    background-color: #fff;    color:#737373;    font-size: 11px;    padding: 0;}@media screen and (min-width: 768px) {    body {        width: 748px;        margin:10px auto;    }}</style><style id="custom" type="text/css"></style></head>
<body><pre><code>导语：这篇论文是PCB之后孙老师团队又一篇部件对齐网络，为了解决行人reid中遮挡问题。旷视出品。</code></pre>
<p><strong>Paper:</strong> <a href="http://openaccess.thecvf.com/content_CVPR_2019/html/Sun_Perceive_Where_to_Focus_Learning_Visibility-Aware_Part-Level_Features_for_Partial_CVPR_2019_paper.html">Perceive Where to Focus: Learning Visibility-aware Part-level Features for Partial Person Re-identification</a>
<strong>Code:</strong> 暂时没有github

</p>
<h3>Abstract:</h3>
<p>本文研究了人员再识别任务中的一个现实问题:,<strong>部分re-ID</strong>。在部分重新识别场景下，图像可能包含对行人的部分观察。如果我们直接将局部的行人图像与整体的行人图像进行比较，这种极端的空间偏差会大大降低学习图像的识别能力。提出了一种视觉感知部分模型(Visibility-aware Part Model，VPM)，该模型通过自我监控来学习感知区域的可见性。可见性感知允许VPM提取区域级别的特征，并将两个图像集中在它们的共享区域(在两个图像上都可见)上进行比较。VPM在提高部分重新标识的准确性方面获得了两倍的好处。一方面，与学习全局特性相比，VPM学习区域级特性并从细粒度信息中获益。另一方面，通过可视性感知，VPM能够估计两个图像之间的共享区域，从而抑制空间的不一致。实验结果表明，我们的方法显著地改进了学习表示，获得的精度与目前的水平相当。

</p>
<h3>Introduction</h3>
<p>行人重识别一个很大的问题：<strong>摄像机未能捕获整体行人</strong>
直观地说，部分重新id增加了正确检索的难度。通过分析，我们发现，与整体的人的本我相比，部分的人的本我提出了两个更独特的挑战，如图1所示。
<img src="https://img-blog.csdnimg.cn/20191211122455530.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzE3NDAzNjE3,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述">
首先，部分re-ID加剧了probe图像与gallery图像之间的空间错位。在整体re- ID设置下，空间错位主要来源于行人的关节运动和视角的变化。在部分re-ID设置下，即使从相同视点捕获两个具有相同姿态的行人，两幅图像仍然存在严重的空间错位(图1 (a))。

</p>
<p>第二，当我们直接将部分行人与整体行人进行比较时，整体行人中未共享的身体区域会成为分散注意力的噪音,而不是识别力的线索。我们注意到，同样的情况也发生在任何两个比较的图像包含不同比例的整体行人
(图1 (b))。

</p>
<p><strong>因此，作者提出：</strong>
提出了一种用于部分重建id的可见性感知部件模型(VPM)。如图1 (c)所示，VPM通过关注与部分re-ID相关的共享区域来避免或缓解这两种独特的困难。更具体地说，我们首先在整体人的图像上定义一组区域。在训练中，给定部分行人图像，VPM学习在卷积特征图上定位所有预定义区域。在定位每个区域之后，VPM感知哪些区域是可见的，并学习区域级的特征。在测试过程中，给定要比较的两幅图像，VPM首先计算它们共享区域之间的局部距离，然后得出总体距离。

</p>
<p>VPM在提高部分重新标识的准确性方面获得了两倍的好处。<strong>一方面，与学习全局特性相比，VPM学习区域级别的特性，因此受益于细粒度信息，这与整体person re-ID的情况类似[23,12]。</strong> 
<strong>另一方面，利用视觉感知，VPM能够对两幅图像之间的共享区域进行估计，从而抑制空间不一致以及来自未共享区域的噪声。</strong>
实验结果证实，与全局特征学习基线[34]相比，VPM在局部特征识别精度上有显著提高，与强局部卷积基线[23]相比也有显著提高。取得的成绩与目前的水平相当。

</p>
<p>此外，VPM具有运用自我监督来学习区域可见性意识的特点。我们从整体图像中随机裁剪部分行人图像，并自动生成区域标签，产生所谓的自我监督。自我监督使VPM能够学习定位预定义区域。它还有助于VPM在特征学习过程中关注可见区域，这对于学习特征的识别能力至关重要，如4.4节所述。

</p>
<p><strong>网络结构图</strong>

</p>
<p><img src="https://img-blog.csdnimg.cn/20191211122913212.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzE3NDAzNjE3,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述"><strong>与SOTA比较结果如下：</strong>

</p>
<p><img src="https://img-blog.csdnimg.cn/20191211122945577.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzE3NDAzNjE3,size_16,color_FFFFFF,t_70" alt="在这里插入图片描述">
</p>
</body></html>