# FreeGo什么
没有人提供知识的Go程序。使用MCTS（但没有蒙特卡罗播报）和深度残差卷积神经网络堆栈。

这是Alpha Go Zero论文“ 精通无人类知识的棋局 ”中描述的系统的忠实重新实现。出于所有目的和目的，它是一个开源的AlphaGo Zero。

等一下
如果您想知道问题所在：您仍然需要网络权重。此存储库中没有网络权重。如果您设法获得AlphaGo零权重，则该程序将具有同等强度，前提是您还获得了一些张量处理单元。缺少那些TPU，我建议使用顶级的GPU-它并不完全相同，但是结果仍然是引擎要比顶尖的人强得多。

给我重量
在商品硬件上，重新计算AlphaGo零权重大约需要1700年。

发布该程序的原因之一是，我们正在进行公共的，分布式的工作以重复该工作。共同努力，尤其是从小规模开始，一个良好的网络将花费不到1700年的时间（您可以将其引入该程序，突然变得强大）。

我想帮忙
使用自己的硬件
您需要一台带有GPU的PC，即由NVIDIA或AMD制造的独立显卡，最好不要太旧，并安装最新的驱动程序。

可以在没有GPU的情况下运行该程序，但是性能会低得多。如果您的CPU不是很新（Haswell或更新的版本，Ryzen或更新的版本），那么性能将非常糟糕，尝试加入分布式工作可能毫无用处。但是您仍然可以玩，特别是如果您有耐心的话。

视窗
转到位于https://github.com/leela-zero/leela-zero/releases的Github发布页面，下载最新版本，解压缩并启动autogtp.exe。它将自动连接到服务器并在后台执行其工作，并在每次游戏后上载结果。您只需关闭autogtp窗口即可将其停止。

macOS和Linux
请按照以下说明在build子目录中编译leelaz和autogtp二进制文件。然后作为解释的运行autogtp 有助于下面的说明。当您运行autogtp时，将开始进行贡献。

使用云提供商
许多云公司提供免费试用版（或付费解决方案，此处未讨论），可用于帮助实现leela-zero项目。

这里有社区维护的说明：

在Tesla V100 GPU上免费运行Leela Zero客户端（Google云免费试用）

免费在Tesla V100 GPU上运行Leela Zero客户端（Microsoft Azure云免费试用）

我现在只想和Leela Zero一起玩
从此处下载最著名的网络权重文件，或者，如果您更喜欢人类风格，请从此处从人类游戏中训练（较弱）的网络。

如果您使用的是Windows，请从此处下载正式版本，然后转到 本自述文件的“ 用法”部分。

如果您使用的是macOS，则可以通过事实上的标准软件包管理器Homebrew获得Leela Zero 。您可以使用以下方法安装它：

brew install leela-zero
如果您使用的是Unix，则必须自己编译程序。请按照下面的编译说明进行操作，然后阅读“ 用法”部分。

编译AutoGTP和/或Leela Zero
要求
GCC，Clang或MSVC，任何C ++ 14编译器
Boost 1.58.x或更高版本，标头和program_options，文件系统和系统库（Debian / Ubuntu上的libboost-dev，libboost-program-options-dev和libboost-filesystem-dev）
zlib库（Debian / Ubuntu上的zlib1g和zlib1g-dev）
标准的OpenCL C标头（Debian / Ubuntu上的opencl-header或 https://github.com/KhronosGroup/OpenCL-Headers/tree/master/CL）
OpenCL ICD加载程序（Debian / Ubuntu上的ocl-icd-libopencl1或在https://github.com/KhronosGroup/OpenCL-ICD-Loader上的参考实现）
强烈建议使用支持OpenCL的设备，最好是非常快的GPU，并带有最新的驱动程序（对OpenCL 1.1的支持就足够了）。如果此部分由Linux发行版（例如nvidia-opencl-icd）单独打包，请不要忘记安装OpenCL驱动程序。如果没有GPU，请添加定义“ USE_CPU_ONLY”，例如，通过在cmake命令行中添加-DUSE_CPU_ONLY = 1。
可选：BLAS库：OpenBLAS（libopenblas-dev）或英特尔MKL
该程序已在Windows，Linux和macOS上进行了测试。
编译示例-Ubuntu＆类似
# Test for OpenCL support & compatibility
sudo apt install clinfo && clinfo

# Clone github repo
git clone https://github.com/leela-zero/leela-zero
cd leela-zero
git submodule update --init --recursive

# Install build depedencies
sudo apt install cmake g++ libboost-dev libboost-program-options-dev libboost-filesystem-dev opencl-headers ocl-icd-libopencl1 ocl-icd-opencl-dev zlib1g-dev

# Use a stand alone build directory to keep source dir clean
mkdir build && cd build

# Compile leelaz and autogtp in build subdirectory with cmake
cmake ..
cmake --build .

# Optional: test if your build works correctly
./tests
编译示例-macOS
# Clone github repo
git clone https://github.com/leela-zero/leela-zero
cd leela-zero
git submodule update --init --recursive

# Install build depedencies
brew install boost cmake zlib

# Use a stand alone build directory to keep source dir clean
mkdir build && cd build

# Compile leelaz and autogtp in build subdirectory with cmake
cmake ..
cmake --build .

# Optional: test if your build works correctly
./tests
编译示例-Windows
# Clone github repo
git clone https://github.com/leela-zero/leela-zero
cd leela-zero
git submodule update --init --recursive

cd msvc
Double-click the leela-zero2015.sln or leela-zero2017.sln corresponding
to the Visual Studio version you have.
# Build from Visual Studio 2015 or 2017
贡献
对于Windows，可以使用发行包，请参阅“我要帮助”。

Unix和macOS，在完成编译后并在build目录中：

# Copy leelaz binary to autogtp subdirectory
cp leelaz autogtp

# Run AutoGTP to start contributing
./autogtp/autogtp
玩游戏或分析游戏的用法
Leela Zero不能直接使用。您需要一个图形界面，它将通过GTP协议与Leela Zero进行交互。

该引擎支持GTP协议版本2。

Lizzie是专用于Leela Zero的客户，Leela Zero显示实时搜索能力，获胜率图表，并具有自动游戏分析模式。具有适用于Windows，Mac和Linux的二进制文件。

Sabaki是具有GTP 2功能的非常漂亮的GUI。

LeelaSabaki进行了修改，以显示游戏树中的变化和获胜统计数据，以及游戏板上的热图。

GoReviewPartner是用于使用漫游器（另存为.rsgf文件）自动审查和分析游戏的工具，支持Leela Zero。

很多go软件都可以通过GTP与引擎连接，因此请环顾四周。

在引擎命令行上添加--gtp命令行选项，以启用Leela Zero的GTP支持。您将需要一个权重文件，并使用-w选项进行指定。

支持所有必需的命令，以及比赛子集和“ loadsgf”。全套可以通过“ list_commands”看到。可以通过time_settings命令在GTP上指定时间控制。还支持kgs-time_settings扩展。这些必须由GTP 2接口提供，而不是通过命令行提供！

权重格式
权重文件是一个文本文件，每行包含一行系数。网络的布局与AlphaGo Zero论文相同，但允许任何数量的剩余块，并且每层可以有任意数量的输出（滤波器），只要后者对于所有层都是相同的即可。该程序将在启动时自动检测金额。第一行包含版本号。

卷积层有2个权重行：
卷积权重
渠道偏差
Batchnorm图层具有2个权重行：
批处理标准
批范数方差
内部产品（完全连接）层具有2行重量：
层权重
输出偏差
卷积权重按[输出，输入，filter_size，filter_size]顺序，完全连接的层权重按[输出，输入]顺序。首先是剩余塔，然后是政策负责人，然后是价值负责人。除策略和值头开头的卷积过滤器为1x1（如本文所述）外，所有卷积过滤器均为3x3。

第一层有18个输入，而不是本文中的17个。原始的AlphaGo Zero零点设计略有失衡，因为黑人玩家更容易看到棋盘边缘（由于填充在神经网络中的工作原理）。此问题已在Leela Zero中修复。输入是：

1) Side to move stones at time T=0
2) Side to move stones at time T=-1  (0 if T=0)
...
8) Side to move stones at time T=-7  (0 if T<=6)
9) Other side stones at time T=0
10) Other side stones at time T=-1   (0 if T=0)
...
16) Other side stones at time T=-7   (0 if T<=6)
17) All 1 if black is to move, 0 otherwise
18) All 1 if white is to move, 0 otherwise
这些每个都形成一个19 x 19位平面。

在training / caffe目录中，有一个zero.prototxt文件，其中包含（NVIDIA）-Caffe protobuff格式的全部40个残留块设计的描述。它可以用于设置nv-caffe以训练合适的网络。zero_mini.prototxt文件描述了较小的12个剩余块的情况。training / tf目录在tfprocess.py文件中包含TensorFlow格式的网络构造。

专家说明：通道偏差在网络拓扑中似乎是多余的，因为它们后面紧跟着一个batchnorm层，该层应规范化均值。实际上，它们对批处理规范层中的中心/比例操作的“ beta”参数进行了编码，并针对批处理规范均值/方差调整的效果进行了校正。在推断时，Leela Zero会将通道偏差融合到Batchnorm平均值中，从而抵消它并执行中心操作。存在这种回旋结构仅是为了向后兼容。如果该段对您没有任何意义，请忽略其存在，仅像通常那样添加通道偏置层，输出将是正确的。

训练
获取数据
在游戏结束时，您可以向Leela Zero发送“ dump_training”命令，然后发送游戏获胜者（“白色”或“黑色”）和文件名，例如：

dump_training white train.txt
这将以以下所述的格式将训练数据保存（追加）到磁盘，并使用gzip压缩。

训练数据在新游戏上重置。

监督学习
Leela可以将连接的SGF游戏的数据库转换为适合学习的数据文件：

dump_supervised sgffile.sgf train.txt
这将导致生成一系列gzip压缩文件，从名称train.txt开始，并包含从指定的SGF生成的训练数据，适用于深度学习框架。

训练数据格式
培训数据由具有以下数据的文件组成，所有文件均为文本格式：

16行十六进制字符串，每条长361位，对应于上一节中的前16个输入平面
1行带有1个数字，指示要移动的人，0 =黑色，1 =白色，可以从中重建最后2个输入平面
1行包含362（19x19 +1）个浮点数，表示搜索到的移动结束时的搜索概率（访问计数）。最后一个数字是通过的概率。
1行或1或-1，对应于游戏结果，玩家可以移动
进行培训
为了训练新网络，您可以使用现有框架（Caffe，TensorFlow，PyTorch，Theano），并使用如上所述的一组训练数据。您仍然需要构造模型描述（为Caffe提供了2个示例），解析输入文件格式，并以适当的格式输出权重。

在training / tf目录中有TensorFlow的完整实现。

使用TensorFlow进行监督学习
这需要TensorFlow 1.4或更高版本的有效安装：

src/leelaz -w weights.txt
dump_supervised bigsgf.sgf train.out
exit
training/tf/parse.py 6 128 train.out
这将运行并定期将Leela零权重文件（具有6个块和128个过滤器的网络的文件）以及以批号编号的学习状态快照转储到磁盘上。如果中断，可以使用以下方法恢复培训：

training/tf/parse.py 6 128 train.out leelaz-model-batchnumber
去做
 进一步优化Winograd转换。
 在搜索中改善GPU批处理。
 障碍物的根过滤。
更多后端：
 基于MKL-DNN的后端。
 使用cuDNN或cuBLAS的CUDA特定版本。
 使用MIOpen / ROCm的AMD特定版本。
相关链接
分布式工作量的状态页：https : //zero.sjeng.org
Leela Zero的GUI和学习工具：https : //github.com/featurecat/lizzie
在GUI中观看Leela Zero的培训游戏：https : //github.com/fsparv/LeelaWatcher
原始Alpha Go（李·塞多尔）论文：https：//storage.googleapis.com/deepmind-media/alphago/AlphaGoNaturePaper.pdf
Alpha Go Zero论文：https : //deepmind.com/documents/119/agz_unformatted_nature.pdf
Alpha Zero（Go，Chess，Shogi）论文：https : //arxiv.org/pdf/1712.01815.pdf
AlphaGo零解释在一张图中：https : //medium.com/applied-data-science/alphago-zero-explained-in-one-diagram-365f5abf67e0
Stockfish国际象棋引擎移植到Leela Zero框架：https : //github.com/LeelaChessZero/lczero
Leela Chess Zero（国际象棋优化客户端） https://github.com/LeelaChessZero/lc0
执照
该代码在GPLv3或更高版本下发布，但ThreadPool.h，cl2.hpp，half.hpp以及eigen和clblast_level3子目录除外，它们具有在这些文件中提到的特定许可证（与GPLv3兼容）。

根据GNU GPL版本3第7节的附加许可

如果您通过与NVIDIA CUDA工具包和/或NVIDIA CUDA深度神经网络库和/或NVIDIA TensorRT推理库（或这些程序的修改版）中的NVIDIA Corporation的库链接或组合来修改本程序或任何涵盖的工作，库），其中包含各自许可协议的条款所涵盖的部分，则本程序的许可人授予您额外的许可，以传达所产生的作品。
