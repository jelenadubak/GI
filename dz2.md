Exercise 2



```python

!pip install pysam

```

    Requirement already satisfied: pysam in /usr/local/lib/python3.7/dist-packages (0.19.0)
    


```python
from pysam import AlignmentFile
path_to_file = "merged-tumor.bam"
cnt_unmapped = 0
cnt_total_reads = 0
cnt_mapping_quality_zero = 0
sum_mapping_quality = 0

for read in AlignmentFile(path_to_file):
    cnt_total_reads = cnt_total_reads + 1
    sum_mapping_quality = sum_mapping_quality + read.mapping_quality
    if read.mapping_quality == 0:
        cnt_mapping_quality_zero = cnt_mapping_quality_zero + 1
    if read.flag & 4:
        cnt_unmapped = cnt_unmapped + 1
avg_mapping_quality = sum_mapping_quality / cnt_total_reads
cnt_maping_quality_without_zeros = cnt_total_reads - cnt_mapping_quality_zero
avg_mapping_quality_without_zeros = sum_mapping_quality / cnt_maping_quality_without_zeros

print(f"Number of unmapped reads in the file: {cnt_unmapped}.")
print(f"Total number of reads: {cnt_total_reads}.")
print(f"Number of reads with mapping quality 0: {cnt_mapping_quality_zero}.")
print(f"Average mapping quality for all the reads: {avg_mapping_quality}.")
print(f"Average mapping quality if reads with mapping quality=0 are filtered out: {avg_mapping_quality_without_zeros}.")
```

    Number of unmapped reads in the file: 17765.
    Total number of reads: 2921629.
    Number of reads with mapping quality 0: 126628.
    Average mapping quality for all reads: 55.91379158681681.
    Average mapping quality if reads with mapping quality=0 are filtered out: 58.446975510921106.
    
