
# Empirical distribution mixture models

For your reference, please see and cite the [preprint uploaded to bioRxiv.](https://www.biorxiv.org/content/10.1101/794263v1)

Empirical distribution mixture models assume that evolution occurs along a
species tree according to a mixture of amino acid substitution models. The
transition rate matrices of the different components share one set of
exchangeabilities but differ in their stationary distributions.

**EDCluster** is a Python script obtaining empirical stationary distributions with
corresponding weights from a set of site distributions. A site distribution is
the probability distribution of used amino acids at a specific site in the
alignment. Consequently, site distributions are are points in 20-dimensional
space with elements summing up to 1.0.

Site distributions can be calculated during Bayesian analysis, for example with
Phylobayes and the CAT model [1] . In this case, a site distribution corresponds
to the expectation of the posterior distribution of the stationary distribution
of amino acids at a specific site.

The script presented here can transform the site distributions before further
analysis. Application of linear transformations is a standard procedure in
analyses of compositional data. The two provided transformations are: (1) the
centered log ratio transformation (CLR, [2]), and (2) the log centered log ratio
transformation (LCLR, [3]). The transformations ensure that site distributions
exhibiting specific different features are moved further apart from each other,
so that they fall into different groups in the subsequent analysis.

K-means clustering with Scikit-Learn [4] is used to group the prepared site
distributions into 4, 8, 16, 32, 64, 128, and 256 clusters. The cluster centers,
which are the stationary distributions, and weights can be used as components of
EDM models.

Further, sets of stationary distributions and weights estimated from subsets of
the HOGENOM [5] and HSSP [6] data bases, as well as a union of both are
provided. Empirical distribution mixture models resulting from these sets have
been termed **UDM models**. The files can directly be used with several
established phylogenetic softwware packages such as IQ-TREE [7], Phylobayes [8],
or RevBayes [9].

    usage: EDCluster [-h] [-t {none,clr,lclr}] [-k K] [-n] [-p P] [--pickle-only]
                     [--continue-run] [-v]
                     [filenames [filenames ...]]
    
    EDCluster version 2.0.0.
    Developed by Dominik Schrempf (2020). 
    
    Scalable detection of empirical distribution mixture models by
    transformation and clustering of site distributions. Each amino acid frequency
    distribution is considered as a point in twenty dimensional space. The K-Means
    clustering algorithm is used to label the points from 1 to K, for a given value
    of K. The clusters are output in various file formats, readily usable with
    IQ-TREE [1], Phylobayes [2], and RevBayes [3].
    
    Before clustering, coordinate transformations can be applied.
    
    Implemented transformations:
    - centered log ratio (CLR) transform [4]
    - log centered log ratio (LCLR) transform [5]
    
    Points close to the boundaries, that is, with some coordinates having low
    probability, exhibit special features. The coordinate transformations project
    these points to a position far away from the projection of points with high
    diversity and intermediate frequency values for all coordinates.
    
    The site distribution files are expected to be tab separated, and of the
    following form:
    
    ----------------------------------------------------------------------
      A C D E F G H I K L M N P Q R S T V W Y
    
    1 0.008 0.001 0.001 0.007 0.002 0.004 0.01 ...
    2 ...
    ...
    ----------------------------------------------------------------------
    
    By default, EDcluster calculates mixture model components of empirical
    distribution mixture (EDM) models for K={4,8,16,32,64,128,256,512,1024,2048},
    and all coordinate transformations. This can take a while. Calculation of an
    EDM model with a specific number of components, as well as a specific
    transformation can be achieved with the -k, and -t options (see below). 
    
    positional arguments:
      filenames           Names of files containing site distributions (default:
                          None)
    
    optional arguments:
      -h, --help          show this help message and exit
      -t {none,clr,lclr}  Use specific transformation. (default: None)
      -k K                Use specific number of clusters. (default: None)
      -n                  Also create Nicologos. (default: False)
      -p P                Prefix of output files. (default: None)
      --pickle-only       Read, transform, and save data; then exit. (default:
                          False)
      --continue-run      Use saved data for clustering. (default: False)
      -v                  show program's version number and exit
    
    [1] Nguyen, L., Schmidt, H. A., von Haeseler, A., & Minh, B. Q. (2015).
    Iq-tree: a fast and effective stochastic algorithm for estimating
    maximum-likelihood phylogenies. Molecular Biology and Evolution, 32(1),
    268–274. http://dx.doi.org/10.1093/molbev/msu300
    
    [2] Lartillot, N., Rodrigue, N., Stubbs, D., & Richer, J. (2013). Phylobayes
    mpi: phylogenetic reconstruction with infinite mixtures of profiles in a
    parallel environment. Systematic Biology, 62(4), 611–615.
    http://dx.doi.org/10.1093/sysbio/syt022
    
    [3] Höhna, S., Landis, M. J., Heath, T. A., Boussau, B., Lartillot, N., Moore,
    B. R., Huelsenbeck, J. P., … (2016). Revbayes: bayesian phylogenetic inference
    using graphical models and an interactive model-specification language.
    Systematic Biology, 65(4), 726–736. http://dx.doi.org/10.1093/sysbio/syw021
    
    [4] Aitchison, J. (1982). The statistical analysis of compositional data.
    Journal of the Royal Statistical Society, Series B (Methological), 44(2),
    139–177.
    
    [5] Godichon-Baggioni, A., Maugis-Rabusseau, C., & Rau, A. (2017).
    Clustering transformed compositional data using K-means, with applications in
    gene expression and bicycle sharing system data. ArXiv, 1–32.

