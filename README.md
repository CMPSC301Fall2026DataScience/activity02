# CMPSC301 Data Science

Activity 02: Data Origins and the Scope of Research Questions

## Assigned and Due

- **Assigned**: Thursday, 10th September 2026
- **Due and Expiration**: Monday, 14th September 2026 by class time.

Note: the expiration date is the last date you can submit your work for a grade.

<img src=graphics/dataOrigins_small.png alt="data_origins" style="display: block; margin: 0 auto;">

</center>

## Table of Contents
- [CMPSC301 Data Science](#cmpsc301-data-science)
  - [Assigned and Due](#assigned-and-due)
  - [Table of Contents](#table-of-contents)
  - [Overview](#overview)
  - [Learning Objectives](#learning-objectives)
  - [Activity Goals](#activity-goals)
  - [Instructions](#instructions)
    - [Setting Up R (Do This First!)](#setting-up-r-do-this-first)
    - [Working the Stations](#working-the-stations)
    - [Running the Scripts](#running-the-scripts)
  - [Deliverable](#deliverable)
  - [Submission](#submission)
  - [GatorGrade](#gatorgrade)
  - [Seeking Assistance](#seeking-assistance)
    - [Common Issues and Solutions](#common-issues-and-solutions)
  - [Additional Resources](#additional-resources)
  - [Learning Extensions (Optional)](#learning-extensions-optional)

## Overview

Every dataset comes from somewhere - a sensor, a survey, a scraped webpage, a
cash register - and where it comes from determines what questions it can
honestly answer. In this 45-minute, in-class activity you will rotate through
four short "data stations," each built around a different real-world data
origin: an automated weather sensor, a hashtag search on social media, a
voluntary course survey, and a complete retail transaction log.

At each station you will **copy and paste** ready-made R code into a script
file using RStudio where you can run it, to examine the output.

Then, acting as a **data detective**, you will decide what the data's origin
was and which research questions are *in scope* (answerable from the data alone)
versus *out of scope* (tempting to ask, but unsupported by this data).

By the end of this activity, you will be able to look at any dataset and ask,
before trusting a single conclusion from it: *where did this come from, and
what can it actually tell me?*

![--- --- --- --- --- --- --- --- ---](graphics/div_bar.png)

## Learning Objectives

By completing this activity, you will be able to:

1. **Trace a dataset's origin** - identify who or what collected it, how, when, and why
2. **Recognize sampling method and bias** - distinguish voluntary response, convenience samples, sensor logs, and complete records
3. **Distinguish in-scope from out-of-scope research questions** - explain why a question may not be answerable from a given dataset
4. **Read and run basic R/tidyverse code** - `read_csv()`, `summary()`/`str()`, `group_by()`/`summarize()`, and `ggplot2`
5. **Justify conclusions in writing** - support claims about a dataset's scope with specific reasoning, not guesses

![--- --- --- --- --- --- --- --- ---](graphics/div_bar.png)

## Activity Goals

This activity guides you through one combined tutorial covering four data stations:

- [Tutorial_01](tutorials/tutorial_01_data_origins_and_scope.md)
  - **Station 1: Weather Sensor Data** - an automated, single-location sensor log
  - **Station 2: Social Media Posts** - a hashtag search, a self-selected sample of public posts
  - **Station 3: Course Survey** - a voluntary, anonymous end-of-semester survey
  - **Station 4: Retail Sales Transactions** - a complete point-of-sale record for two stores

Each station pairs a short R script with detective questions you will answer
in `writing/reflection.md`.

![--- --- --- --- --- --- --- --- ---](graphics/div_bar.png)

## Instructions

### Setting Up R (Do This First!)

**IMPORTANT:** All four stations share the same package requirement. Set this
up once before starting:

Open RStudio and run:

```r
install.packages("tidyverse")
```

OR, if you want to first check that the library exists before you automatically install the library on your machine, use the following code. The below code will save you time in the long-run since you do not have to jump over the line that installs and reinstalls the `tidyverse` library when you execute your programs.

```r
# Load tidyverse, install if necessary
if (!require('tidyverse')) {
  install.packages('tidyverse')
  library('tidyverse')
}
```

Note: No other project setup (no `uv`, no virtual environment) is required for R.

### Working the Stations

1. **Read** the activity guide: [Tutorial_01: Data Origins and the Scope of Research Questions](tutorials/tutorial_01_data_origins_and_scope.md)
2. **Open** each station's `.R` file in `src/` and replace each `TODO` comment with the matching code block from the tutorial
3. **Run** each line in RStudio (`Ctrl+Enter` / `Cmd+Return`) and read the console output and plots
4. **Discuss** the backstory for that station with your group: who collected this data, and why?
5. **Answer** that station's detective questions in `writing/reflection.md` before moving to the next station
6. **Finish** the General Reflection section once all four stations are complete

### Running the Scripts

Each station's script can be run independently, for example:

```r
source("src/station_01_weather_sensor/explore_weather.R")
```

Or open the file directly in RStudio and run it line by line, which is
recommended so you can pause and read each result.

![--- --- --- --- --- --- --- --- ---](graphics/div_bar.png)

## Deliverable

You will submit:
- Completed R scripts with all `TODO` items resolved for each station:
  - `src/station_01_weather_sensor/explore_weather.R`
  - `src/station_02_social_media/explore_social_media.R`
  - `src/station_03_course_survey/explore_survey.R`
  - `src/station_04_retail_sales/explore_retail_sales.R`
- Completed `writing/reflection.md` with answers to all detective and reflection questions
- All data files remain in their respective `data/` folder

**Note:** You do NOT need to submit screenshots of your plots. We will verify
functionality by running your code.

## Submission

This is a check mark grade.

Please submit this assignment by pushing your work to your GitHub repository.
Ensure that:
- All TODO items have been replaced with working code
- All scripts run without errors
- The reflection document is complete
- Your name has been added to all source files

Use meaningful commit messages that describe what you accomplished:
```bash
git add .
git commit -m "Complete Station 1: Weather sensor origin and scope"
git push
```

![--- --- --- --- --- --- --- --- ---](graphics/div_bar.png)

## GatorGrade

You can check your work by running GatorGrade:

```bash
gatorgrade --config config/gatorgrade.yml
```

This will verify that:
- All required files exist
- TODO items have been removed
- Reflection questions have been answered

![--- --- --- --- --- --- --- --- ---](graphics/div_bar.png)

## Seeking Assistance

If you encounter difficulties:

First, try adding code at the beginning of each program to remove all left-over variables and plots from previous runs. This will ensure that you are performing a "clean run" of your programs with each run.

```R
# Clear environment and plots
rm(list = ls()) # clear all variables
graphics.off()  # clear all plots
cat("\014")    # clear the console

# Load tidyverse, install if necessary
if (!require('tidyverse')) {
  install.packages('tidyverse')
  library('tidyverse')
}
```

1. **Read the error messages carefully** - R and RStudio provide helpful error messages
2. **Check the tutorial document** - it contains the exact code to copy and paste
3. **Consult the tidyverse documentation** - https://www.tidyverse.org/
4. **Ask during class or office hours** - bring specific questions about what you've tried
5. **Work with classmates** - discuss the origin/scope reasoning together, but write your own answers

### Common Issues and Solutions

**Issue:** `could not find function` error
- **Solution:** Make sure you ran `library(tidyverse)` at the top of the script before using `read_csv()`, `%>%`, or `ggplot()`.

**Issue:** `cannot open file 'data/...'` error
- **Solution:** Make sure your RStudio working directory is the project root, not the `src/` subfolder. Use `getwd()` to check, and `setwd()` if needed.

**Issue:** Plot window doesn't show anything
- **Solution:** Run the `ggplot(...)` code as one full block (don't run just the first line), and check the Plots pane in RStudio.

**Issue:** Not sure what "scope" means for a dataset
- **Solution:** Re-read the backstory for that station in the tutorial - it describes exactly who collected the data and how.

![--- --- --- --- --- --- --- --- ---](graphics/div_bar.png)

## Additional Resources

- **tidyverse Documentation:** https://www.tidyverse.org/
- **ggplot2 Documentation:** https://ggplot2.tidyverse.org/
- **R for Data Science (free book):** https://r4ds.hadley.nz/
- **dplyr Cheat Sheet:** https://posit.co/resources/cheatsheets/

![--- --- --- --- --- --- --- --- ---](graphics/div_bar.png)

## Learning Extensions (Optional)

Looking for an extra challenge?! After completing the required stations,
challenge yourself:

1. **Find your own dataset** - locate a public dataset online and write its origin story
2. **Design a fifth station** - propose a new data origin (e.g., a lab experiment, a government census) and list in-scope/out-of-scope questions for it
3. **Investigate a real headline** - find a news article that cites data, and evaluate whether its conclusions match the data's actual scope
4. **Combine datasets** - discuss what new questions become answerable (or stay out of scope) if you joined two of the four station datasets together

![--- --- --- --- --- --- --- --- ---](graphics/div_bar.png)

**Remember:** The goal is not just to run the R code, but to build the habit
of asking "where did this data come from, and what can it actually tell me?"
before trusting any conclusion drawn from it.

Now, go get 'em!
