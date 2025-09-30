```
module load module load blast/2.16.0+
```

download HLA database A_nuc.fasta, B_nuc.fasta, C_nuc.fasta

change the header to only keep the HLA type
```
sed -E 's/^>[^ ]+ ([^ ]+).*/>\1/' C_nuc.fasta > C_nuc_new_header.fasta
sed -E 's/^>[^ ]+ ([^ ]+).*/>\1/' B_nuc.fasta > B_nuc_new_header.fasta
sed -E 's/^>[^ ]+ ([^ ]+).*/>\1/' A_nuc.fasta > A_nuc_new_header.fasta
```

create the database
```
makeblastdb -in C_nuc_new_header.fasta -dbtype nucl -out HLA-C_db
makeblastdb -in B_nuc_new_header.fasta -dbtype nucl -out HLA-B_db
makeblastdb -in A_nuc_new_header.fasta -dbtype nucl -out HLA-A_db
```

make the prediction
```
blastn -query YiChen-HLC4.2383_F07_053.seq -db HLA-C_db -out YiChen-HLC4.2383_F07_053_HLA-C_results.txt -outfmt 6
blastn -query YiChen-HLB3.2381_A07_063.seq -db HLA-B_db -out YiChen-HLB3.2381_A07_063_HLA-B_results.txt -outfmt 6
blastn -query YiChen-HLB4.2381_B07_061.seq -db HLA-B_db -out YiChen-HLB4.2381_B07_061_HLA-B_results.txt -outfmt 6
blastn -query YiChen-HLC1.2383_C07_059.seq -db HLA-C_db -out YiChen-HLC1.2383_C07_059_HLA-C_results.txt -outfmt 6
blastn -query YiChen-HLC2.2383_D07_057.seq -db HLA-C_db -out YiChen-HLC2.2383_D07_057_HLA-C_results.txt -outfmt 6
blastn -query YiChen-HLC3.2383_E07_055.seq -db HLA-C_db -out YiChen-HLC3.2383_E07_055_HLA-C_results.txt -outfmt 6
```
