# White-Slog3-color-DaVinci-Resolve-nodes

&nbsp;

It is well known that Sony's S-Log3 gamma curve offers powerful color grading flexibility. If you are shooting with a Sony Alpha mirrorless camera released after 2020 that records 10-bit color — such as the a7 IV, a7S III, a7R V, a7C II, a1, a6700, ZV-E1, or ZV-E10 II — you will have plenty of room to shape the image in DaVinci Resolve. The footage holds up well to contrast, saturation, and creative stylization without breaking down as easily as 8-bit log. The S-Log3 workflow also plays an important role in modern film and hybrid shooting pipelines. That said, if you are an experienced colorist, this may be unnecessary, and you might not even use this node setup. But if you are just getting started with Sony mirrorless cameras, color grading can feel intimidating. This node structure is designed to save you time and give you a clean starting point. The test version centers on a single node set: "STD", a neutral, standard reconstruction that serves as your clean grading baseline. It is available in Simplified Chinese and English. The node was tested on the Sony a6700 & a7m4, and it should also work with other Sony Alpha mirrorless cameras that support 10-bit recording, though minor adjustments may be needed. All nodes assume an S-Log3 "expose to the right" workflow. When using a gray card, reference the 18% middle-gray exposure and overexpose neutral gray by approximately +1.3 to +1.7 EV to keep the shadows clean and maintain grading headroom.

索尼 S-Log3 伽马曲线在业内被公认为具备极强的调色灵活性。如果你使用的是 2020 年之后发布、支持 10-bit 录制的索尼 Alpha 无反相机，例如 a7 IV、a7S III、a7R V、a7C II、a1、a6700、ZV-E1 或 ZV-E10 II，在 DaVinci Resolve 中会有充足的调色空间。这类素材在对比度、饱和度和风格化处理上都比较耐调，不容易像 8-bit Log 素材那样出现断层或失真。 S-Log3 的工作流在现代影视拍摄流程中十分重要。当然，如果你是经验丰富的调色师，这套节点结构可能对你来说不重要，你甚至可能完全不会采用它。但如果你是刚开始接触索尼无反相机的调色小白，S-Log3 确实可能让人感到棘手。 分享这套节点的初衷，就是帮你节省时间，并提供一个干净、可靠的调色起点。 本次测试版包含一组节点：“STD”，用于相对中性的标准还原。这组节点提供简体中文和英文版本。节点测试基于索尼 a6700以及a7m4的素材，其他支持 10-bit 录制的索尼 Alpha 无反机型也可兼容，但可能需要根据机型和拍摄场景做轻微调整。 所有节点都基于 S-Log3 “向右曝光”的拍摄技巧。即以 18% 中性灰为曝光参考，将其适当过曝约 +1.3 至 +1.7 EV，以获得更干净的暗部并保留充足的调色余量。

### Before You Use This Node Set, Here Are a Few Things to Know

**What is a DaVinci Resolve color grading node?**

A node in DaVinci Resolve is the basic building block of the color page. Think of it as a processing station in an image pipeline. The image enters a node from the left, the node applies exposure, contrast, color, masks, noise reduction, LUTs, or other adjustments, and then passes the result to the next node on the right.

The advantage of working with nodes is that everything stays non-destructive and clearly organized. Your original footage is never permanently changed. Each node handles one part of the look, so if you want to revise something later, you just go back to that specific node instead of rebuilding the entire grade.

Common node types include serial nodes, parallel nodes, layer nodes, external nodes, and compound nodes.

**How is this different from a regular LUT, and why use nodes instead?**

A LUT is essentially a static RGB lookup table. It maps input colors to output colors without preserving any adjustment logic, and it cannot isolate different parts of the image. A DaVinci Resolve node tree, by contrast, is an editable, modular, and reorderable grading pipeline. Each node can handle exposure, contrast, white balance, selections, masks, curves, color space transforms, noise reduction, or stylization, and the nodes can be connected through serial, parallel, layer, or external structures to create a clear grading logic.

This means you can perform primary correction and color space conversion before a LUT, then make local fixes or stylistic tweaks after it. You can even use parallel nodes to work on skin tones, sky, and highlights independently without them interfering with each other. With a LUT, if the highlights clip, the shadows crush, or the skin tones turn green, you usually have no choice but to lower the overall intensity or swap the LUT entirely. With nodes, you can go back to the exact step that is causing the issue and correct it precisely.

A LUT can also behave very differently depending on exposure, camera log profile, and color space. A node tree lets you normalize the image first, then decide whether to apply a LUT and where to place it, which helps prevent the color space from being locked in too early or the creative intent from going off track. A node tree also acts like a flowchart, showing the full path from raw footage to final output. If a shot looks off, you can troubleshoot it node by node, and once you are happy with the result, you can save it as a PowerGrade for reuse.

**How do you import downloaded grading nodes into DaVinci Resolve?**

Downloaded node sets usually come as `.drx` files. To import one, open DaVinci Resolve and go to the Color page. In the upper-left corner, open the Gallery panel and make sure you are viewing a PowerGrade album rather than a regular stills album. Then drag the `.drx` file into the Gallery, or right-click inside the Gallery, choose Import, and select the file.

To use it, select your clip, find the imported preset in the Gallery, right-click it, and choose Apply Grade to apply the full node tree to the current clip. You can also right-click and choose Show Node Graph, then drag individual nodes or groups into your existing node tree. If you want to append the node tree after your current grade instead of replacing it, use Append Node Graph.

**What is the structure of this node set?**

This node set consists of eight independent, controllable grading nodes or node groups, arranged from front to back as follows: **CST IN**, **Denoise**, **White Balance**, **Contrast**, **Saturation**, **Grading**, **Effect**, and **CST OUT**.

**CST IN** converts the original S-Log3 footage from Sony mirrorless cameras into DaVinci Resolve’s intermediate color space and DaVinci Wide Gamut.

**Denoise** is a noise reduction node. It is disabled by default because most modern mirrorless cameras, when shot at native ISO in controlled lighting, produce fairly clean log footage. DaVinci Resolve’s noise reduction is extremely resource-intensive, and enabling it can make playback sluggish during grading. Even if you want a cleaner preview, I do not recommend leaving it on all the time. This is mainly about keeping your grading experience smooth.

**White Balance** is where you correct any white balance errors from the shoot. This group offers two approaches: a simpler slider-based adjustment and a more precise color wheel adjustment. The slider method is easier to pick up, but the color wheel method usually produces more natural results.

**Contrast** adjusts contrast after color space conversion, noise reduction, and white balance have been handled. You should tweak it based on the specific scene. Honestly, this is the node I use most often. If your footage is well exposed, sometimes a small adjustment here is all you need to make the image look solid. This node is also the core of the entire workflow. Always remember: **fix the light first, then shape the color**. Secondary stylization should sit on top of a balanced, neutral primary correction. This is also why some people feel their grades get progressively “muddy” — they skip this step and try to stylize before the image is properly balanced.

**Saturation** controls the overall saturation of the image. This group includes four sub-tools: **Dispersion**, **Channel Saturation**, **Six Vectors**, and **Color Optimization**.

1.  **Dispersion** helps reduce obvious chromatic fringing caused by lens optical limitations, especially purple or green edges. This adjustment is built around the Hue vs. Saturation curve.
    
2.  **Channel Saturation** adjusts saturation through color channels. If the image feels too flat, you can increase the key output percentage on this node to strengthen the effect.
    
3.  **Six Vectors** is another saturation tool. In most cases, you only need to use either Channel Saturation or Six Vectors, not both. Six Vectors works by dividing the color wheel into red, yellow, green, cyan, blue, and magenta segments, so you can boost greens, hold back blues, or refine skin tones without affecting the rest of the image. Its saturation algorithm is also more restrained and works well with the Density parameter, which affects both saturation and luminance relationships. This helps high-saturation areas feel more solid and less likely to look washed out or clipped. Compared with primary color wheels or channel-based saturation, Six Vectors tends to produce a deeper, more controlled look. If both tools feel less intuitive than the basic saturation slider on the primary wheels, you can simply disable them and stick with the primary saturation control.
    
4.  **Color Optimization** is an experimental adjustment I built to address the yellow-green and reddish-magenta tones that sometimes appear after S-Log3 conversion. It shifts yellow-greens slightly toward cyan and helps control red spill. For projects where color accuracy is critical, I would not recommend enabling this node. “Pleasing” and “accurate” are not always the same thing.
    

**Grading** provides three blank parallel nodes for secondary, zone-based adjustments, plus a **Styled LUT** node. Use the three parallel nodes for your own secondary work. If you have a creative LUT you like, drop it into the Styled LUT node to quickly apply a look. The influence of this LUT is controlled through the key output panel, and I have set the initial value relatively low so it does not overpower the image.

**Effect** includes three practical effects, all disabled by default.

1.  **soft/lim** applies a softer contrast curve. It increases contrast while making it harder to clip highlights or crush shadows.
    
2.  **Partition Sharpening** adds sharpening primarily to high-frequency detail areas rather than applying a flat, plastic-looking global sharpen.
    
3.  **Black Diffusion** simulates a black diffusion filter using DaVinci Resolve’s Glow effect. It softens highlights and gives them a dreamy, hazy quality.
    

**CST OUT** converts the image from DaVinci Resolve’s intermediate color space and DaVinci Wide Gamut into a standard Gamma 2.2 / Rec.709 output. Adjust this according to your monitoring environment and delivery requirements.

Gamma 2.2 and Gamma 2.4 are both common display curves for SDR video. The main difference is how they render shadows. Gamma 2.4 produces deeper shadows and stronger contrast, which aligns more closely with the BT.1886 standard for television monitors. It is better suited for dark-room monitoring and traditional broadcast delivery. Gamma 2.2 keeps the shadows slightly brighter and the overall image a bit flatter, which is closer to sRGB and how most computer displays and web videos appear.

Rec.709 is the standard HD SDR color space and is roughly equivalent to sRGB. It offers the best compatibility and is the most common choice for online video and broadcast delivery. Rec.709-A is not a “higher-end” color space. It is DaVinci Resolve’s compatibility option for the Apple ecosystem. It writes NCLC tags into the file so that QuickTime, iPhone, and macOS native players display the footage closer to what you see inside Resolve, reducing the washed-out or faded look that can sometimes appear on Macs. However, it is not a broadcast or industry-standard delivery format. If you are delivering for television, professional post, or any project that must strictly follow BT.1886 / Rec.709, use standard Rec.709 with Gamma 2.4.

I set the default output to Gamma 2.2 and Rec.709 because most mainstream mobile screens render SDR content close to sRGB / Gamma 2.2. Both Android and iPhone devices typically display ordinary SDR video within this framework. So if your goal is for the video to look natural on phones, social platforms, and the web, exporting as Rec.709 / sRGB with a Gamma 2.2 tag is usually a safe choice.

BT.2020 is a much wider color space that covers a significantly larger range of colors than Rec.709. It is typically used with 10-bit and HDR workflows. If you need to deliver HDR, you can adjust the CST OUT node accordingly. HDR has not yet become mainstream for most creators, so I will not go into detail here, but you can explore it further on your own.

**Can I use this node set with log footage from other camera brands or older Sony cameras?**

Different brands have different log curves, and this node set was developed specifically for S-Log3. Applying it directly to footage from other systems — such as Canon C-Log2 / C-Log3, Nikon N-Log, or DJI D-Log / D-Log M — will likely produce incorrect brightness and color mapping. You can try changing the input transform in CST IN to match another camera’s log profile, but the contrast and color response may still feel off. For that reason, I do not recommend it.

Older Sony models such as the A7S, A7S II, A7 III, and A6300 do not record 10-bit internally. If you apply this node set to 8-bit log footage, large areas of smooth color — especially skies — will often show banding. That is a limitation of 8-bit color, not necessarily the node set itself.

**在使用这套节点前，你需要知道以下几点：**

&nbsp;

1.  **什么是达芬奇调色节点？  
    **  
    达芬奇调色节点是 DaVinci Resolve 调色页面里的基本处理单元。你可以把它理解成图像处理流水线上的一个个“处理盒子”。原始素材的画面从左边进入节点，节点对它做曝光、对比度、色彩、局部遮罩、降噪、LUT 等操作，再从右边输出给下一个节点。节点的优势在于非破坏性和清晰的传递结构，原始素材不会被直接修改，每个节点只负责一部分调整，后续想改哪一步，就回到对应节点修改，而不需要推翻整个调色。  
    <br/>常见节点类型有：**串行节点、并****行节点、**图层节点、****外部节点、**复合节点。  
    ******
2.  **相比形式更为常见的调色LUT（.cube文件或.3DL文件）达芬奇调色节点有哪些不同和优势？  
    **  
    LUT本质上是一个静态的RGB映射表，它把输入色彩直接转换成输出色彩，不保留任何调整逻辑，也无法区分画面中的不同区域；而达芬奇调色节点是一个可编辑、可拆分、可重排的处理流程，每个节点都能独立承担曝光、对比度、白平衡、选区、遮罩、曲线、色彩空间转换、降噪、风格化等任务，并且节点之间可以通过串行、并行、图层、外部等结构建立清晰的逻辑关系，这意味着你可以在LUT之前做一级校色和色彩空间转换，在LUT之后做局部修复和风格微调，甚至通过并行节点同时处理肤色、天空、高光而不互相干扰。相比之下，LUT一旦套用，如果高光被平削、暗部被裁切、肤色偏绿，通常只能整体降低强度或干脆换掉，而节点允许你回到具体步骤精确修正。此外，同样的LUT套在不同曝光、不同相机Log、不同色彩空间的素材上结果可能差别很大，而节点可以先做一级校色和色彩空间统一，再决定要不要挂LUT以及挂在什么位置，从而避免色域被提前锁死或风格表达错误。节点树还能像流程图一样展示从原始素材到最终输出的完整路径，某个镜头出问题可以逐节点排查，确认有效后也能保存为PowerGrade复用。  
    <br/><br/>
3.  **如何在达芬奇当中导入下载好的调色节点？**  
    下载好的调色节点通常以 .drx 文件形式提供，导入时先打开达芬奇并切换到“调色”页面，在左上角找到“画廊”面板，确认当前选中的是 PowerGrade 集而不是普通静帧集，然后直接把 .drx 文件拖进画廊空白处，或者在画廊里右键选择“导入”并选中该文件即可完成导入；使用时选中目标片段，在画廊中找到导入的预设，右键点击“应用调色”即可把完整节点树应用到当前片段，也可以右键选择“显示节点图”，把其中某个或某几个节点单独拖进当前节点树中，若只是想附加到现有调色后面，还可以使用“附加节点图”  
    <br/>
4.  **这组节点下有哪些结构？  
    **这组节点一共包含了8个独立的可控的调色节点（集），从前到后分别是“CST IN”(输入色彩空间转换）、“Denoise”（降噪节点）、“White Balance”（白平衡节点）、“Contrast”（一级对比度调整）、“Saturation”（饱和度调整集）、“Grading”（颜色分级/二级调色、风格化组）、“Effect ”（效果集）以及“CST OUT”（输出色彩空间转换）  
    **CST IN**的作用是将索尼无反相机拍摄的原始Slog3素材的色彩空间以及伽马曲线转化为达芬奇调色中间片以及达芬奇宽色域  
    **Denoise**的作用是降噪，该节点默认是关闭的（因为大部分现代的无反相机在可控的光线条件下以原生增益拍摄的灰片一般不会有大量的噪点，达芬奇的降噪功能极其占用系统资源，添加降噪效果后后续调色的预览会变得卡顿，所以即使你非常需要看到降噪后相对干净的预览画面，我也不推荐你一直开启它，这事关你的调色体验）  
    **White Balance**的作用显而易见，是预留给你后期修正素材拍摄时错误的白平衡的，这个节点集下包含了两种白平衡调节方式，一种是更容易上手的滑块调整、一种则是相对麻烦的色轮调整。前者调整的效果往往不如后者自然。  
    **Contrast**的作用是对完成色彩空间转换、降噪以及白平衡调整后的素材调整对比度，可根据具体拍摄场景进行调节。坦言之，这个节点是我平时使用频率最高的节点。如果你导入的素材足够理想，甚至很多时候你只需要在这个节点上微调，画面观感就已经足够好。这一节点也是整个调整流程的核心，一定要牢记“先调光、后调色”的原则，二级风格化调整需要建立在对比度适中、偏中性的一级还原的基础上。这也是为什么一些人认为他们的素材越调越“脏”，因为他们没有遵循这一重要原则。  
    **Saturation**的作用是用于控制画面整体的饱和度，这一个节点集下包含了“Dispersion”（去除镜头色散节点）、“Channel saturation”（颜色通道饱和度调整工具）、“Six vectors"(颜色六矢量切片器饱和度调整工具）、以及“Color Optimization”（色彩优化节点次集）。  
    （1）“Dispersion”很好理解，就是用于消除视频拍摄时因镜头本身光学素质缺陷导致的过于明显的紫边，这一调整基于色相VS饱和度曲线  
    （2）“Channel saturation”是通过颜色通道进行饱和度调整的节点，如果你觉得当前画面的饱和度过低，不符合你的调色预期，可以在节点键选项下将键输出的百分比适当调大  
    （3）“Six vectors"与“Channel saturation”同为调整饱和度的工具，一般情况下只通过二者其中一种方式来对画面饱和度进行调整就足够了，这一节点与“Channel saturation”节点对饱和度产生的影响有所不同，六矢量切片器中的饱和度是面向色相分段的饱和度控制，它把色轮分成红、黄、绿、青、蓝、品等独立色段，可以只提升绿色、只压暗蓝色、只校正肤色段，而不影响其他颜色；同时它的饱和度算法更克制，常配合“密度”参数一起使用，密度会同时影响颜色的饱和度和明度关系，让高饱和区域更扎实、不容易发灰或溢出。相比校色轮以及通过颜色通道来控制饱和度，六矢量切片器调整过后的画面明显更“深沉”。当然，如果你觉得以上两个工具对于你来说操作都不如一级校色轮上的饱和度调整滑块工具那样直观，你也可以选择清除这两个节点的调整并沿用一级校色轮的饱和度调整工具。  
    （4）“Color Optimization”是我对Slog3还原后普遍出现的黄绿色以及红品色观感不佳做出的一些实验性的调整和优化，基于色相VS饱和度曲线，它会让画面当中的黄绿色更偏青且红色溢出得到一定的控制与缓解，在一些对于颜色准确度有非常严苛要求的调色项目中，我并不建议你启用这一节点，因为“好看”与“准确”是两码事。  
    **Grading**节点集下预留了三个分区调整的空白并行节点和一个“Styled LUT”节点，可在这三个空白并行节点上执行你的二级分区调整。此外，如果你有自己的风格化LUT，将其拖放至“Styled LUT”节点上可以帮助你快速完成画面的风格化。需要注意的是，这一节点同样是用键输出界面来控制LUT对画面的影响程度，我设置的初始值相对低。  
    **Effect**节点集下包含了三个实用的效果，默认为关闭的状态  
    （1）**“soft/lim”**柔和对比度曲线：更柔和的对比度调整曲线，增加画面对比度的同时不容易高光溢出和暗部拆切  
    （2）**“Partition Sharpening”**分区锐化：针对画面高频细节区域进行锐化处理，并非“塑料感”的全局锐化  
    （3）**“Black Diffusion”**数字黑柔滤镜：通过达芬奇内置的“发光”效果模拟黑柔滤镜对于高光部分的柔化处理，会让画面的高光部分变得梦幻、朦胧  
    **CST OUT**的作用是将达芬奇调色中间片以及达芬奇宽色域转化为标准的伽马2.2和Rec.709色域输出，可根据你的监看环境以及输出标准进行对应的调整。
    
    伽马 2.2 和 2.4 都是 SDR 视频里常见的显示曲线，核心差别是暗部亮度。2.4 暗部更沉、对比更强，接近 BT.1886 电视监视器标准，适合暗环境监看和传统电视交付；伽马2.2 暗部更亮、整体更“平”，更接近 sRGB 和多数电脑显示器、网页视频的显示习惯。
    
    Rec.709 是高清 SDR 标准色域，约等于 sRGB，兼容性最好，网络视频、电视交付最常用。Rec.709-A 不是更“高级”的色域，而是达芬奇为苹果生态做的兼容方案，它在文件里写入 NCLC 标签，让 QuickTime、iPhone、Mac 自带播放器更接近达芬奇预览，避免在 Mac 上发灰、发白。 但它不是广播或行业标准，若交付电视台、专业后期或必须严格符合 BT.1886/Rec.709 的项目，仍应使用标准 Rec.709 + Gamma 2.4。至于为什么我在该节点的默认值设定成伽马2.2以及Rec.709色域，是因为主流手机屏幕的 SDR 显示曲线通常接近 sRGB / Gamma 2.2，安卓和 iPhone 在播放普通 SDR 视频时大多也按这个体系来呈现。所以如果你希望视频在手机、网页、社交平台上看更自然，输出色彩空间设为 sRGB 或 Rec.709，伽马标签设为 2.2 ，通常是比较稳妥的选择。
    
    BT.2020 则是更大的色域容器，覆盖颜色范围远大于 Rec.709，通常配合 10bit 和 HDR 输出流程使用。如果你要输出HDR的视频，只需要在该节点做对应的修改即可，由于HDR内容尚未成为主流，在此不做过多赘述，相关知识可自行了解。
    
5.  如果我是别的品牌的无反相机拍摄的灰片素材或者索尼早期机型拍摄的LOG素材，可以使用这套节点吗？  
    首先，不同品牌的灰片曲线存在明显差异，这套节点基于Slog3曲线调整开发，直接套用其他品牌相机的素材（如佳能Clog2/3、尼康N-LOG、大疆D-log/D-logM）会导致画面亮度和色彩无法以正确的方式被映射，尽管你可以通过修改**CST IN**(色彩空间转换输入）对其他品牌相机拍摄的LOG素材进行转换，画面的对比度以及颜色仍有可能不正确，所以不建议这样做。  
    索尼早期机型，如A7S/A7S2/A7M3/A6300等机型不具备10bit机内记录能力，直接套用后，如果画面当中包含有例如天空等大面积纯色渐变场景，8bit的色彩往往不可避免地会出现断层的情况。