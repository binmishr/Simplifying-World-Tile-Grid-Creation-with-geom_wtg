# Simplifying-World-Tile-Grid-Creation-with-geom_wtg

The details of the codeset and plots are included in the attached Microsoft Word Document (.docx) file in this repository. 
You need to view the file in "Read Mode" to see the contents properly after downloading the same.

The concerned R package worldtilegrid is attached as .ZIP file with this repository.

WorldTileGrid Package - A Brief Introduction
=============================================

A “tile grid map” is a cartogram that uses same-sized tiles in approximate, relative positions of each other to represent a world map.The world tile grid relative position reference system used by this ‘ggplot2’ ‘Geom/Stat’ was the original work of ‘Jon Schwabish’ and converted to ‘CSV’ by ‘Maarten Lambrechts’.

Ref: https://policyviz.com/2017/10/12/the-world-tile-grid-map/
Ref:http://www.maartenlambrechts.com/2017/10/22/tutorial-a-worldtilegrid-with-ggplot2.html

What’s Inside The Tin
The following functions are implemented:

geom_wtg / stat_wtg: World Tile Grid Geom/Stat

theme_enhance_wtg World tile grid theme cruft remover that can be used with any other theme

The following data is included/exported:
wtg: World Tile Grid Basemap Data

Installation
=============
    Library("worldtilegrid")

Usage
======
    library(worldtilegrid)
    library(tidyverse)

# current verison
    packageVersion("worldtilegrid")

## [1] '0.1.0'

Example (All countries are in the data set)

        set.seed(1)
        data_frame(
          ctry = worldtilegrid::wtg$alpha.3,
          `Thing Val` = sample(1000, length(ctry))
        ) -> xdf

        ggplot(xdf, aes(country = ctry, fill = `Thing Val`)) +
          geom_wtg() +
          geom_text(aes(label = stat(alpha.2)), stat="wtg", size=2) + # re-compute the stat to label
          coord_equal() +
          viridis::scale_fill_viridis() +
          labs(title = "World Tile Grid") +
          hrbrthemes::theme_ft_rc() +
          theme_enhance_wtg()

![image](https://user-images.githubusercontent.com/26252963/149613799-2e9582c7-0f12-408b-98ec-9e56c65d1e73.png)

Example (Only a few countries are in the data set)

    set.seed(1)
    data_frame(
      ctry = worldtilegrid::wtg$alpha.3[1:30],
      `Thing Val` = sample(1000, length(ctry))
    ) -> xdf

    ggplot(xdf, aes(country = ctry, fill = `Thing Val`)) +
      geom_wtg() +
      geom_text(aes(label = stat(alpha.2)), stat="wtg", size=2) + # re-compute the stat to label
      coord_equal() +
      viridis::scale_fill_viridis() +
      labs(title = "World Tile Grid") +
      hrbrthemes::theme_ft_rc() +
      theme_enhance_wtg()

![image](https://user-images.githubusercontent.com/26252963/149613822-14a10a61-af4c-4f94-b2e7-957f8bc00295.png)


Facet Example (All countries are in the data set)

    set.seed(1)
    data_frame(
      ctry = worldtilegrid::wtg$alpha.3,
      `Thing Val` = sample(1000, length(ctry)),
      grp = 'Thing One'
    ) -> xdf1

    data_frame(
      ctry = worldtilegrid::wtg$alpha.3,
      `Thing Val` = sample(1000, length(ctry)),
      grp = 'Thing Two'
    ) -> xdf2

    bind_rows(
      xdf1,
      xdf2
    ) -> xdf

    ggplot(xdf, aes(country = ctry, fill = `Thing Val`)) +
      geom_wtg() +
      coord_equal() +
      facet_wrap(~grp) +
      viridis::scale_fill_viridis() +
      labs(title = "World Tile Grid Facets") +
      hrbrthemes::theme_ft_rc() +
      theme_enhance_wtg()

![image](https://user-images.githubusercontent.com/26252963/149613848-aea057e3-7951-402b-bff2-ea38fa11c412.png)


Facet Example (Only a few countries are in the data set)
The geom will fill in the gaps for you:

    set.seed(1)
    data_frame(
      ctry = c("USA", "MEX", "CAN", "RUS", "BRA"),
      `Thing Val` = sample(1000, length(ctry)),
      grp = 'Thing One'
    ) -> xdf1

    data_frame(
      ctry = c("USA", "MEX", "CAN", "RUS", "BRA"),
      `Thing Val` = sample(1000, length(ctry)),
      grp = 'Thing Two'
    ) -> xdf2

    bind_rows(
      xdf1,
      xdf2
    ) -> xdf

    ggplot(xdf, aes(country = ctry, fill = `Thing Val`)) +
      geom_wtg() +
      coord_equal() +
      facet_wrap(~grp) +
      viridis::scale_fill_viridis(na.value = hrbrthemes::ft_cols$gray) +
      labs(title = "World Tile Grid Facets") +
      hrbrthemes::theme_ft_rc() +
      theme_enhance_wtg()
![image](https://user-images.githubusercontent.com/26252963/149613863-73695f89-9707-46d6-9157-488f8ca5eb84.png)




