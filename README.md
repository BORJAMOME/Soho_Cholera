# The Cholera Map That Transformed the World: John Snow's Data Journalism 💀
Visualization in R of the cholera outbreak in the London neighborhood of Soho by John Snow.

# Precedents
The cholera outbreak on Broad Street, London, in 1854, was studied by John Snow, who used data mapping to track cases. Snow found that most cases were clustered around a water pump on Broad Street. This analysis revealed a clear pattern of cholera spread related to water quality. His discovery was crucial for understanding infectious diseases and led to improvements in public health. This innovative approach laid the groundwork for future epidemiological research and reforms in sanitation and water supply systems. Snow transformed the way infectious diseases were addressed, emphasizing the importance of data mapping in epidemiological investigation.

![](Snow-cholera-map.jpg)



## Figures

``` r

#libraries
library(leaflet)
library(isdas)
```
``` r
# Load data for deaths and water pumps
data("snow_deaths")
data("snow_pumps")
```
``` r
# Define custom icon for "Deaths"
death_icon <- makeIcon(
  iconUrl = "https://emojicdn.elk.sh/💀",
  iconWidth = 15, iconHeight = 15
)
# Definir el icono personalizado para "Pumps"
pump_icon <- makeIcon(
  iconUrl = "https://emojicdn.elk.sh/🚰",
  iconWidth = 20, iconHeight = 20
)
```
``` r
# Create interactive map
snow_map <- leaflet() |>
  # Set map view
  setView(lng = -0.136, lat = 51.513, zoom = 16) |>
  # Change the map color to gray
  addProviderTiles("CartoDB.Positron") |>
  # Add markers for deaths with custom icon
  addMarkers(data = snow_deaths, ~long, ~lat,
             icon = death_icon,
             group = "Deaths" ) |>
  # Add markers for pumps with custom icon
  addMarkers(data = snow_pumps, ~long, ~lat,
             icon = pump_icon,
             group = "Pumps" ) |>
  # Add layer control to toggle between deaths and water pumps
  addLayersControl(overlayGroups = c("Deaths", "Pumps"),
                   options = layersControlOptions(collapsed = FALSE))
```
``` r
  # Show interactive map
  snow_map
```
