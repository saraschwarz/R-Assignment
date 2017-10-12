#R final project
## Data Inspection
- read in data
  * snp <- read.table("snp_position.txt", header = TRUE, fill = TRUE)
  * fang <- read.table("fang_et_al_genotypes.txt", header = TRUE, fill = TRUE)
#### fang
- typeof(fang)
  * "list"
- class(fang)
  * "data.frame"
- str(fang)
  * 'data.frame':	2782 obs. of  986 variables:
- dim(fang)
  * 2782 rows 986 columns
#### snp_position
- typeof(snp)
  * "list"
- class(snp)
  * "data.frame"
- str(snp)
  * 'data.frame':	1017 obs. of  15 variables:
- dim(snp)
  * 1017 rows  15 columns
## Data Processing
#### Sorting Maize from Teosinte files
- Unique names in Group column
  * fnames <- unique(fang$Group)
- saved as characters
  * fnames <- as.character(unique(fang$Group))
- Pull out names for maize
  * fznames <- fnames[c(16, 14, 15)]
- Pull out names for teosinte
  * ftnames <- fnames[c(6, 12, 7)]
- Save rows that match maize names 
  * zfang <- fang[as.character(fang$Group) %in% fznames, ]
- Save rows that match teosinte names
  * tfang <- fang[as.character(fang$Group) %in% ftnames, ]
#### Maize file processing
- Save transposed maize file 
  * transz <- t(zfang)
- Save transposed maize file as a data frame with strings
  * transzdf <- as.data.frame(transz, stringsAsFactors = FALSE)
- Create column with row names of maize file
  * transzdf$sample_ID <- rownames(transzdf)
- !!!!
  * names(transzdf) <- as.character(transzdf[1,])
- Remove top 3 lines
  * transzdf <-  transzdf[-(1:3),]
- Merge snp file to maize file
  * zmerge <- merge(snp, transzdf, by.x = "SNP_ID", by.y = "Sample_ID")
#### Teosinte file processing
- Save transposed teosinte file 
  * transt <- t(tfang)
- Save transposed teosinte file as a data frame with strings
  * transtdf <- as.data.frame(transt, stringsAsFactors = FALSE)
- Create column with row names of teosinte file
  * transtdf$sample_ID <- rownames(transtdf)
- !!!!
  * names(transtdf) <- as.character(transtdf[1,])
- Remove top 3 lines
  * transtdf <-  transtdf[-(1:3),]
- Merge snp file to teosinte file
  * tmerge <- merge(snp, transtdf, by.x = "SNP_ID", by.y = "Sample_ID")
## Data Analysis 