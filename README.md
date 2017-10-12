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
- Reorder columns into SNP ID, Chromosome, postition
  * colzmerge <- zmerge [,c(1,3,4,2,5:1588)]
- Seperate files by chromosome
  * ZChr1 <- colzmerge[colzmerge$Chromosome == "1",]
  * ZChr2 <- colzmerge[colzmerge$Chromosome == "2",]
  * ZChr3 <- colzmerge[colzmerge$Chromosome == "3",]
  * ZChr4 <- colzmerge[colzmerge$Chromosome == "4",]
  * ZChr5 <- colzmerge[colzmerge$Chromosome == "5",]
  * ZChr6 <- colzmerge[colzmerge$Chromosome == "6",]
  * ZChr7 <- colzmerge[colzmerge$Chromosome == "7",]
  * ZChr8 <- colzmerge[colzmerge$Chromosome == "8",]
  * ZChr9 <- colzmerge[colzmerge$Chromosome == "9",]  
  * ZChr10 <- colzmerge[colzmerge$Chromosome == "10",] 
- Sort position column in each chromosome file as ascending
  * zChr1ascend <- ZChr1[order(as.numeric(as.character(ZChr1$Position))),]
  * zChr2ascend <- ZChr2[order(as.numeric(as.character(ZChr2$Position))),]
  * zChr3ascend <- ZChr3[order(as.numeric(as.character(ZChr3$Position))),]
  * zChr4ascend <- ZChr4[order(as.numeric(as.character(ZChr4$Position))),]  
  * zChr5ascend <- ZChr5[order(as.numeric(as.character(ZChr5$Position))),]  
  * zChr6ascend <- ZChr6[order(as.numeric(as.character(ZChr6$Position))),]  
  * zChr7ascend <- ZChr7[order(as.numeric(as.character(ZChr7$Position))),]  
  * zChr8ascend <- ZChr8[order(as.numeric(as.character(ZChr8$Position))),]  
  * zChr9ascend <- ZChr9[order(as.numeric(as.character(ZChr9$Position))),] 
  * zChr107ascend <- ZChr10[order(as.numeric(as.character(ZChr10$Position))),] 
- Sort position column in each chromosome file as descending
  * zChr1descend <- ZChr1[order(as.numeric(as.character(ZChr1$Position)) , decreasing = TRUE),]
  * zChr2descend <- ZChr2[order(as.numeric(as.character(ZChr2$Position)) , decreasing = TRUE),]
  * zChr3descend <- ZChr3[order(as.numeric(as.character(ZChr3$Position)) , decreasing = TRUE),]
  * zChr4descend <- ZChr4[order(as.numeric(as.character(ZChr4$Position)) , decreasing = TRUE),] 
  * zChr5descend <- ZChr5[order(as.numeric(as.character(ZChr5$Position)) , decreasing = TRUE),]
  * zChr6descend <- ZChr6[order(as.numeric(as.character(ZChr6$Position)) , decreasing = TRUE),]
  * zChr7descend <- ZChr7[order(as.numeric(as.character(ZChr7$Position)) , decreasing = TRUE),] 
  * zChr8descend <- ZChr8[order(as.numeric(as.character(ZChr8$Position)) , decreasing = TRUE),] 
  * zhr9descend <- ZChr9[order(as.numeric(as.character(ZChr9$Position)) , decreasing = TRUE),]
  * zChr10descend <- ZChr10[order(as.numeric(as.character(ZChr10$Position)) , decreasing = TRUE),]  
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
- Reorder columns into SNP ID, Chromosome, postition
  * coltmerge <- tmerge [,c(1,3,4,2,5:990)]
- Seperate files by chromosome
  * tChr1 <- coltmerge[coltmerge$Chromosome == "1",]
  * tChr2 <- coltmerge[coltmerge$Chromosome == "2",]
  * tChr3 <- coltmerge[coltmerge$Chromosome == "3",]
  * tChr4 <- coltmerge[coltmerge$Chromosome == "4",]
  * tChr5 <- coltmerge[coltmerge$Chromosome == "5",]
  * tChr6 <- coltmerge[coltmerge$Chromosome == "6",]
  * tChr7 <- coltmerge[coltmerge$Chromosome == "7",]
  * tChr8 <- coltmerge[coltmerge$Chromosome == "8",]
  * tChr9 <- coltmerge[coltmerge$Chromosome == "9",]  
  * tChr10 <- coltmerge[coltmerge$Chromosome == "10",] 
- Sort position column in each chromosome file as ascending
  * tChr1ascend <- tChr1[order(as.numeric(as.character(tChr1$Position))),]
  * tChr2ascend <- tChr2[order(as.numeric(as.character(tChr2$Position))),]
  * tChr3ascend <- tChr3[order(as.numeric(as.character(tChr3$Position))),]
  * tChr4ascend <- tChr4[order(as.numeric(as.character(tChr4$Position))),]  
  * tChr5ascend <- tChr5[order(as.numeric(as.character(tChr5$Position))),]  
  * tChr6ascend <- tChr6[order(as.numeric(as.character(tChr6$Position))),]  
  * tChr7ascend <- tChr7[order(as.numeric(as.character(tChr7$Position))),]  
  * tChr8ascend <- tChr8[order(as.numeric(as.character(tChr8$Position))),]  
  * tChr9ascend <- tChr9[order(as.numeric(as.character(tChr9$Position))),] 
  * tChr107ascend <- tChr10[order(as.numeric(as.character(tChr10$Position))),] 
- Sort position column in each chromosome file as descending
  * tChr1descend <- tChr1[order(as.numeric(as.character(tChr1$Position)) , decreasing = TRUE),]
  * tChr2descend <- tChr2[order(as.numeric(as.character(tChr2$Position)) , decreasing = TRUE),]
  * tChr3descend <- tChr3[order(as.numeric(as.character(tChr3$Position)) , decreasing = TRUE),]
  * tChr4descend <- tChr4[order(as.numeric(as.character(tChr4$Position)) , decreasing = TRUE),] 
  * tChr5descend <- tChr5[order(as.numeric(as.character(tChr5$Position)) , decreasing = TRUE),]
  * tChr6descend <- tChr6[order(as.numeric(as.character(tChr6$Position)) , decreasing = TRUE),]
  * tChr7descend <- tChr7[order(as.numeric(as.character(tChr7$Position)) , decreasing = TRUE),] 
  * tChr8descend <- tChr8[order(as.numeric(as.character(tChr8$Position)) , decreasing = TRUE),] 
  * tChr9descend <- tChr9[order(as.numeric(as.character(tChr9$Position)) , decreasing = TRUE),]
  * tChr10descend <- tChr10[order(as.numeric(as.character(tChr10$Position)) , decreasing = TRUE),] 
## Data Analysis 