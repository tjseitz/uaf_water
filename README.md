# UAF Water project

### QIIME 2 filtering


[Tutorial on QIIME 2](https://docs.qiime2.org/2021.2/tutorials/filtering/)

Make a feature-table with only tap samples, both "cold" and "hot"

```
qiime feature-table filter-samples \
  --i-table table.qza \
  --m-metadata-file uaf_water.16S.metadata.tsv \
  --p-where "[water-type]='Tap'" \
  --o-filtered-table tap-table.qza
```

Make a feature-table with only "flush" and "main" water-type samples

```
qiime feature-table filter-samples \
  --i-table table.qza \
  --m-metadata-file uaf_water.16S.metadata.tsv \
  --p-where "[water-type] IN ('Flush', 'Main')" \
  --o-filtered-table flush-main-table.qza
  ```
  
  Make a feature-table with only "tap" and "main" water-type samples from "MBS"
  
  ```
  qiime feature-table filter-samples \
  --i-table table.qza \
  --m-metadata-file uaf_water.16S.metadata.tsv \
  --p-where "[water-type] IN ('Tap', 'Main') AND [location]='MBS'" \
  --o-filtered-table MBS-main-tap-table.qza
  ```
  
  
  ## Now calculate the core diversity metrics for each filtered table
  
  Start with Tap water only
  
  ```
  qiime diversity core-metrics-phylogenetic \
  --i-phylogeny rooted-tree.qza \
  --i-table tap-table.qza \
  --p-sampling-depth 1103 \
  --m-metadata-file uaf_water.16S.metadata.tsv \
  --output-dir tap-core-metrics-results
  ```
  
   ```
  qiime diversity core-metrics-phylogenetic \
  --i-phylogeny rooted-tree.qza \
  --i-table tap-table.qza \
  --p-sampling-depth 1103 \
  --m-metadata-file uaf_water.16S.metadata.tsv \
  --output-dir flush-main-core-metrics-results
  ```
  
  
  ```
  qiime diversity core-metrics-phylogenetic \
  --i-phylogeny rooted-tree.qza \
  --i-table MBS-main-tap-table.qza \
  --p-sampling-depth 1103 \
  --m-metadata-file uaf_water.16S.metadata.tsv \
  --output-dir flush-main-core-metrics-results
  ```



Test for significance by one of the grouping factors, in this case water temp
```
qiime diversity beta-group-significance \
  --i-distance-matrix tap-core-metrics-results/unweighted_unifrac_distance_matrix.qza \
  --m-metadata-file uaf_water.16S.metadata.tsv \
  --m-metadata-column temperature \
  --o-visualization tap-core-metrics-results/unweighted-unifrac-temperature-significance.qzv \
  --p-pairwise
```
