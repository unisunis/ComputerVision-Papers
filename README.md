# GAN-papers

## Baseline
- [Generative Adversarial Nets](http://papers.nips.cc/paper/5423-generative-adversarial-nets.pdf)
  - 始まり。GeneratorとDiscriminatorという２つのネットワークを学習させて、Generatorから対象物を生成するアイデア
- [Unsupervised Representation Learning With Deep Convolutional Generative Adversarial Networks](https://arxiv.org/pdf/1511.06434.pdf%C3%AF%C2%BC%E2%80%B0)
  - DCGAN。Batch Normalizationを用いる、GeneratorにはLeaky-ReLUを用いる等GANを学習させるテクニックを駆使している。
  - ただし、高解像度にはmode collapse(同一画像を生成するようになる)が起きたり、学習の収束が安定しなかったり等問題は山積み。

## GAN Techniques
- [Conditional Image Synthesis with Auxiliary Classifier GANs](https://arxiv.org/pdf/1610.09585.pdf)
  - Discriminatorにどのスタイルなのかを判別する項を追加したACGANを提案。
  - 狙ったドメインの画像生成が可能。
- [Towards Principled Methods For Training Generative Adversarial Networks](https://arxiv.org/pdf/1701.04862.pdf)
  - 上記のDCGANは収束性の問題があるとして、GeneratorとDiscriminatorの間の確率分布の距離をJS-divergenceではなくEarth-Mover Distanceを用いることを提案。
  - このEarth-Mover Distanceを最小化することで学習が安定する。次に示すWassersteinGANへの布石となる。
- [Wasserstein GAN](https://arxiv.org/pdf/1701.07875.pdf)
  - 前の論文からの続きとして、Earth-Mover Distanceを最小化するWGANを提案。
  - Earth-Mover Distanceを最小化するために、Discriminatorは1-Lipchitzを満たす必要がある。そのために、Discriminatorの勾配をweight clippingで制限。
- [Improved Training of Wasserstein GANs](https://arxiv.org/pdf/1704.00028.pdf)
  - 上記のWGANでは重みの値が二極化してしまうといった問題点があった。そこで、weight clippingではなくgradient penaltyを採用したWGAN-GPを提案。
  - 損失関数にDiscriminatorの勾配を制限する項を追加。
- [On Convergence and Stability of GANs](https://arxiv.org/pdf/1705.07215.pdf)
  - 訓練データの周りの領域においてのみ、勾配に制約をかけるDRAGANを提案。
- [Spectral Normalization for Generative Adversarial Networks](https://arxiv.org/pdf/1802.05957.pdf)
  - GeneratorとDiscriminatorの各層にSpectral Normalizationを加えることで1-Lipchitzの制約を満たす。
  - 実質的にハイパーパラメータのチューニングをする必要がなくなった。
- [Unrolled Generative Adversarial Networks](https://arxiv.org/pdf/1611.02163.pdf)
  - Discriminatorの学習がどうしても早くなってしまうため、学習を進めればDiscriminatorが完全にGeneratorが贋作かどうかを判別出来る。
  - Discriminatorの学習を何段階か行わせ、それに対してGeneratorの学習を行う。
- [Self-Attention Generative Adversarial Networks](https://arxiv.org/pdf/1805.08318.pdf)
  - 画像内の離れた区間も見られるよう、self-attention機構をGeneratorとDiscriminatoに追加。
- [The Relativistic Discriminator : A Key Element Missing from Standard GAN](https://arxiv.org/pdf/1807.00734.pdf)
  - 真のデータと偽のデータのスコア差、もしくはどちらかの平均との差を取って学習するRelativistic Discriminatorを提案する。
- [Which Trainings Methods for GANs Do Acutually Converge ?](https://arxiv.org/pdf/1801.04406.pdf)
  - Instance noiseもしくはZero-centered gradient penaltiesを与えることで学習が安定することを提案
  - 実際の学習ではgradient penalty with critical regularizerを導入することで、一般的な最適化問題へと落とし込めている。
  - 論文では記されてないが、1024 * 1024サイズの画像を生成することも可能。
  
## High-Resolution Image Generation
- [StackGAN : Text to Photo-realistic Image Synthesis with Stacked Generative Adversarial Networks](https://arxiv.org/pdf/1612.03242.pdf)
  - 二段階のDiscriminatorとGeneratorを学習させて、高解像度256 * 256の画像を生成
  - 論文中では、文章から画像を生成している。
- [StackGAN++ : Realistic Image Synthesis with Stacked Generative Adversarial Networks](https://arxiv.org/pdf/1710.10916.pdf)
  - StackGANをバージョンアップさせ、多段階的な学習を行うことで高解像度の画像を生成。
- [Progressive Growing of GANs of Improved Quality, Stability and Variation](https://arxiv.org/pdf/1710.10196.pdf)
  - 4 * 4の画像から多段階的に層を追加することによって1024 * 1024といった高解像度の画像を生成。
  - Variationにはminibatch standard deviation、stabilityにはgradient penaltyを与えることで対処している。
  
## Style Transfer
- [Unpaired Image-to-Image Translation using Cycle-Consitent Generative Adversarial Networks](https://arxiv.org/pdf/1703.10593.pdf)
  - Pix2pix等によるスタイル変換はパラレルデータが必要だった、ノンパラレルデータでも学習できるようCycleGANを提案。
  - ２つのGeneratorとDiscriminatorのペアを用意して、互いに変換しあう。
- [StarGAN : Unified Generative Adversarial Networks for Multi-Domain Image-to-Image Translation](https://arxiv.org/pdf/1711.09020.pdf)
  - CycleGANは一対一のドメイン間しか変換できなかった、マルチドメイン間で変換できるStarGANを提案。
  - DiscriminatorはReal/Fakeの判別だけでなく、どのドメインかも判別出来るようになる。
  
## Application
- [Towards the Automatic Anime Characters Creation with Generative Adversarial Networks](https://arxiv.org/pdf/1708.05509.pdf)
  - クオリティの高いアニメキャラ生成。makegirlsmoeの論文。
  - データセットの作成、Illustration2Vecを用いる、SRResNetを用いるなど随所に工夫が見られる。
- [CartoonGAN : Generative Adversarial Networks for Photo Cartoonization](http://openaccess.thecvf.com/content_cvpr_2018/papers/Chen_CartoonGAN_Generative_Adversarial_CVPR_2018_paper.pdf)
  - 風景写真からアニメ風背景への変換。CycleGANベースでedge-smoothedとsemantic content lossを考慮。
- [CAN : Creative Adversarial Networks Generating "Art" by Learning About Styles and Deviating from Style Norms](https://arxiv.org/pdf/1706.07068.pdf)
  - 美術画の生成
- [MaskGAN : Better Text Generation Via Filling in the ____](https://arxiv.org/pdf/1801.07736.pdf)
  - 自然言語処理への応用。____に入る言葉を学習する。
- [High-Quality Nonparallel Voice Conversion Based-on Cycle-Consistent Adversarial Network](https://arxiv.org/pdf/1804.00425.pdf)
  - 声質変換への応用。CycleGANを用いることで、ノンパラレルコーパスに対して声質変換を行う。
  - 論文中では、メルケプストラムの低次元側に対してCycleGANを適用している。
