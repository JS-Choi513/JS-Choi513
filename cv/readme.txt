#source generation code

datadrivencv::use_datadriven_cv(
full_name = "Jinseo Choi",
data_location = "https://docs.google.com/spreadsheets/d/1BgEhba9RKnFdXUhA9kO0mHzAWHpyJ-NyCe3JHupbOHU",
pdf_location = "https://github.com/JS-Choi513/JS-Choi513/tree/main/cv/cv.pdf",
source_location = "https://github.com/JS-Choi513/JS-Choi513/tree/main/cv/cv.html"
)

# This script builds both the HTML and PDF versions of your CV

# If you wanted to speed up rendering for googlesheets driven CVs you could use
# this script to cache a version of the CV_Printer class with data already
# loaded and load the cached version in the .Rmd instead of re-fetching it twice
# for the HTML and PDF rendering. This exercise is left to the reader.

# Knit the HTML version
rmarkdown::render("cv.rmd",
                  params = list(pdf_mode = FALSE),
                  output_file = "cv.html")

# Knit the PDF version to temporary html location
tmp_html_cv_loc <- fs::file_temp(ext = ".html")
rmarkdown::render("cv.rmd",
                  params = list(pdf_mode = TRUE),
                  output_file = tmp_html_cv_loc)

# Convert to PDF using Pagedown
pagedown::chrome_print(input = tmp_html_cv_loc,
                       output = "cv.pdf")
