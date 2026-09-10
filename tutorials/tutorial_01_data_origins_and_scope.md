# Tutorial 1: Data Origins and the Scope of Research Questions

## Overview

Every dataset comes from somewhere: a sensor, a survey, a scraped webpage, a
cash register. Where data comes from - and *how* it was collected - determines
what questions it can honestly answer. In this 45-minute activity you will
rotate through four short "data stations." At each station you will copy and
paste ready-made R code into RStudio, run it, look at the output, and then act
as a **data detective**: figure out the data's origin and decide which
research questions are *in scope* (answerable from this data alone) and which
are *out of scope* (tempting to ask, but not something this data can support).

![--- --- --- --- --- --- --- --- ---](../graphics/div_bar.png)

## What You Will Learn

By the end of this activity, you will be able to:

1. **Trace a dataset's origin** - who or what collected it, how, when, and why
2. **Identify sampling method and bias** - voluntary response, convenience sample, complete census, sensor log, etc.
3. **Distinguish in-scope from out-of-scope questions** - recognize when a question requires data the dataset does not contain
4. **Run and read basic R/tidyverse code** - `read_csv()`, `summary()`, `group_by()`/`summarize()`, and `ggplot2`
5. **Justify your reasoning in writing** - explain *why* a question is or is not answerable, not just guess

**Note:** You do not need to finish every reflection question during class.
Anything unfinished should be completed as homework and submitted before the
deadline in the main [README](../README.md).

6. **New commands** - While we are using new commands in R that you have perhaps never seen before, we will be covering many of them in the near future. Stay tuned for more!
 
![--- --- --- --- --- --- --- --- ---](../graphics/div_bar.png)

## Before You Start

Open RStudio and make sure the `tidyverse` package is installed:

```r
install.packages("tidyverse")
```

You only need to do this once. For each station below, open the matching `.R`
file in `src/`, copy the code shown under each `TODO`, and paste it in place
of that `TODO` comment. Run each line with `Ctrl+Enter` (Windows/Linux) or
`Cmd+Return` (macOS).

![--- --- --- --- --- --- --- --- ---](../graphics/div_bar.png)

## Station 1: Weather Sensor Data

**File:** `src/station_01_weather_sensor/explore_weather.R`
**Data:** `data/weather_station.csv`

### Backstory

A single automated weather station (`WX-042`) mounted on a campus rooftop
records temperature, humidity, and wind speed every hour. It has no human
operator - it logs continuously, all day, every day, at one fixed location.

### Step 1: Load the tidyverse library

Replace `# TODO: Load the tidyverse library` with:

```r
library(tidyverse)
```

### Step 2: Read in the data

Replace `# TODO: Read in data/weather_station.csv` with:

```r
weather <- read_csv("data/weather_station.csv")
```

### Step 3: Preview the data

Replace `# TODO: Preview the structure and first few rows of the data` with:

```r
str(weather)
head(weather)
```

### Step 4: Summarize temperature and humidity

Replace `# TODO: Summarize temperature and humidity across the day` with:

```r
weather %>%
  summarize(
    avg_temp = mean(temp_f),
    min_temp = min(temp_f),
    max_temp = max(temp_f),
    avg_humidity = mean(humidity_pct)
  )
```

### Step 5: Plot temperature over time

Replace `# TODO: Plot temperature over time` with:

```r
ggplot(weather, aes(x = timestamp, y = temp_f, group = 1)) +
  geom_line(color = "steelblue") +
  labs(title = "Hourly Temperature at Station WX-042",
       x = "Time", y = "Temperature (F)")
```

### Detective Questions (record your answers in `writing/reflection.md`)

- **Origin:** Who/what collected this data, how often, and from where?
- **Scope:** Name one question this data *can* answer, and one question about
  weather that this data *cannot* answer (for example, anything about a
  different location, a different day, or seasons/months not recorded).

![--- --- --- --- --- --- --- --- ---](../graphics/div_bar.png)

## Station 2: Social Media Posts

**File:** `src/station_02_social_media/explore_social_media.R`
**Data:** `data/social_media_posts.csv`

### Backstory

These are posts collected by searching for the hashtag `#campuseats` over
one week. Only people who chose to post publicly, and who happened to use
that specific hashtag, are included. Usernames have been hashed for privacy.

### Step 1: Load the tidyverse library

Replace `# TODO: Load the tidyverse library` with:

```r
library(tidyverse)
```

### Step 2: Read in the data

Replace `# TODO: Read in data/social_media_posts.csv` with:

```r
posts <- read_csv("data/social_media_posts.csv")
```

### Step 3: Preview the data

Replace `# TODO: Preview the structure and first few rows of the data` with:

```r
str(posts)
head(posts)
```

### Step 4: Count posts by platform

Replace `# TODO: Count posts by platform` with:

```r
posts %>%
  count(platform, sort = TRUE)
```

### Step 5: Plot likes per post

Replace `# TODO: Plot likes per post, ordered from highest to lowest` with:

```r
posts %>%
  mutate(post_id = fct_reorder(post_id, likes)) %>%
  ggplot(aes(x = post_id, y = likes)) +
  geom_col(fill = "darkorange") +
  coord_flip() +
  labs(title = "Likes per Post (#campuseats)", x = "Post", y = "Likes")
```

### Detective Questions

- **Origin:** Who decided which posts appear in this dataset? Is every
  student's opinion represented, or only people who post publicly with this
  hashtag?
- **Scope:** Name one question this data *can* answer, and one question
  (for example, "what percentage of all students like the dining hall food?")
  that this data *cannot* answer, and explain why.

![--- --- --- --- --- --- --- --- ---](../graphics/div_bar.png)

## Station 3: Course Survey

**File:** `src/station_03_course_survey/explore_survey.R`
**Data:** `data/course_survey.csv`

### Backstory

At the end of the Fall 2025 semester, one section of CMPSC301 (35 students
enrolled) was emailed a voluntary, anonymous survey about study habits and
course enjoyment. 20 of 35 students responded (57% response rate).

### Step 1: Load the tidyverse library

Replace `# TODO: Load the tidyverse library` with:

```r
library(tidyverse)
```

### Step 2: Read in the data

Replace `# TODO: Read in data/course_survey.csv` with:

```r
survey <- read_csv("data/course_survey.csv")
```

### Step 3: Preview the data

Replace `# TODO: Preview the structure and first few rows of the data` with:

```r
str(survey)
head(survey)
```

### Step 4: Compare quiz averages by enjoyment

Replace `# TODO: Compare average quiz score for students who enjoy the course vs. those who do not` with:

```r
survey %>%
  group_by(enjoys_course) %>%
  summarize(avg_quiz = mean(quiz_avg), n = n())
```

### Step 5: Plot hours studied vs. quiz average

Replace `# TODO: Plot hours studied vs. quiz average` with:

```r
ggplot(survey, aes(x = hours_studied_per_week, y = quiz_avg, color = enjoys_course)) +
  geom_point(size = 3) +
  labs(title = "Study Hours vs. Quiz Average",
       x = "Hours Studied per Week", y = "Quiz Average")
```

### Detective Questions

- **Origin:** Was this survey mandatory or voluntary? What is the response
  rate, and which students might be missing from the 15 who did not respond?
- **Scope:** Name one question this data *can* answer, and one question
  (for example, "do CMPSC301 students at other universities study the same
  way?") that this data *cannot* answer, and explain why.

![--- --- --- --- --- --- --- --- ---](../graphics/div_bar.png)

## Station 4: Retail Sales Transactions

**File:** `src/station_04_retail_sales/explore_retail_sales.R`
**Data:** `data/retail_sales.csv`

### Backstory

Two campus bookstore locations (`BOOKSTORE-A` and `BOOKSTORE-B`) automatically
log every in-person, point-of-sale transaction. This is a complete record of
those registers - not a sample - but it says nothing about online orders or
other stores.

### Step 1: Load the tidyverse library

Replace `# TODO: Load the tidyverse library` with:

```r
library(tidyverse)
```

### Step 2: Read in the data

Replace `# TODO: Read in data/retail_sales.csv` with:

```r
sales <- read_csv("data/retail_sales.csv")
```

### Step 3: Preview the data

Replace `# TODO: Preview the structure and first few rows of the data` with:

```r
str(sales)
head(sales)
```

### Step 4: Total sales by product category

Replace `# TODO: Total sales amount by product category` with:

```r
sales %>%
  group_by(product_category) %>%
  summarize(total_sales = sum(amount_usd)) %>%
  arrange(desc(total_sales))
```

### Step 5: Plot total sales by store

Replace `# TODO: Plot total sales amount by store` with:

```r
sales %>%
  group_by(store_id) %>%
  summarize(total_sales = sum(amount_usd)) %>%
  ggplot(aes(x = store_id, y = total_sales, fill = store_id)) +
  geom_col() +
  labs(title = "Total Sales by Store", x = "Store", y = "Total Sales (USD)")
```

### Detective Questions

- **Origin:** Is this a sample or a complete record? What is it a complete
  record *of*, and what is it silent about (online sales, other campuses,
  other weeks/seasons)?
- **Scope:** Name one question this data *can* answer, and one question
  (for example, "are online textbook sales rising or falling?") that this
  data *cannot* answer, and explain why.

![--- --- --- --- --- --- --- --- ---](../graphics/div_bar.png)

## Wrap-Up

Finish the **General Reflection** section of `writing/reflection.md`,
comparing the four data origins and explaining, in your own words, why
knowing a dataset's origin matters before trusting any conclusion drawn from
it.
