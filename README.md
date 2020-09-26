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
