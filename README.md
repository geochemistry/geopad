# geopad

    ggords
        Installation
        Example Usage
        ggpca
        ggpnmds
        License

ggords

The package provides six functions: ggpca(), ggca(), ggpcoa(), ggnmds(), ggrda(), ggcca(). You can customize the display labels and themes. Labels can contain formulas. Image themes can be set by themes in ggplots or by other packages(ggthemr).
Installation

library(devtools)
install_github("wdy91617/ggords")

Example Usage

library(ggords)
require(vegan)
#> Loading required package: vegan
#> Loading required package: permute
#> Loading required package: lattice
#> This is vegan 2.4-4
require(ggplot2)
#> Loading required package: ggplot2
data(Envs)

ggpca
1. get group factor

Env.w <- hclust(dist(scale(Envs)), "ward.D")
gr <- cutree(Env.w , k=4)
grl <- factor(gr)

2. Compute PCA

Env.pca <- rda(Envs,scale = TRUE)
#head(summary(Env.pca))

3. Produce a plot

ggpca(Env.pca)

4. Add a group

ggpca(Env.pca, group = grl) 

5. Set a theme

ggpca(Env.pca, group = grl, spacol = "white") + theme_dark()

6. Set a theme (use ggthemr packages, more themes in ggthemer)

library(ggthemr)

chalk_theme <- ggthemr('chalk', set_theme = FALSE)
fd_theme <- ggthemr('flat dark', set_theme = FALSE)

p <- ggpca(Env.pca, group = grl, spacol = "white")
p + chalk_theme$theme

p + fd_theme$theme

7. Remove the arrow

ggpca(Env.pca, group = grl, spearrow = NULL)

8. Modify legend title, group color and point shape

ggpca(Env.pca, group = grl, spearrow = NULL) + 
  scale_color_manual(name = "Groups",values = c("red2", "purple1", "grey20","cyan")) +
  scale_shape_manual(name = "Groups",values = c(8,15,16,17))

9. Add confidence ellipses

ggpca(Env.pca, group = grl, spearrow = NULL, ellipse = TRUE) +
  scale_colour_hue(l = 70, c = 300)

ggpnmds
1. Compute NMDS

Env.nmds <- metaMDS(Envs, distance="bray")
#> Square root transformation
#> Wisconsin double standardization
#> Run 0 stress 0.04321381 
#> Run 1 stress 0.04321545 
#> ... Procrustes: rmse 0.000332486  max resid 0.001544699 
#> ... Similar to previous best
#> Run 2 stress 0.04321384 
#> ... Procrustes: rmse 0.0005743842  max resid 0.002679384 
#> ... Similar to previous best
#> Run 3 stress 0.06230603 
#> Run 4 stress 0.04321479 
#> ... Procrustes: rmse 0.00074061  max resid 0.003457211 
#> ... Similar to previous best
#> Run 5 stress 0.07681417 
#> Run 6 stress 0.0623054 
#> Run 7 stress 0.06972094 
#> Run 8 stress 0.0432159 
#> ... Procrustes: rmse 0.0004013882  max resid 0.001869575 
#> ... Similar to previous best
#> Run 9 stress 0.04321421 
#> ... Procrustes: rmse 0.0001015489  max resid 0.0004638241 
#> ... Similar to previous best
#> Run 10 stress 0.04321421 
#> ... Procrustes: rmse 0.000647809  max resid 0.003023385 
#> ... Similar to previous best
#> Run 11 stress 0.04321383 
#> ... Procrustes: rmse 5.693312e-05  max resid 0.0001668148 
#> ... Similar to previous best
#> Run 12 stress 0.04321469 
#> ... Procrustes: rmse 0.0007662745  max resid 0.003576096 
#> ... Similar to previous best
#> Run 13 stress 0.04321539 
#> ... Procrustes: rmse 0.0003309146  max resid 0.001540436 
#> ... Similar to previous best
#> Run 14 stress 0.06230623 
#> Run 15 stress 0.04321394 
#> ... Procrustes: rmse 0.0005394657  max resid 0.002445097 
#> ... Similar to previous best
#> Run 16 stress 0.04321387 
#> ... Procrustes: rmse 3.773925e-05  max resid 0.0001624311 
#> ... Similar to previous best
#> Run 17 stress 0.04321547 
#> ... Procrustes: rmse 0.0003366437  max resid 0.001564668 
#> ... Similar to previous best
#> Run 18 stress 0.07548226 
#> Run 19 stress 0.07779553 
#> Run 20 stress 0.2242599 
#> *** Solution reached
#head(summary(Env.nmds))

2. Produce a plot

ggnmds(Env.nmds)

3. Add a group

ggnmds(Env.nmds, group = grl) 

4. Set a theme

ggnmds(Env.nmds, group = grl, spacol = "white") + theme_dark()

5. Set a theme (use ggthemr packages, more themes in ggthemer)

library(ggthemr)

chalk_theme <- ggthemr('chalk', set_theme = FALSE)
fd_theme <- ggthemr('flat dark', set_theme = FALSE)

p <- ggnmds(Env.nmds, group = grl, spacol = "white")
p + chalk_theme$theme

p + fd_theme$theme

6. Remove the arrow

ggnmds(Env.nmds, group = grl, spearrow = NULL)

7. Set labels

mlabs<-c("NH[4]^{`+`}" , "NO[3]^{`-`}" ,"delta^13*C","A[1]","sqrt(2*pi)","frac(x^2,2)",
         "sin(x)","hat(x)","bar(xy)","90*degree","x^{y+z}")

ggnmds(Env.nmds, group = grl, spearrow = NULL, msplabs = mlabs)

8. Modify legend title, group color and point shape

ggnmds(Env.nmds, group = grl, spearrow = NULL) + 
  scale_color_manual(name = "Groups",values = c("red2", "purple1", "grey20","cyan")) +
  scale_shape_manual(name = "Groups",values = c(8,15,16,17))

9. Add confidence ellipses

ggnmds(Env.nmds, group = grl, spearrow = NULL, ellipse = TRUE) +
  scale_colour_hue(l = 70, c = 300)

License

Released under GPL-3.
