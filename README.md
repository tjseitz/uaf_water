# UAF Water project

### QIIME 2 filtering


[Tutorial on QIIME 2](https://docs.qiime2.org/2021.2/tutorials/filtering/)

Make a feature-table with only tap samples, both "cold" and "hot"

```
qiime feature-table filter-samples \
  --i-table table.qza \
  --m-metadata-file sample-metadata.tsv \
  --p-where "[water-type]='Tap'" \
  --o-filtered-table tap-table.qza
```

Make a feature-table with only "flush" and "main" water-type samples

```
qiime feature-table filter-samples \
  --i-table table.qza \
  --m-metadata-file sample-metadata.tsv \
  --p-where "[water-type] IN ('Flush', 'Main')" \
  --o-filtered-table flush-main-table.qza
  ```
  
  Make a feature-table with only "tap" and "main" water-type samples from "MBS"
  
  ```
  qiime feature-table filter-samples \
  --i-table table.qza \
  --m-metadata-file sample-metadata.tsv \
  --p-where "[water-type] IN ('Tap', 'Main') AND [location]='MBS'" \
  --o-filtered-table MBS-main-tap-table.qza
  ```
  
  
  
