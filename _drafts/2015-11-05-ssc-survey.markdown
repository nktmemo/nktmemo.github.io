---
layout: post
title:  "Semi-Supervised Clustering: A Survey"
date:   2015-11-05 18:44:46 +0900
categories: jekyll update
---
- Wagstaff, Kiri, et al. "Constrained k-means clustering with background knowledge." ICML. Vol. 1. 2001.

- Basu, Sugato, Mikhail Bilenko, and Raymond J. Mooney. "A probabilistic framework for semi-supervised clustering." Proceedings of the tenth ACM SIGKDD international conference on Knowledge discovery and data mining. ACM, 2004.

- Lu, Zhengdong. "Semi-supervised clustering with pairwise constraints: A discriminative approach." International Conference on Artificial Intelligence and Statistics. 2007. (**constrained spectral clustering**)
- Lu, Zhengdong, and Miguel Carreira-Perpinan. "Constrained spectral clustering through affinity propagation." Computer Vision and Pattern Recognition, 2008. CVPR 2008. IEEE Conference on. IEEE, 2008. (**constrained spectral clustering**)

- Kulis, Brian, et al. "Semi-supervised graph clustering: a kernel approach."Machine learning 74.1 (2009): 1-22. (**sskm**)

- Lu, Zhiwu, and Horace HS Ip. "Constrained spectral clustering via exhaustive and efficient constraint propagation." Computer Vision–ECCV 2010. Springer Berlin Heidelberg, 2010. 1-14.

- Lelis, Levi, and Jörg Sander. "Semi-supervised density-based clustering." Data Mining, 2009. ICDM'09. Ninth IEEE International Conference on. IEEE, 2009.
SSDBSCAN is a semi-supervised variant of DBSCAN that explicitly
uses the labels of a few points to determine the neighborhood parameters

- Ruiz, Carlos, Myra Spiliopoulou, and Ernestina Menasalvas. "Density-based semi-supervised clustering." Data mining and knowledge discovery 21.3 (2010): 345-370
C-DBSCAN

- Calandriello, Daniele, Gang Niu, and Masashi Sugiyama. "Semi-supervised information-maximization clustering." Neural Networks 57 (2014): 103-111

**SS Mode seeking (without fixing the number of clusters):**
- Tuzel, Oncel, Fatih Porikli, and Peter Meer. "Kernel methods for weakly supervised mean shift clustering." Computer Vision, 2009 IEEE 12th International Conference on. IEEE, 2009.
must-link only

- Anand, Sruthy, et al. "Semi-supervised kernel mean shift clustering." Pattern Analysis and Machine Intelligence, IEEE Transactions on 36.6 (2014): 1201-1215.

# Applications
- automatically detecting road lanes from GPS data

- gene clustering (classification) - the Database of Interacting Proteins (DIP) data set in biology contains information about proteins co-occurring in processes, which can be viewed as must-link constraints during gene clustering  
[*] Segal, Eran, Haidong Wang, and Daphne Koller. "Discovering molecular pathways from protein interaction and gene expression data." Bioinformatics19.suppl 1 (2003): i264-i272.

- graph clustering - Constraints of this form are also natural in the context of the graph clustering problem (a.k.a. graph partitioning or vertex partitioning), where edges in the graph encode pairwise relationships

- information retrieval: the expert critique is often in the form “these two documents shouldn’t be in the same  
[*] Cohn, David, Rich Caruana, and Andrew McCallum. "Semi-supervised clustering with user feedback." Constrained Clustering: Advances in Algorithms, Theory, and Applications 4.1 (2003): 17-32.

mode-seeking (without the number of clusters):

SS mode seeking (without the number of clusters):
