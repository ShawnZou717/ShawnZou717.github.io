---
layout: post
title: BUGS While Running WW3 Model Quick Start
date: 2023-09-22 14:00:00+0800
description: a review of Coriolis force
tags: ww3
categories: physical-oceanography
giscus_comments: true
related_posts: false
toc:
  sidebar: left
---

## WW3 Quick Start

WW3 can be the most widely used wave model in meteorological prediction and reanalysis. This model directly comes from the very frontier research's keyboard. Focusing more on research function rather than commercial operation, thus it is totally user unfriendly, even if you run the very first quick start demo given in the munual, errors could occur quite frequent. Here I am recording 2 bugs I have met.

As the manual states, there are only 2 steps before you can compile and run ww3 model.

```bash
# set up compiler and forecast mode
model/bin/w3_setup model -c gnu -s NCEP_st4

# download data via ftp
model/bin/ww3_from_ftp.sh
```

Now, you can start compiling.

```bash
model/bin/w3_make
```

I saw 2 bugs before I complete compilation. Here I descripe what is the feature and solution of each error.

## 