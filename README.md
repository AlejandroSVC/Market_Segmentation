# MULTIPLE CORRESPONDENCE ANALYSIS WITH R

# Set working directory and load the data
setwd("directory")
data <- read.table("data.txt", header = TRUE) 

# Assign short labels to the categories of the variables

data$p3 <- factor(data$p3,  levels = c(1,2,3,4),
labels = c("BM","BR","BP","BN"))

data$p4 <- factor(data$p4,  levels = c(1,2,3,4),
labels = c("VAM","VAR","VAP","VAN"))

data$tenencia <- factor(data$tenencia,  levels = c(1,2,3,4),
labels = c("VP","VA","VC","VI"))

data$allega_int <- factor(data$allega_int,  levels = c(1,2),
labels = c("AN","AS"))

data$hh_d_habitab <- factor(data$hh_d_habitab,  levels = c(1,2),
labels = c("CHN","CHS"))

data$pobreza5d <- factor(data$pobreza5d,  levels = c(1,2),
labels = c("NPB","PB"))

# ANALYSIS

# All the variables in the dataset will be included

# Load the libraries

library(FactoMineR)
library(ggplot2)

# install.packages("devtools")

library("devtools")
install_github("kassambara/factoextra")

# Load factoextra

library("factoextra")

# Fit the MCA model to the data

res.mca <- MCA(data, graph=FALSE)

# Plot the MCA results

fviz_mca_var(res.mca, repel = TRUE, col.var = "contrib",
  gradient.cols = c("#00AFBB", "#E7B800", "#FC4E07"))

![AMC plot](docs/assets/images/ACM_Casen_2022_RM_JHogar.png)

The plot shows two groups of categories associated to “POBRE” and “NO POBRE”

PB	:	Pobre
BR	:	En el entorno o barrio se observa cierta cantidad de basura
CHS	:	La vivienda presenta carencias en habitabilidad
VAR	:	En el entorno o barrio existe cierto nivel de vandalismo

NPB	:	No pobre
VAN	:	En el entorno o barrio no existe vandalismo
VP	:	vivienda propia
CHN	:	La vivienda no presenta carencias en habitabilidad
VC	:	Tenencia de vivienda: cedida
VA	:	Tenencia de vivienda: arrendada

# Visualize variable categorie contributions on axes 1

fviz_contrib(res.mca, choice ="var", axes = 1)

![Contributions](docs/assets/images/ACM_Variable_categories_contributions_on_axes_1.png)

