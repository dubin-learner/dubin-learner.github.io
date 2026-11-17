# Image Process Resources
> 这些代码很实用，可以让我们站在巨人的肩膀上。源博客[地址](http://blog.sina.com.cn/s/blog_631a4cc40100wrvz.html)

## Feature Extraction

### Resources
- SIFT [1] [[Demo program]](http://www.cs.ubc.ca/~lowe/keypoints/siftDemoV4.zip) [[SIFT Library]](http://blogs.oregonstate.edu/hess/code/sift/) [[VLFeat]](http://www.vlfeat.org/)
- PCA-SIFT [2] [[Project]](http://www.cs.cmu.edu/~yke/pcasift/)
- Affine-SIFT [3] [[Project]](http://www.ipol.im/pub/algo/my_affine_sift/)
- SURF [4] [[OpenSURF]](http://www.chrisevansdev.com/computer-vision-opensurf.html) [[Matlab Wrapper]](http://www.maths.lth.se/matematiklth/personal/petter/surfmex.php)
- Affine Covariant Features [5] [[Oxford project]](http://www.robots.ox.ac.uk/~vgg/research/affine/)
- MSER [6] [[Oxford project]](http://www.robots.ox.ac.uk/~vgg/research/affine/) [[VLFeat]](http://www.vlfeat.org/)
- Geometric Blur [7] [[Code]](http://www.robots.ox.ac.uk/~vgg/software/MKL/)
- Local Self-Similarity Descriptor [8] [[Oxford implementation]](http://www.robots.ox.ac.uk/~vgg/software/SelfSimilarity/)
- Global and Efficient Self-Similarity [9] [[Code]](http://www.vision.ee.ethz.ch/~calvin/gss/selfsim_release1.0.tgz)
- Histogram of Oriented Graidents [10] [[INRIA Object Localization Toolkit]](http://www.navneetdalal.com/software) [[OLT toolkit for Windows]](http://www.computing.edu.au/~12482661/hog.html)
- GIST [11] [[Project]](http://people.csail.mit.edu/torralba/code/spatialenvelope/)
- Shape Context [12] [[Project]](http://www.eecs.berkeley.edu/Research/Projects/CS/vision/shape/sc_digits.html)
- Color Descriptor [13] [[Project]](http://koen.me/research/colordescriptors/)
- Pyramids of Histograms of Oriented Gradients [[Code]](http://www.robots.ox.ac.uk/~vgg/research/caltech/phog/phog.zip)
- Space-Time Interest Points (STIP) [14] [[Code]](http://www.irisa.fr/vista/Equipe/People/Laptev/download/stip-1.1-winlinux.zip)
- Boundary Preserving Dense Local Regions [15] [[Project]](http://vision.cs.utexas.edu/projects/bplr/bplr.html)

### References

1. D. Lowe. **Distinctive Image Features from Scale-Invariant Keypoints**, IJCV 2004. [[PDF]](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.157.3843&rep=rep1&type=pdf)
2. Y. Ke and R. Sukthankar, **PCA-SIFT: A More Distinctive Representation for Local Image Descriptors**,CVPR, 2004. [[PDF]](http://www.cs.cmu.edu/~rahuls/pub/cvpr2004-keypoint-rahuls.pdf)
3. J.M. Morel and G.Yu, ASIFT, **A new framework for fully affine invariant image comparison**. *SIAM Journal on Imaging Sciences*, 2009. [[PDF]](http://www.google.com/url?sa=t&source=web&cd=3&ved=0CDEQFjAC&url=http://www.cmap.polytechnique.fr/~yu/publications/SIAM_ASIFT.pdf&ei=uccMTs-tK6eEsgKX1Yz4CQ&usg=AFQjCNFRn8wFQa_pB054ZZEErrCXSXfzQA&sig2=c6tAIqvtz2HY7WwPKkUizQ)
4. H. Bay, T. Tuytelaars and L. V. Gool, **SURF: Speeded Up Robust Features**,ECCV, 2006. [[PDF]](ftp://ftp.vision.ee.ethz.ch/publications/articles/eth_biwi_00517.pdf)
5. K. Mikolajczyk, T. Tuytelaars, C. Schmid, A. Zisserman, J. Matas, F. Schaffalitzky, T. Kadir and L. Van Gool, **A comparison of affine region detectors**. IJCV, 2005. [[PDF]](http://www.robots.ox.ac.uk/~vgg/research/affine/det__files/vibes_ijcv2004.pdf)
6. J. Matas, O. Chum, M. Urba, and T. Pajdla. **Robust wide baseline stereo from maximally stable extremal regions**. BMVC, 2002. [[PDF]](http://www.google.com/url?sa=t&source=web&cd=2&ved=0CCYQFjAB&url=http://cmp.felk.cvut.cz/~matas/papers/presentations/mser_taormina_Sep03.pdf&ei=E8gMTs6kLY2osAKyjK32CQ&usg=AFQjCNF6D04gbS5o-1bYHiwc870utUEAMg&sig2=EM1iHEOVuCPiEUyFhJDLkA)
7. A. C. Berg, T. L. Berg, and J. Malik. **Shape matching and object recognition using low distortion correspondences**. CVPR, 2005. [[PDF]](http://www.google.com/url?sa=t&source=web&cd=1&ved=0CBsQFjAA&url=http://acberg.com/papers/berg_correspondence_cvpr.pdf&ei=b8gMTtLbIM6rsAKGrbWBCg&usg=AFQjCNHfh36YWDf_HowuMsENc_y0nPE1hw&sig2=noT-y0tTErVhQnQXflawOg)
8. E. Shechtman and M. Irani. **Matching local self-similarities across images and videos**, CVPR, 2007. [[PDF]](http://www.google.com/url?sa=t&source=web&cd=1&ved=0CBoQFjAA&url=http://research.microsoft.com/en-us/um/people/manik/projects/trade-off/papers/ShechtmanCVPR07.pdf&ei=gMgMTp_pH4XFsQLzu-i3Cg&usg=AFQjCNHYDO0SSj1nYm_mj8nyOfDADoZpEA&sig2=7NDGqiR8VYrsJrJpqJwHyA)
9. T. Deselaers and V. Ferrari. **Global and Efficient Self-Similarity for Object Classification and Detection**. CVPR 2010. [[PDF]](http://www.google.com/url?sa=t&source=web&cd=1&ved=0CB4QFjAA&url=http://thomas.deselaers.de/publications/papers/deselaers-cvpr10.pdf&ei=jcgMTqvSEI2EsgL1kN2ICg&usg=AFQjCNHZyBW59YZNumVR0pRye1grkS9qsQ&sig2=FNHuC6TKnrCvVfErttJZkA)
10. N. Dalal and B. Triggs. **Histograms of Oriented Gradients for Human Detection**. CVPR 2005. [[PDF]](http://lear.inrialpes.fr/people/triggs/pubs/Dalal-cvpr05.pdf)
11. A. Oliva and A. Torralba. **Modeling the shape of the scene: a holistic representation of the spatial envelope**, IJCV, 2001. [[PDF]](http://www.google.com/url?sa=t&source=web&cd=1&ved=0CBsQFjAA&url=http://www.cs.cmu.edu/~efros/courses/LBMV07/Papers/oliva-ijcv-01.pdf&ei=msgMTvG8B-SBsgKQ16WdCg&usg=AFQjCNFqZVy5bWhB_Xzoni_C6CvpC3jWeQ&sig2=LTyLplUsyfFD2f1vj8bXCQ)
12. S. Belongie, J. Malik and J. Puzicha. **Shape matching and object recognition using shape contexts**, PAMI, 2002. [[PDF]](http://www.google.com/url?sa=t&source=web&cd=1&ved=0CBoQFjAA&url=http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.18.8852&rep=rep1&type=pdf&ei=pcgMTpamFvKmsALQ7oymCg&usg=AFQjCNH8Ecse7glHaVx-ImAqoVk41Ay9-Q&sig2=IqoNpz97EKYXpUe9vIEK4Q)
13. K. E. A. van de Sande, T. **Gevers and Cees G. M. Snoek, Evaluating Color Descriptors for Object and Scene Recognition**, PAMI, 2010.
14. I. Laptev, **On Space-Time Interest Points**, IJCV, 2005. [[PDF]](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.158.9437&rep=rep1&type=pdf)
15. J. Kim and K. Grauman, **Boundary Preserving Dense Local Regions**, CVPR 2011. [[PDF]](http://www.cs.utexas.edu/~grauman/papers/bplr_CVPR2011.pdf)

## Image Segmentation

### Resources
- Normalized Cut [1] [[Matlab code]](http://www.cis.upenn.edu/~jshi/software/)
- Gerg Mori' Superpixel code [2] [[Matlab code]](http://www.cs.sfu.ca/~mori/research/superpixels/)
- Efficient Graph-based Image Segmentation [3] [[C++ code]](http://people.cs.uchicago.edu/~pff/segment/) [[Matlab wrapper]](http://www.mathworks.com/matlabcentral/fileexchange/25866-efficient-graph-based-image-segmentation)
- Mean-Shift Image Segmentation [4] [[EDISON C++ code]](http://coewww.rutgers.edu/riul/research/code/EDISON/index.html) [[Matlab wrapper]](http://www.wisdom.weizmann.ac.il/~bagon/matlab_code/edison_matlab_interface.tar.gz)
- OWT-UCM Hierarchical Segmentation [5] [[Resources]](http://www.eecs.berkeley.edu/Research/Projects/CS/vision/grouping/resources.html)
- Turbepixels [6] [[Matlab code 32bit]](http://www.cs.toronto.edu/~babalex/turbopixels_code.tar.gz) [[Matlab code 64bit]](http://www.cs.toronto.edu/~babalex/TurboPixels64.rar) [[Updated code]](http://www.cs.toronto.edu/~babalex/superpixels_update.tgz)
- Quick-Shift [7] [[VLFeat]](http://www.vlfeat.org/overview/quickshift.html)
- SLIC Superpixels [8] [[Project]](http://ivrgwww.epfl.ch/supplementary_material/RK_SLICSuperpixels/index.html)
- Segmentation by Minimum Code Length [9] [[Project]](http://perception.csl.uiuc.edu/coding/image_segmentation/)
- Biased Normalized Cut [10] [[Project]](http://www.cs.berkeley.edu/~smaji/projects/biasedNcuts/)
- Segmentation Tree [11-12] [[Project]](http://vision.ai.uiuc.edu/segmentation)
- Entropy Rate Superpixel Segmentation [13] [[Code]](http://www.umiacs.umd.edu/~mingyliu/src/ers_matlab_wrapper_v0.1.zip)

### References

1. J. Shi and J Malik, **Normalized Cuts and Image Segmentation**, PAMI, 2000 [[PDF]](http://www.cis.upenn.edu/~jshi/papers/pami_ncut.pdf)
2. X. Ren and J. Malik. **Learning a classification model for segmentation**. ICCV, 2003. [[PDF]](http://ttic.uchicago.edu/~xren/publication/xren_iccv03_discrim.pdf)
3. P. Felzenszwalb and D. Huttenlocher. **Efficient Graph-Based Image Segmentation**, IJCV 2004. [[PDF]](http://www.google.com/url?sa=t&source=web&cd=1&ved=0CB8QFjAA&url=http://people.cs.uchicago.edu/~pff/papers/seg-ijcv.pdf&ei=T80MTuniMMSpsQLhtISOCg&usg=AFQjCNFOD1DT07FVoFPb0Whk9w1250yRoA&sig2=EcXtgtLMfl4X_l1uMOT_Tg)
4. D. Comaniciu, P Meer. **Mean Shift: A Robust Approach Toward Feature Space Analysis**. PAMI 2002. [[PDF]](http://www.google.com/url?sa=t&source=web&cd=1&ved=0CB0QFjAA&url=http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.94.4140&rep=rep1&type=pdf&ei=WM0MTqvBFYLFsQLV6L2kCg&usg=AFQjCNF-K1LtZvsFOEgQC1hPuky8kkmPSA&sig2=mcpVbGba1V-ueq9IIOs2Rg)
5. P. Arbelaez, M. Maire, C. Fowlkes and J. Malik. **Contour Detection and Hierarchical Image Segmentation**. PAMI, 2011. [[PDF]](http://www.google.com/url?sa=t&source=web&cd=3&ved=0CC0QFjAC&url=http://www.eecs.berkeley.edu/Pubs/TechRpts/2009/EECS-2009-129.pdf&ei=Yc0MTpLBO6eGsgK3qKmvCg&usg=AFQjCNEcqayUHreIzx1q7cNQbBoOk4d4hg&sig2=B2vVJA06l3tnqGfL6zgZOA)
6. A. Levinshtein, A. Stere, K. N. Kutulakos, D. J. Fleet, S. J. Dickinson, and K. Siddiqi, **TurboPixels: Fast Superpixels Using Geometric Flows**, PAMI 2009. [[PDF]](http://www.google.com/url?sa=t&source=web&cd=1&ved=0CBsQFjAA&url=http://www.cs.toronto.edu/~sven/Papers/turbopixels.pdf&ei=iM0MTpyiOemksQKWyJWKCg&usg=AFQjCNHy5VAuaeQZHBzNBt_L_cfnRDMWBw&sig2=eWRgRcvrmSKHEKUDLNT9pg)
7. A. Vedaldi and S. Soatto, **Quick Shift and Kernel Methodsfor Mode Seeking**, ECCV, 2008. [[PDF]](http://vision.ucla.edu/papers/vedaldiS08quick.pdf)
8. R. Achanta, A. Shaji, K. Smith, A. Lucchi, P. Fua, and S. Susstrunk, **SLIC Superpixels**, *EPFL Technical Report*, 2010. [[PDF]](http://www.google.com/url?sa=t&source=web&cd=2&ved=0CCEQFjAB&url=http://cvlab.epfl.ch/publications/publications/2010/AchantaSSLFS10a.pdf&ei=lM0MTtqaKonksQKw1qSyCg&usg=AFQjCNFoRCrs90RY9LxYQRP6PlkyJ_IWYg&sig2=e7lZf3vnwPvZiZ89daxBOA)
9. A. Y. Yang, J. Wright, S. Shankar Sastry, Y. Ma, **Unsupervised Segmentation of Natural Images via Lossy Data Compression**, CVIU, 2007. [[PDF]](http://www.google.com/url?sa=t&source=web&cd=3&ved=0CC8QFjAC&url=http://robotics.eecs.berkeley.edu/~sastry/pubs/Pdfs%20of%202008/YangUnsupervised2008.pdf&ei=n80MTp-2DfSrsAK406CxCg&usg=AFQjCNGTwJUsi0CvkGt2dKpWnpS0A9zw-w&sig2=Aap8c9UvmdhoTgjjRfs4gQ)
10. S. Maji, N. Vishnoi and J. Malik, **Biased Normalized Cut**, CVPR 2011
11. E. Akbas and N. Ahuja, **From ramp discontinuities to segmentation tree**, ACCV 2009. [[PDF]](http://www.computer.org/portal/web/csdl/doi/10.1109/34.546258)
12. N. Ahuja, **A Transform for Multiscale Image Segmentation by Integrated Edge and Region Detection**, PAMI 1996. [[PDF]](http://www.computer.org/portal/web/csdl/doi/10.1109/34.546258)
13. M.-Y. Liu, O. Tuzel, S. Ramalingam, and R. Chellappa, **Entropy Rate Superpixel Segmentation**, CVPR 2011. [[PDF]](http://www.umiacs.umd.edu/~mingyliu/papers/liu_cvpr2011.pdf)

## Object Detection

### Resources

- A simple object detector with boosting [[Project]](http://people.csail.mit.edu/torralba/shortCourseRLOC/boosting/boosting.html)
- INRIA Object Detection and Localization Toolkit [1] [[Project]](http://pascal.inrialpes.fr/soft/olt/)
- Discriminatively Trained Deformable Part Models [2] [[Project]](http://people.cs.uchicago.edu/~pff/latent/)
- Cascade Object Detection with Deformable Part Models [3] [[Project]](http://people.cs.uchicago.edu/~rbg/star-cascade/)
- Poselet [4] [[Project]](http://www.eecs.berkeley.edu/~lbourdev/poselets/)
- Implicit Shape Model [5] [[Project]](http://www.vision.ee.ethz.ch/~bleibe/code/ism.html)
- Viola and Jones's Face Detection [6] [[Project]](http://pr.willowgarage.com/wiki/Face_detection)

### References

1. N. Dalal and B. Triggs. **Histograms of Oriented Gradients for Human Detection**. CVPR 2005. [[PDF]](http://lear.inrialpes.fr/people/triggs/pubs/Dalal-cvpr05.pdf)
2. P. Felzenszwalb, R. Girshick, D. McAllester, D. Ramanan. **Object Detection with Discriminatively Trained Part Based Models**, PAMI, 2010 [[PDF]](http://people.cs.uchicago.edu/~pff/papers/lsvm-pami.pdf)
3. P. Felzenszwalb, R. Girshick, D. McAllester. **Cascade Object Detection with Deformable Part Models**. CVPR 2010 [[PDF]](http://people.cs.uchicago.edu/~pff/papers/cascade.pdf)
4. L. Bourdev, J. Malik, **Poselets: Body Part Detectors Trained Using 3D Human Pose Annotations**, ICCV 2009 [[PDF]](http://www.eecs.berkeley.edu/Research/Projects/CS/vision/human/poselets_iccv09.pdf)
5. B. Leibe, A. Leonardis, B. Schiele. **Robust Object Detection with Interleaved Categorization and Segmentation**, IJCV, 2008. [[PDF]](http://www.vision.ee.ethz.ch/~bleibe/papers/leibe-interleaved-ijcv07final.pdf)
6. P. Viola and M. Jones, **Rapid Object Detection Using a Boosted Cascade of Simple Features**, CVPR 2001. [[PDF]](http://research.microsoft.com/en-us/um/people/viola/Pubs/Detect/violaJones_CVPR2001.pdf)

## Saliency Detection

### Resources

- Itti, Koch, and Niebur' saliency detection [1] [[Matlab code]](http://www.saliencytoolbox.net/)
- Frequency-tuned salient region detection [2] [[Project]](http://ivrgwww.epfl.ch/supplementary_material/RK_CVPR09/index.html)
- Saliency detection using maximum symmetric surround [3] [[Project]](http://ivrg.epfl.ch/supplementary_material/RK_ICIP2010/index.html)
- Attention via Information Maximization [4] [[Matlab code]](http://www.cse.yorku.ca/~neil/AIM.zip)
- Context-aware saliency detection [5] [[Matlab code]](http://webee.technion.ac.il/labs/cgm/Computer-Graphics-Multimedia/Software/Saliency/Saliency.html)
- Graph-based visual saliency [6] [[Matlab code]](http://www.klab.caltech.edu/~harel/share/gbvs.php)
- Saliency detection: A spectral residual approach. [7] [[Matlab code]](http://www.klab.caltech.edu/~xhou/projects/spectralResidual/spectralresidual.html)
- Segmenting salient objects from images and videos. [8] [[Matlab code]](http://www.cse.oulu.fi/MVG/Downloads/saliency)
- Saliency Using Natural statistics. [9] [[Matlab code]](http://cseweb.ucsd.edu/~l6zhang/)
- Discriminant Saliency for Visual Recognition from Cluttered Scenes. [10] [[Code]](http://www.svcl.ucsd.edu/projects/saliency/)
- Learning to Predict Where Humans Look [11] [[Project]](http://people.csail.mit.edu/tjudd/WherePeopleLook/index.html)
- Global Contrast based Salient Region Detection [12] [[Project]](http://cg.cs.tsinghua.edu.cn/people/~cmm/saliency/)

### References

1. L. Itti, C. Koch, and E. Niebur. **A model of saliency-based visual attention for rapid scene analysis**. PAMI, 1998. [[PDF]](http://www.lira.dist.unige.it/teaching/SINA_08-09/papers/itti98model.pdf)
2. R. Achanta, S. Hemami, F. Estrada, and S. Susstrunk. **Frequency-tuned salient region detection**. In CVPR, 2009. [[PDF]](http://www.cs.utoronto.ca/~strider/publications/SaliencyCVPR09.pdf)
3. R. Achanta and S. Susstrunk. **Saliency detection using maximum symmetric surround**. In ICIP, 2010. [[PDF]](http://gitl.sysu.edu.cn/papers/icip2010/pdfs/0002653.pdf)
4. N. Bruce and J. Tsotsos. **Saliency based on information maximization**. InNIPS, 2005. [[PDF]](http://books.nips.cc/papers/files/nips18/NIPS2005_0081.pdf)
5. S. Goferman, L. Zelnik-Manor, and A. Tal. **Context-aware saliency detection**. In CVPR, 2010. [[PDF]](http://webee.technion.ac.il/~lihi/Publications/10-Saliency.pdf)
6. J. Harel, C. Koch, and P. Perona. **Graph-based visual saliency**. NIPS, 2007. [[PDF]](http://www.klab.caltech.edu/~harel/pubs/gbvs_nips.pdf)
7. X. Hou and L. Zhang. **Saliency detection: A spectral residual approach**. CVPR, 2007. [[PDF]](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.125.5641&rep=rep1&type=pdf)
8. E. Rahtu, J. Kannala, M. Salo, and J. Heikkila. **Segmenting salient objects from images and videos**. CVPR, 2010. [[PDF]](http://www.rni.helsinki.fi/~msa/pub/ECCV2010_Cameraready.pdf)
9. L. Zhang, M. Tong, T. Marks, H. Shan, and G. Cottrell. **Sun: A bayesian framework for saliency using natural statistics**. Journal of Vision, 2008. [[PDF]](http://cseweb.ucsd.edu/~gary/pubs/Zhang-et-al-2008-accepted.pdf)
10. D. Gao and N. Vasconcelos, **Discriminant Saliency for Visual Recognition from Cluttered Scenes**, NIPS, 2004. [[PDF]](http://www.svcl.ucsd.edu/publications/conference/2004/nips04/nips04.pdf)
11. T. Judd and K. Ehinger and F. Durand and A. Torralba, **Learning to Predict Where Humans Look**, ICCV, 2009. [[PDF]](http://people.csail.mit.edu/torralba/publications/wherepeoplelook.pdf)
12. M.-M. Cheng, G.-X. Zhang, N. J. Mitra, X. Huang, S.-M. Hu. **Global Contrast based Salient Region Detection**. CVPR 2011.

## Image Classification

### Resources

- Pyramid Match [1] [[Project]](http://people.csail.mit.edu/jjl/libpmk/)
- Spatial Pyramid Matching [2] [[Code]](http://www.cs.unc.edu/~lazebnik/research/SpatialPyramid.zip)
- Locality-constrained Linear Coding [3] [[Project]](http://www.ifp.illinois.edu/~jyang29/LLC.htm) [[Matlab code]](http://www.ifp.illinois.edu/~jyang29/codes/CVPR10-LLC.rar)
- Sparse Coding [4] [[Project]](http://www.ifp.illinois.edu/~jyang29/ScSPM.htm) [[Matlab code]](http://www.ifp.illinois.edu/~jyang29/codes/CVPR09-ScSPM.rar)
- Texture Classification [5] [[Project]](http://www.robots.ox.ac.uk/~vgg/research/texclass/index.html)
- Multiple Kernels for Image Classification [6] [[Project]](http://www.robots.ox.ac.uk/~vgg/software/MKL/)
- Feature Combination [7] [[Project]](http://www.vision.ee.ethz.ch/~pgehler/projects/iccv09/index.html)
- SuperParsing [[Code]](http://www.cs.unc.edu/~jtighe/Papers/ECCV10/eccv10-jtighe-code.zip)

### References

1. K. Grauman and T. Darrell, **The Pyramid Match Kernel: Discriminative Classification with Sets of Image Features**, ICCV 2005. [[PDF]](http://people.csail.mit.edu/kgrauman/grauman_darrell_iccv05.pdf)
2. S. Lazebnik, C. Schmid, and J. Ponce. **Beyond Bags of Features: Spatial Pyramid Matching for Recognizing Natural Scene Categories**, CVPR 2006 [[PDF]](http://www.cs.unc.edu/~lazebnik/publications/cvpr06b.pdf)
3. J. Wang, J. Yang, K. Yu, F. Lv, T. Huang, and Y. Gong. **Locality-constrained Linear Coding for Image Classification**, CVPR, 2010 [[PDF]](http://www.ifp.illinois.edu/~jyang29/papers/CVPR09-ScSPM.pdf)
4. J. Yang, K. Yu, Y. Gong, T. Huang, **Linear Spatial Pyramid Matching using Sparse Coding for Image Classification**, CVPR, 2009 [[PDF]](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.167.4480&rep=rep1&type=pdf)
5. M. Varma and A. Zisserman, **A statistical approach to texture classification from single images**, IJCV2005. [[PDF]](http://www.google.com/url?sa=t&source=web&cd=1&ved=0CB4QFjAA&url=http://research.microsoft.com/en-us/um/people/manik/pubs/varma05.pdf&ei=PtgMTt-CIO6rsAKBwKGCCg&usg=AFQjCNE07GnNKVdRm-ng71GuRK2iqJkK8A&sig2=H_XY_xwWN_osZCjRhpe6vA)
6. A. Vedaldi, V. Gulshan, M. Varma, and A. Zisserman, **Multiple Kernels for Object Detection**. ICCV, 2009. [[PDF]](http://www.google.com/url?sa=t&source=web&cd=1&ved=0CB4QFjAA&url=http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.163.5316&rep=rep1&type=pdf&ei=UNgMToLLL_SjsQL65PitCg&usg=AFQjCNFEO0j8MUMdnxSOWene05fd2xbwmQ&sig2=1nVnviqOQk-pvOeF_t5FRA)
7. P. Gehler and S. Nowozin, **On Feature Combination for Multiclass Object Detection**, ICCV, 2009. [[PDF]](http://www.google.com/url?sa=t&source=web&cd=2&ved=0CCgQFjAB&url=http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.165.9309&rep=rep1&type=pdf&ei=btgMTsWSKqj-sQKS86GRCg&usg=AFQjCNFareFupa_y45ddPEoE_jFDHPwqUA&sig2=wz8IqUPRaVJOQjJ8wK_PXw)
8. J. Tighe and S. Lazebnik, **SuperParsing: Scalable Nonparametric Image Parsing with Superpixels**, ECCV 2010. [[PDF]](http://www.cs.unc.edu/~lazebnik/publications/eccv10-jtighe.pdf)

## Category-Independent Object Proposal

### Resources

- Objectness measure [1] [[Code]](http://www.vision.ee.ethz.ch/~calvin/objectness/objectness-release-v1.01.tar.gz)
- Parametric min-cut [2] [[Project]](http://sminchisescu.ins.uni-bonn.de/code/cpmc/)
- Object proposal [3] [[Project]](http://vision.cs.uiuc.edu/proposals/)

### References

1. B. Alexe, T. Deselaers, V. Ferrari, **What is an Object?**, CVPR 2010 [[PDF]](http://www.google.com/url?sa=t&source=web&cd=5&ved=0CDoQFjAE&url=http://thomas.deselaers.de/publications/papers/alexe-cvpr10.pdf&ei=PNMMToSrOPGFsAKGnfDxCQ&usg=AFQjCNEly3j5jc8GGc3dufcmL6d82Ra3oQ&sig2=wuCtCCIuhGlg_gx8Fj3U_Q)
2. J. Carreira and C. Sminchisescu. **Constrained Parametric Min-Cuts for Automatic Object Segmentation**, CVPR 2010. [[PDF]](http://sminchisescu.ins.uni-bonn.de/papers/cs-cvpr10.pdf)
3. I. Endres and D. Hoiem. **Category Independent Object Proposals**, ECCV 2010. [[PDF]](http://cs.uiuc.edu/homes/iendres2/publications/eccv2010_prop.pdf)

## MRF

### Resources

- Graph Cut [[Project]](http://vision.csd.uwo.ca/code/) [[C++/Matlab Wrapper Code]](http://vision.csd.uwo.ca/code/gco-v3.0.zip)

### References

1. Y. Boykov, O. Veksler and R. Zabih, **Fast Approximate Energy Minimization via Graph Cuts**, PAMI 2001 [[PDF]](http://www.cs.cornell.edu/~rdz/Papers/BVZ-pami01-final.pdf)

## Shadow Detection

### Resources

- Shadow Detection using Paired Region [[Project]](http://www.cs.illinois.edu/homes/guo29/projects/shadow.html)
- Ground shadow detection [[Project]](http://www.jflalonde.org/software.html#shadowDetection)

### References

1. R. Guo, Q. Dai and D. Hoiem, **Single-Image Shadow Detection and Removal using Paired Regions**, CVPR 2011 [[PDF]](http://www.cs.illinois.edu/homes/guo29/files/cvpr11_shadow.pdf)
2. J.-F. Lalonde, A. A. Efros, S. G. Narasimhan, **Detecting Ground Shadowsin Outdoor Consumer Photographs**, ECCV 2010 [[PDF]](http://www.jflalonde.org/projects/shadows/lalonde_eccv_10.pdf)

## Optical Flow

### Resources

- Kanade-Lucas-Tomasi Feature Tracker [[C Code]](http://www.ces.clemson.edu/~stb/klt/)
- Optical Flow Matlab/C++ code by Ce Liu [[Project]](http://people.csail.mit.edu/celiu/OpticalFlow/)
- Horn and Schunck's method by Deqing Sun [[Code]](http://www.cs.brown.edu/~dqsun/code/hs.zip)
- Black and Anandan's method by Deqing Sun [[Code]](http://www.cs.brown.edu/~dqsun/code/ba.zip)
- Optical flow code by Deqing Sun [[Matlab Code]](http://www.cs.brown.edu/~dqsun/code/flow_code.zip) [[Project]](http://www.cs.brown.edu/~dqsun/research/software.html)
- Large Displacement Optical Flow by Thomas Brox [[Executable for 64-bit Linux]](http://www.cs.berkeley.edu/~brox/resources/pami2010Linux64.zip) [[ Matlab Mex-functions for 64-bit Linux and 32-bit Windows]](http://www.cs.berkeley.edu/~brox/resources/pami2010Matlab.zip) [[Project]](http://www.cs.berkeley.edu/~brox/code.html)
- Variational Optical Flow by Thomas Brox [[Executable for 64-bit Linux]](http://www.cs.berkeley.edu/~brox/resources/eccv2004Linux64.zip) [[ Executable for 32-bit Windows ]](http://www.cs.berkeley.edu/~brox/resources/eccv2004Windows.zip) [[ Matlab Mex-functions for 64-bit Linux and 32-bit Windows ]](http://www.cs.berkeley.edu/~brox/resources/eccv2004Matlab.zip) [[Project]](http://www.cs.berkeley.edu/~brox/code.html)

### References

1. B.D. Lucas and T. Kanade, **An Iterative Image Registration Technique with an Application to Stereo Vision**, IJCAI 1981. [[PDF]](http://www.google.com/url?sa=t&source=web&cd=3&ved=0CC8QFjAC&url=http://ijcai.org/Past%20Proceedings/IJCAI-81-VOL-2/PDF/017.pdf&ei=2C0OTryPILLDsQL1oNyYCg&usg=AFQjCNEXx-32X0w4rJ6d1I2IVfJQtXfTWw&sig2=rN8inAm7Yui5UgU5Ud7ZLw)
2. J. Shi, C. Tomasi, **Good Feature to Track**, CVPR 1994. [[PDF]](http://faculty.cs.tamu.edu/jchai/CPSC641/shi_tomasi_94.pdf)
3. C. Liu. **Beyond Pixels: Exploring New Representations and Applications for Motion Analysis**. *Doctoral Thesis*. MIT 2009. [[PDF]](http://www.google.com/url?sa=t&source=web&cd=4&ved=0CDMQFjAD&url=http://dspace.mit.edu/bitstream/handle/1721.1/53293/549097790.pdf?sequence=1&ei=rS0OTp_gF-bksQLmgNmSCg&usg=AFQjCNG48X7YFWRjyTTs_x8qztE_smejHw&sig2=gFRKnqTVFCLXKamySkE9YQ)
4. B.K.P. Horn and B.G. Schunck, **Determining Optical Flow**, *Artificial Intelligence*, 1981. [[PDF]](http://citeseer.ist.psu.edu/viewdoc/download;jsessionid=25F0703789BF4763DEA189E2FB981292?doi=10.1.1.66.562&rep=rep1&type=pdf)
5. M. J. Black and P. Anandan, **A framework for the robust estimation of optical flow**, ICCV 93. [[PDF]](http://www.cs.brown.edu/research/pubs/pdfs/1993/Black-1993-FRE.pdf)
6. D. Sun, S. Roth, and M. J. Black, **Secrets of optical flow estimation and their principles**, CVPR 2010. [[PDF]](http://www.cs.brown.edu/~dqsun/pubs/cvpr_2010_flow.pdf)
7. T. Brox, J. Malik, **Large displacement optical flow: descriptor matching in variational motion estimation**, PAMI, 2010 [[PDF]](http://lmb.informatik.uni-freiburg.de/people/brox/pub/brox_tpami10_ldof.pdf)
8. T. Brox, A. Bruhn, N. Papenberg, J. Weickert, **High accuracy optical flow estimation based on a theory for warping**, ECCV 2004 [[PDF]](http://lmb.informatik.uni-freiburg.de/people/brox/pub/brox_eccv04_of.pdf)

## Object Tracking

### Resources

- Particle filter object tracking [1] [[Project]](http://blogs.oregonstate.edu/hess/code/particles/)
- KLT Tracker [2-3] [[Project]](http://www.ces.clemson.edu/~stb/klt/)
- MILTrack [4] [[Code]](http://vision.ucsd.edu/~bbabenko/data/MilTracker-V1.0.zip)
- Incremental Learning for Robust Visual Tracking [5] [[Project]](http://www.cs.toronto.edu/~dross/ivt/)
- Online Boosting Trackers [6-7] [[Project]](http://www.vision.ee.ethz.ch/boostingTrackers/index.htm)
- L1 Tracking [8] [[Matlab code]](http://www.dabi.temple.edu/~hbling/code/L1_Tracking_v4_release.zip)

### References

1. P. Perez, C. Hue, J. Vermaak, and M. Gangnet. **Color-Based Probabilistic Tracking**, ECCV, 2002. [[PDF]](http://www.irisa.fr/vista/Papers/2002/perez_hue_eccv02.pdf)
2. B.D. Lucas and T. Kanade, **An Iterative Image Registration Technique with an Application to Stereo Vision**, IJCAI 1981. [[PDF]](http://www.google.com/url?sa=t&source=web&cd=3&ved=0CC8QFjAC&url=http://ijcai.org/Past%20Proceedings/IJCAI-81-VOL-2/PDF/017.pdf&ei=2C0OTryPILLDsQL1oNyYCg&usg=AFQjCNEXx-32X0w4rJ6d1I2IVfJQtXfTWw&sig2=rN8inAm7Yui5UgU5Ud7ZLw)
3. J. Shi, C. Tomasi, **Good Feature to Track**, CVPR 1994. [[PDF]](http://faculty.cs.tamu.edu/jchai/CPSC641/shi_tomasi_94.pdf)
4. B. Babenko, M. H. Yang, S. Belongie, **Robust Object Tracking with Online Multiple Instance Learning**, PAMI 2011 [[PDF]](http://vision.ucsd.edu/~bbabenko/data/miltrack-pami-final.pdf)
5. D. Ross, J. Lim, R.-S. Lin, M.-H. Yang, **Incremental Learning for Robust Visual Tracking**, IJCV 2007 [[PDF]](http://www.cs.toronto.edu/~dross/ivt/RossLimLinYang_ijcv.pdf)
6. H. Grabner, and H. Bischof, **On-line Boosting and Vision**, CVPR 2006 [[PDF]](http://www.vision.ee.ethz.ch/boostingTrackers/Grabner2006On-lineBoostingand.pdf)
7. H. Grabner, C. Leistner, and H. Bischof, **Semi-supervised On-line Boosting for Robust Tracking**, ECCV 2008 [[PDF]](http://www.vision.ee.ethz.ch/boostingTrackers/Grabner2008Semi-supervisedOn-lineboosting.pdf)
8. X. Mei and H. Ling, **Robust Visual Tracking using L1 Minimization**, ICCV, 2009. [[PDF]](http://www.dabi.temple.edu/~hbling/publication/09-tracking-iccv.pdf)

## Image Matting

### Resources

- Closed Form Matting [[Code]](http://people.csail.mit.edu/alevin/matting.tar.gz)
- Spectral Matting [[Project]](http://www.vision.huji.ac.il/SpectralMatting/)
- Learning-based Matting [[Code]](http://www.mathworks.com/matlabcentral/fileexchange/31412)

### References

1. A. Levin D. Lischinski and Y. Weiss. **A Closed Form Solution to Natural Image Matting**, PAMI 2008 [[PDF]](http://www.wisdom.weizmann.ac.il/~levina/papers/Matting-Levin-Lischinski-Weiss-PAMI.pdf)
2. A. Levin, A. Rav-Acha, D. Lischinski. **Spectral Matting**. PAMI 2008. [[PDF]](http://www.wisdom.weizmann.ac.il/~levina/papers/spectral-matting-levin-etal-pami08.pdf)
3. Y. Zheng and C. Kambhamettu, **Learning Based Digital Matting**, ICCV 2009 [[PDF]](http://vims.cis.udel.edu/publications/matting_iccv09_Zheng.pdf)

## Bilateral Filtering

### Resources

- Fast Bilateral Filter [[Project]](http://people.csail.mit.edu/sparis/bf/)
- Real-time O(1) Bilateral Filtering [[Code]](http://vision.ai.uiuc.edu/~qyang6/publications/code/qx_constant_time_bilateral_filter_ss.zip)
- SVM for Edge-Preserving Filtering [[Code]](http://vision.ai.uiuc.edu/~qyang6/publications/code/cvpr-10-svmbf/program_video_conferencing.zip)

### References

1. Q. Yang, K.-H. Tan and N. Ahuja, **Real-time O(1) Bilateral Filtering**, CVPR 2009. [[PDF]](http://vision.ai.uiuc.edu/~qyang6/publications/cvpr-09-qingxiong-yang.pdf)
2. Q. Yang, S. Wang, and N. Ahuja, **SVM for Edge-Preserving Filtering**, CVPR 2010. [[PDF]](http://vision.ai.uiuc.edu/~qyang6/publications/cvpr-10-qingxiong-yang-svmbf.pdf)

## Image Denoising

### Resources

- K-SVD [[Matlab code]](http://www.cs.technion.ac.il/~ronrubin/Software/ksvdbox13.zip)
- BLS-GSM [[Project]](http://decsai.ugr.es/~javier/denoise/)
- BM3D [[Project]](http://www.cs.tut.fi/~foi/GCF-BM3D/)
- FoE [[Code]](http://www.cs.brown.edu/~roth/research/software.html)
- GFoE [[Code]](http://www.cs.huji.ac.il/~yweiss/BRFOE.zip)
- Non-local means [[Code]](http://dmi.uib.es/~abuades/codis/NLmeansfilter.m)
- Kernel regression [[Code]](http://www.soe.ucsc.edu/~htakeda/MatlabApp/KernelRegressionBasedImageProcessingToolBox_ver1-1beta.zip)

## Image Super-Resolution

### Resources

- MRF for image super-resolution [[Project]](http://people.csail.mit.edu/billf/project%20pages/sresCode/Markov%20Random%20Fields%20for%20Super-Resolution.html)
- Multi-frame image super-resolution [[Project]](http://www.robots.ox.ac.uk/~vgg/software/SR/index.html)
- UCSC Super-resolution [[Project]](http://www.soe.ucsc.edu/~milanfar/SR-Software.htm)
- Sprarse coding super-resolution [[Code]](http://www.ifp.illinois.edu/~jyang29/codes/CVPR08-SR.rar)

## Image Deblurring

### Resources

- Eficient Marginal Likelihood Optimization in Blind Deconvolution [[Code]](http://www.wisdom.weizmann.ac.il/~levina/papers/LevinEtalCVPR2011Code.zip)
- Analyzing spatially varying blur [[Project]](http://www.eecs.harvard.edu/~ayanc/svblur/)
- Radon Transform [[Code]](http://people.csail.mit.edu/taegsang/Documents/RadonDeblurringCode.zip)

## Image Quality Assessment

### Resources

- FSIM [1] [[Project]](http://www4.comp.polyu.edu.hk/~cslzhang/IQA/FSIM/FSIM.htm)
- Degradation Model [2] [[Project]](http://users.ece.utexas.edu/~bevans/papers/2000/imageQuality/index.html)
- SSIM [3] [[Project]](https://ece.uwaterloo.ca/~z70wang/research/ssim/)
- SPIQA [[Code]](http://vision.ai.uiuc.edu/~bghanem2/shared_code/SPIQA_code.zip)

### References

1. L. Zhang, L. Zhang, X. Mou and D. Zhang, **FSIM: A Feature Similarity Index for Image Quality Assessment**, TIP 2011. [[PDF]](http://www4.comp.polyu.edu.hk/~cslzhang/IQA/TIP_IQA_FSIM.pdf)
2. N. Damera-Venkata, and T. D. Kite, W. S. Geisler, B. L. Evans, and A. C. Bovik, **Image Quality Assessment Based on a Degradation Model**, TIP 2000. [[PDF]](http://www.hpl.hp.com/personal/Niranjan_Damera-Venkata/files/iq.pdf)
3. Z. Wang, A. C. Bovik, H. R. Sheikh and E. P. Simoncelli, **Image quality assessment: from error visibility to structural similarity**, TIP 2004. [[PDF]](http://www.google.com/url?sa=t&source=web&cd=1&ved=0CBkQFjAA&url=http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.11.2477&rep=rep1&type=pdf&ei=pjwOTtCsGoKHsAKYpY37CQ&usg=AFQjCNH8Vs8aq-5gjPUVcCWSAowj0UND8A&sig2=e7aSpy_ms0jHPJDWJdT_YQ)
4. B. Ghanem, E. Resendiz, and N. Ahuja, **Segmentation-Based Perceptual Image Quality Assessment (SPIQA)**, ICIP 2008. [[PDF]](http://vision.ai.uiuc.edu/~bghanem2/Files/SPIQA_ICIP08.pdf)

## Density Estimation

### Resources

- Kernel Density Estimation Toolbox [[Project]](http://www.ics.uci.edu/~ihler/code/kde.html)

## Dimension Reduction

### Resources

- Dimensionality Reduction Toolbox [[Project]](http://homepage.tudelft.nl/19j49/Matlab_Toolbox_for_Dimensionality_Reduction.html)
- ISOMAP [[Code]](http://isomap.stanford.edu/)
- LLE [[Project]](http://www.cs.nyu.edu/~roweis/lle/code.html)
- Laplacian Eigenmaps [[Code]](http://www.cse.ohio-state.edu/~mbelkin/algorithms/Laplacian.tar)
- Diffusion maps [[Code]](http://www.stat.cmu.edu/~annlee/software.htm)

## Nearest Neighbors matching

### Resources

- ANN: Approximate Nearest Neighbor Searching [[Project]](http://www.cs.umd.edu/~mount/ANN/) [[Matlab wrapper]](http://www.wisdom.weizmann.ac.il/~bagon/matlab_code/ann_wrapper_July2010.tar.gz)
- FLANN: Fast Library for Approximate Nearest Neighbors [[Project]](http://www.cs.ubc.ca/~mariusm/index.php/FLANN/FLANN)

## Steoreo

### Resources

- StereoMatcher [[Project]](http://vision.middlebury.edu/stereo/code/)

### References

1. D. Scharstein and R. Szeliski. **A taxonomy and evaluation of dense two-frame stereo correspondence algorithms**, IJCV 2002 [[PDF]](http://vision.middlebury.edu/stereo/taxonomy-IJCV.pdf)

## Structure from motion

### Resources

- Boundler [1] [[Project]](http://phototour.cs.washington.edu/bundler/)

### References

1. N. Snavely, S. M. Seitz, R. Szeliski. **Photo Tourism: Exploring image collections in 3D**. SIGGRAPH, 2006. [[PDF]](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.62.910&rep=rep1&type=pdf)

## Distance Transformation

### Resources

- Distance Transforms of Sampled Functions [1] [[Project]](http://cs.brown.edu/~pff/dt/)

### References

1. P. F. Felzenszwalb and D. P. Huttenlocher. **Distance transforms of sampled functions**. Technical report, Cornell University, 2004. [[PDF]](http://www.google.com/url?sa=t&source=web&cd=1&ved=0CBsQFjAA&url=http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.88.1647&rep=rep1&type=pdf&ei=fTYOTuz3KomgsQLR_4WkCg&usg=AFQjCNFYPzi2T5cIhFvBfRr9fLcvQhtovw&sig2=kQXOFjisyE0F_bFVcLrreQ)

## Chamfer Matching

### Resources

- Fast Directional Chamfer Matching [[Code]](http://www.umiacs.umd.edu/~mingyliu/src/fdcm_matlab_wrapper_v0.2.zip)

### References

1. M.-Y. Liu, O. Tuzel, A. Veeraraghavan, and R. Chellappa, **Fast Directional Chamfer Matching**, CVPR 2010 [[PDF]](http://www.umiacs.umd.edu/~mingyliu/papers/liu_cvpr2010.pdf)

## Clustering

### Resources

- K-Means [[VLFeat]](http://www.vlfeat.org/) [[Oxford code]](http://www.cs.ucf.edu/~vision/Code/vggkmeans.zip)
- Spectral Clustering [[UW Project]](http://www.stat.washington.edu/spectral/) [[Code]](http://vision.ucsd.edu/~sagarwal/spectral-0.2.tgz) [[Self-Tuning code]](http://www.vision.caltech.edu/lihi/Demos/SelfTuningClustering.html)
- Affinity Propagation [[Project]](http://www.psi.toronto.edu/index.php?q=affinity%20propagation)

## Classification

### Resources

- SVM [[Libsvm]](http://www.csie.ntu.edu.tw/~cjlin/libsvm/) [[SVM-Light]](http://svmlight.joachims.org/) [[SVM-Struct]](http://svmlight.joachims.org/)
- Boosting
- Naive Bayes

## Multiple Kernel Learning (MKL)

### Resources

- SHOGUN [[Project]](http://www.shogun-toolbox.org/)
- OpenKernel.org [[Project]](http://www.openkernel.org/)
- DOGMA (online algorithms) [[Project]](http://dogma.sourceforge.net/)
- SimpleMKL [[Project]](http://asi.insa-rouen.fr/enseignants/~arakotom/code/mklindex.html)

### References

1. S. Sonnenburg, G. Rätsch, C. Schäfer, B. Schölkopf. **Large scale multiple kernel learning**. JMLR, 2006. [[PDF]](http://www.jmlr.org/papers/volume7/sonnenburg06a/sonnenburg06a.pdf)
2. F. Orabona and L. Jie. **Ultra-fast optimization algorithm for sparse multi kernel learning**. ICML, 2011. [[PDF]](http://www.icml-2011.org/papers/205_icmlpaper.pdf)
3. F. Orabona, L. Jie, and B. Caputo. **Online-batch strongly convex multi kernel learning**. CVPR, 2010. [[PDF]](http://francesco.orabona.com/papers/10cvpr_a.pdf)
4. A. Rakotomamonjy, F. Bach, S. Canu, and Y. Grandvalet. **Simplemkl**. JMRL, 2008. [[PDF]](http://eprints.pascal-network.org/archive/00004733/01/rakotomamonjy08a.pdf)

## Multiple Instance Learning (MIL)

### Resources

- MIForests [1] [[Project]](http://www.ymer.org/amir/software/milforests/)
- MILIS [2]
- MILES [3] [[Project]](http://infolab.stanford.edu/~wangz/project/imsearch/SVM/PAMI06/) [[Code]](http://www.cs.olemiss.edu/~ychen/MILES.html)
- DD-SVM [4] [[Project]](http://www.cs.olemiss.edu/~ychen/ddsvm.html)

### References

1. C. Leistner, A. Saffari, and H. Bischof, MIForests: **Multiple-Instance Learning with Randomized Trees**, ECCV 2010. [[PDF]](http://www.ymer.org/papers/files/2010-MILForests.pdf)
2. Z. Fu, A. Robles-Kelly, and J. Zhou, **MILIS: Multiple instance learning with instance selection**, PAMI 2010. [[PDF]](http://users.cecs.anu.edu.au/~arobkell/papers/pami10.pdf)
3. Y. Chen, J. Bi and J. Z. Wang, **MILES: Multiple-Instance Learning via Embedded Instance Selection**. PAMI 2006 [[PDF]](http://infolab.stanford.edu/~wangz/project/imsearch/SVM/PAMI06/chen.pdf)
4. Yixin Chen and James Z. Wang, **Image Categorization by Learning and Reasoning with Regions**, JMLR 2004. [[PDF]](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.1.5285&rep=rep1&type=pdf)

## Other Utilities

- Code for downloading Flickr images, by James Hays [[Code]](http://graphics.cs.cmu.edu/projects/im2gps/flickr_code.html)
- The Lightspeed Matlab Toolbox by Tom Minka [[Code]](http://research.microsoft.com/en-us/um/people/minka/software/lightspeed/)
- MATLAB Functions for Multiple View Geometry [[Code]](http://www.robots.ox.ac.uk/~vgg/hzbook/code/)
- Peter's Functions for Computer Vision [[Code]](http://www.csse.uwa.edu.au/~pk/research/matlabfns/#match)
- Statistical Pattern Recognition Toolbox [[Code]](http://cmp.felk.cvut.cz/cmp/software/stprtool/)
 
-----

## Useful Links (dataset, lectures, and other softwares)

### Conference Information

- [Computer Image Analysis, Computer Vision Conferences](http://conferences.visionbib.com/Iris-Conferences.html)

### Papers

- [Computer vision paper on the web](http://www.cvpapers.com/index.html)

- [NIPS Proceedings](http://books.nips.cc/)

### Datasets

- [Compiled list of recognition datasets](http://www.cs.utexas.edu/~grauman/courses/spring2008/datasets.htm)

- [Computer vision dataset from CMU](http://www.cs.cmu.edu/~cil/v-images.html)

### Lectures

- [Videolectures](http://videolectures.net/)

### Source Codes

- [Computer Vision Algorithm Implementations](http://www.cvpapers.com/rr.html)

- [OpenCV](http://opencv.willowgarage.com/wiki/)

- [Source Code Collection for Reproducible Research](http://www.csee.wvu.edu/~xinl/reproducible_research.html)
