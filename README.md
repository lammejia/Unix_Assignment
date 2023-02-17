#Ludvin Mejia
#UNIX Assignment

##Data Inspection

###Attributes of `fang_et_al_genotypes`
To get number of lines, words, and characters. 

```
$ wc fang_et_al_genotypes.txt
```
To get file size.

```
$ du -h fang_et_al_genotypes.txt
```

To get number of columns.

```
$ awk -F "\t" {print NF; exit}' fang_et_al_genotype.txt
```
To get file type

```
$ file fang_et_al_genotypes.txt
```






By inspecting this file I learned that:

1. There are 2783 lines, 2744038 words, and 11051939 characters
2. The sizes is 6.1M
3. The file is ascii text with very long lines
4. There are 986 columns


###Attributes of `snp_position.txt`
To get number of lines, words, and characters. 

```
$ wc snp_position.txt 
```

To get file size.

```
$ du -h snp_position.txt
```

To get what type of file type I'm working with.

```
$ file snp_position.txt
```
To count the number of columns.

```
$ awk -F "\t' {print NF; exit} snp_position.txt
```

By inspecting this file I learned that:

1. There are 984 lines, 13198 words, and 82763 characters.
2. The size is 38K M
3. The file is ascii txt
4. There are 15 columns.


##Data Processing

###Maize Data


With both of my sorted snp and maize data I then joined using the common column (SNP ID) using the following code:

```
$ join -1 1 -2 1 -t $'\t' final_snp.txt sorted_maize.txt > joined_maize.txt
```

I then got rid of unnecessary columns and just kept chromosome number, location, and SNP ID.

```
$ cut -f 1,3,4,16- joined_maize.txt > cleaned_joined_maize.txt
```
With my joined file I then separated out chromosome numbers from the file and created its own file. i indicates a chromosome number I did this indiviually for chromosome 1-10.

```
$ awk '$2 ~ /^i$/' cleaned_joined_maize.txt > chri_maize.txt #^i$ > chri_maize.txt
```

Chromosomes (i=1..10) were arranged from increasing position with - replaced to ? using the following code:

```
$ sed 's/-/?/g' chri_maize.txt | sort -k3,3n > chri_fwd_maize.txt
```

I sorted in reverse and replaced ? to - using the following code (i=1..10):

```
$ sed's/?/-/g' chri_maize.txt | sort -k3,3nr > chri_rev_maize.txt
```

Finding multiple positions.
``` 
$ grep multiple cleaned_joined_maize.txt > multiple_maize.txt
```

Finding unknown positions.


```
$ grep unknown cleaned_joined_maize.txt > unknown_maize.txt
```



###Teosinte Data

For teosinte my code was very similar to the one run above.



First I created a file with the headers on the file using the following code.

```
$ head -n 1 fang_et_al_genotypes.txt > maize_fang.txt
```

I then used grep to find all maize data and added it to the file with my header using the following code. The >> tells Unix not to edit the file but rather to add onto it.

```
$ grep -E "(ZMMIL|ZMMLR|ZMMR)" fange_et_al_genotypes.txt >> maize_fang.txt
```

Then using the code provided by Dr. Hufford I transposed the data with the following code.

```
$ awk -f transpose.awk maize_fang.txt > transposed_maize.txt
```

I then got rid of any header data which is unnecessary.

```
$ tail -n +4 transposed_maize.txt > headless_maize.txt
```
I then sorted my headless_maize.txt using the following code.

```
$ sort -k1,1 headless_maize.txt > sorted_maize.txt
```

I then started working on my snp_position.txt by first getting rid of the header using the following code.

```
$ tail -n +1 snp_position.txt > headless_snp_position.txt
```

I then sorted my 
headless snp position.txt with the following code:

```
$ sort -k1,1 headless_snp_position.txt > final_snp.txt
```


Here is my brief description of what this code does


hello this is hahahahaha