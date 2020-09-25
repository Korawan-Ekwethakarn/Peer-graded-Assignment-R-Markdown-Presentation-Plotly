# Peer-graded-Assignment-R-Markdown-Presentation-Plotly
Create a web page presentation using R Markdown
library(plotly)
plain_x <- c(1:50)
plain_y <- rnorm(50, mean = 0)
data <- data.frame(plain_x, plain_y )
p <- plot_ly(data, x = ~plain_x, y = ~plain_y , type = 'scatter', mode = 'lines')
p
10
20
30
40
50
