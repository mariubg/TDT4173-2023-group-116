# Features

### absolute_humidity_2m:gm3

Humidity readily affects the efficiency of the solar cells and creates a minimal layer of water on its surface. It also decreases the efficiency by 10-20% of the total power output produced.

However, the scatterplot doesn't really show this. Corr = 0.23

### air_density_2m:kgm3

Data analysis spells that solar illuminance/intensity, output current and voltage rise with increase in air pressure. Yet we see a corr = -0.28. Scatterplot shows that air densities over 1.3 rarely produces high energy

### ceiling_height_agl:m

Height of the ceiling. Recent studies show that solar energy is more efficient at high altitude than at sea level. This confirms that higher altitudes have more direct radiation and less diffuse radiation. As a result, full solar radiation is available at higher elevations, creating a more efficient PV system than ground-mounted PV systems.
Scatterplot doesn't really show a lot, other than that the height of the ceilings vary a lot, and a lot are 0. Might not make sense and be error in the data, which means we might want to not use this. After all, a ceiling rarely grows/shrinks from day to day. Corr = 0.083

22k values were NA - replaces by 0. We shouldn't use this.

### clear_sky_energy_1h:J

Clear sky energy of the previous hour. Scatterplot shows a clear connection, where high clear_sky_energy is needed for high pv_measurement, although it can still be low due to other factors. Corr = 0.8 

### clear_sky_rad:W

Sortof measures how clear the skies are. Scatterplot and corr are almost identical to clear_sky_energy. One of these should be a feature, but we probably don't need both.

### cloud_base_agl:m

The cloud base gives the lowest altitude of the visible portion of a cloud. A lot of 0 values? NA values replaced by 0. Should not be used. Corr and scatterplot show that it isnt that useful anyways.

### dew_or_rime:idx

0: neither dew nor rime, 1: dew, -1: rime. High energy only when neither dew or rime are present. Corr is low, but that is because dew and rime limits the energy the same way - but there is a clear connection. Should be very usable, but might not be fit for decision trees, if they only have 1 split.

### dew_point_2m:K

 Gives the instantaneous value of the dew point temperature at the indicated level. Corr = 0.25, higher dew point -> higher energy. Not that strong of a connection

### diffuse_rad:W 

Gives the instantaneous flux of diffuse radiation in Watts per square meter. Scatterplot shows that a certain level here is needed for certain levels of pv - might be useful. Corr = 0.71

### diffuse_rad_1h:J 

Almost identical to the one above, but with more variation. We don't need both, I think the other one is preferred

### direct_rad:W

Gives the instantaneous flux of direct radiation in Watts per square meter. Low rad can make any pv, but high is ofthen high pv, with exceptions of 0. Corr = 0.86

### direct_rad_1h:J

Basicly same as over.

### effective_cloud_cover:p 

Almost no pattern? Corr = -0.22

### elevation:m 

Elevation over sea level. Only one value - 6. So useless

### fresh_snow_12h:cm
### fresh_snow_1h:cm
### fresh_snow_24h:cm 
### fresh_snow_3h:cm
### fresh_snow_6h:cm

Fresh snow at different times. Low Corr. No snow needed for any pv if we choose lower time value. When we increase it, we get more variety. 24h shows a new spike at ca 7h. Might have something to do with cleaning intervals.

### is_day:idx

Corr = 0.55. Day is needed for high energy

### is_in_shadow:idx

Opposite of is_day. We won't need both of these.

### msl_pressure:hPa

Gives the pressure adjusted to sea level. To adjust the pressure to the mean sea level atmospheric conditions such as temperature are taken into account.
This parameter is also known as QFF. Corr = 0.18. 

### precip_5min:mm 
### precip_type_5min:idx

Inversely proportional

### pressure_100m:hPa
### pressure_50m:hPa

Higher pressure -> more energy, 0.18

### prob_rime:p

0 prob of water is neccessary for energy measure. As long as p(r) > 0, there is almost nor energy

### rain_water:kgm2

Inversely exponential, -0.086

### relative_humidity_1000hPa:p

No visible pattern in scatterplot, but -0.41 corr. Might want to investigate further

### sfc_pressure:hPa

Gives the surface pressure also known as QFE. 0.17. Low pressure leads to low energy

### snow_density:kgm3

0 snow is needed for high energy

### snow_depth:cm

0 is needed for high energy. Very similar to the one above

### snow_drift:idx

The snow drift parameter describes how strong snow is carried over the surface due to environmental factors such as wind speed. The index ranges from 0 to 6 with higher values indicating a higher amount of fresh snow being transported because of high wind speeds. All values are 0. Don not use

### snow_melt_10min:mm

 Following parameter returns the snow height that melted within the given interval, i.e. the difference in snow height in cm. Any value over 0 almost always leads to energy of 0 

### snow_water:kgm2

Close to 0 needed for energy, but its linear

### sun_azimuth:d

The solar azimuth angle defines the sun's relative direction along the local horizon. A bell pattern similar to hour. Very usable

### sun_elevation:d

The solar elevation angle (angle between the sun and the horizon) gives the position of the sun above the horizon. Corr 0.7. Like a half bell, but 0 for the night. Very usable

### super_cooled_liquid_water:kgm2

Supercooled liquid water refers to water droplets that remain liquid below their normal freezing point. While this parameter describes the vertically integrated supercooled liquid water content, our API also offers bottom/top altitudes (in meters) where supercooled liquid water is present. If no supercooled liquid water is present, bottom/top altitudes are not defined. -0.13. High pv at low values. Linear falloff

### t_1000hPa:K

Temperature. 0.35. Below 0 C very low pv, then a quick rise.

### total_cloud_cover:p

No visible pattern, -0.18

### visibility:m
### wind_speed_10m:ms
### wind_speed_u_10m:ms
### wind_speed_v_10m:ms
### wind_speed_w_1000hPa:ms

None of these looked promising


Features that appear relevant:
- clear_sky_energy_1h:J
- dew_or_rime:idx
- diffuse_rad:W 
- direct_rad:W
- is_day:idx
- precip_5min:mm 
- precip_type_5min:idx
- prob_rime:p
- relative_humidity_1000hPa:p
- snow_density:kgm3
- snow_water:kgm2
- sun_elevation:d
- super_cooled_liquid_water:kgm2
- t_1000hPa:K