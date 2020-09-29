# Peer-graded-Assignment-R-Markdown-Presentation-Plotly
plot.ly (link)
• platform share and edit plots modularly on the web (examples)
– every part of the plot can be customized and modified
– graphs can be converted from one language to another
• you can choose to log in through Facebook/Twitter/Google/GitHub
1. make sure you have devtools installed in R
2. enter devtools::install_github("ropensci/plotly"), which installs plotly package from
GitHub
3. go to https://plot.ly/r/getting-started/ and follow the instructions
4. enter library(plotly); set_credentials_file("<username>", "<token>") with the appropriate username and token filled in
5. use plotly() methods to upload plots to your account
6. modify any part of the plot as you like once uploaded
7. share the plot
Example
# load packages
library(plotly); library(ggplot2)
# make sure your plot.ly credentials are set correctly using the following command
# set_credentials_file(username=<FILL IN>, api_key=<FILL IN>)
# load data
load("courseraData.rda")
# bar plot using ggplot2
g <- ggplot(myData, aes(y = enrollment, x = class, fill = as.factor(offering)))
g <- g + geom_bar(stat = "identity")
g
Example
 .packages = c("ggplot2","plotly", "DT", "htmlwidgets")
.inst <- .packages %in% installed.packages()
if(length(.packages[!.inst]) > 0) install.packages(.packages[!.inst], repos = "http://cran.us.r-project.org")
notshow = lapply(.packages, require, character.only=TRUE)

###############
#### GRAPH ####
###############

#### 1. Pepare Data ####
datt=read.csv("/Users/chou/GoogleDrive/UMN2014-2017/Plan B/final/clean_dat.csv",header=TRUE)
levels(datt$PMD)=list(P="P",M="M",D="D")

#### 2. Generate ggplot ####
hist_PMD_a=ggplot(datt, aes(x=Area, color=PMD, fill=PMD))+
  geom_histogram(aes(y=..density..), alpha=0.5,
                 position="identity")+
  geom_density(alpha=.3)
box_PMD_a=ggplot(datt, aes(x=PMD, y=Area, fill=PMD)) +
  geom_boxplot(outlier.shape=NA, outlier.colour = NA) +
  geom_point(position = position_jitter(h=0,w=0.3))

#### 3. Convert to interactive plots using plotly ####
p1 = plotly_build(hist_PMD_a)
p2 = plotly_build(box_PMD_a)
p = subplot(p1,p2, margin=0.05)

#### 4. Convert to a HTML widget using htmlwidgets ####
path = paste("/Users/chou/GoogleDrive/Websites/github/myblog_hugo_temple/static/posts/2017-05-26-ioslides-vs-slidify-in-r-markdown-presentation_html", "/area.html", sep="")
saveWidget(as_widget(p), file = path)

###############
#### TABLE ####
###############

#### 1. Prepare Data ####
dat = datt[,-c(1,4,5)]
names(dat) = c("Sample ID", "# in image", "image No.",
               "image name", "location", "PMD", "SI",
               "Area", "Perimeter", "Circularity",
               "Aspect Ratio")

#### 2. Convert to interactive table using DT ####
d=datatable(dat)

#### 3. Convert to HTML widget using htmlwidgets ####
path <- paste("/Users/chou/GoogleDrive/Websites/github/myblog_hugo_temple/static/posts/2017-05-26-ioslides-vs-slidify-in-r-markdown-presentation_html", "/dat.html", sep="")
saveWidget(as_widget(d), file = path) 
