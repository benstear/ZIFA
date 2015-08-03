# ZIFA
Zero-inflated dimensionality reduction algorithm for single-cell data.

Reference: Dimensionality reduction for zero-inflated single cell gene expression analysis. 

Algorithm code is contained in ZIFA.py and block_ZIFA.py. We recommend using block_ZIFA, which subsamples genes in blocks to increase efficiency, for datasets with more than a few thousand genes; it should yield similar results to ZIFA. Runtime for block ZIFA on the full single-cell dataset from Pollen et al, 2014 (~250 samples, ~20,000 genes) is approximately 15 minutes on a quadcore Mac Pro. 

Sample usage: 

import ZIFA

Z, model_params = ZIFA.fitModel(Y, k)

or 

import block_ZIFA

Z, model_params = block_ZIFA.fitModel(Y, k)
 
or 

Z, model_params = block_ZIFA.fitModel(Y, k, n_blocks = desired_n_blocks)

where Y is the observed zero-inflated data, k is the desired number of latent dimensions, and Z is the low-dimensional projection and desired_n_blocks is the number of blocks to divide genes into. By default, the number of blocks is set to n_genes / 500 (yielding a block size of approximately 500). 

Runtime is roughly linear in the number of samples and the number of genes, and quadratic in the block size. 
Decreasing the block size may decrease runtime but will also produce less reliable results. 

See example.py for a full example demonstrating superior performance over factor analysis. 

This code requires pylab, scipy, numpy, and scikits.learn for full functionality. 
 
