<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">

<h1>Atlantic Equatorial Mode Study</h1>




<b>Introduction</b><br><br>
---
The <b>Atlantic Equatorial Mode</b>, also known as <b>Atlantic Niño</b>, is a pattern of
climate variability characterized by positive Sea Surface Temperature (<b>SST</b>) anomalies
in the eastern equatorial Atlantic. Although it shares certain physical mechanisms with the
Pacific <b>El Niño–Southern Oscillation (ENSO)</b>, the Atlantic Niño presents
<b>lower intensity</b>, <b>shorter duration</b>, and a
<b>markedly seasonal and regional character</b>.
<br><br>

This study aims to <b>observationally characterize the Atlantic Niño</b> and
systematically compare it with the <b>Pacific Niño</b>, analyzing their differences in
temporal structure, spatial extent, and atmospheric impact. To do this, monthly variability,
the spatial distribution of <b>SST</b> and <b>precipitation</b> anomalies, and the
relationship between both fields are studied during the period <b>1960–2020</b>.
<br><br>

A central aspect of the work is the <b>robust definition of event identification
criteria</b>, paying special attention to the <b>characteristic seasonality</b> of the
Atlantic Niño and its <b>independence from ENSO</b>. Given that global warming
introduces a background trend in the SST series, an approach based on
<b>seasonal anomalies</b> is adopted, avoiding biases towards recent years and ensuring a
physically consistent interpretation of the detected episodes.
<br><br>

The analysis combines multiple observational and reanalysis datasets, allowing us to
evaluate the <b>robustness of the results</b> against methodological differences and ensure
that the identified patterns do not depend on a single product.

</div>

---

<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">

<b>Datasets</b><br><br>

For the analysis of Sea Surface Temperature (<b>SST</b>), two observational products
widely used in climate studies are employed:
<ul>
  <li><b>HadISST</b>, with a spatial resolution of <b>1° × 1°</b>.</li>
  <li><b>ERSST</b>, with a spatial resolution of <b>2° × 2°</b>.</li>
</ul>

For precipitation, two products with different natures (observational and
reanalysis) are used, which allows for evaluating the robustness of atmospheric signals:
<ul>
  <li><b>NOAA precipitation (PCP)</b>, with a spatial resolution of <b>2.5° × 2.5°</b>.</li>
  <li><b>NCEP–NCAR Reanalysis (precipitation)</b>, with a spatial resolution of
      <b>1.875° × 1.875°</b>.</li>
</ul>

The study period covers <b>1960–2020</b>, selected for the higher quality and
homogeneity of the observational records.

</div>





---

<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">

<b>Data setup (external files)</b><br><br>

The notebook expects the NetCDF datasets to be available locally, but the raw files are large
(~500&nbsp;MB, 200&nbsp;MB, 80&nbsp;MB, and 30&nbsp;MB), so they are intentionally kept
<b>outside</b> the repository to keep clones lightweight.<br><br>

To reproduce the analysis:
<ul>
  <li>Download the four datasets from their original sources (HadISST, ERSST, NOAA PCP, NCEP–NCAR).</li>
  <li>Store them in a local folder (for example: <code>/path/to/data/</code>).</li>
  <li>Update the <code>path</code> variable in <code>Notebook.ipynb</code> to point to your local folder.</li>
</ul>

This keeps the repository portable while still allowing full reproducibility once the data
are placed in a consistent location.


---

![SST_mean](img/1.png)

---
</div>


</div>
<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">

<b>Annual mean temperature and calculation methodology</b><br><br>
Two graphs corresponding to the annual mean temperature in the 
<b>Atlantic Niño (ATL3)</b> and <b>Pacific Niño (Niño 3.4)</b> regions are shown.
In both regions, a <b>clear positive trend</b> in temperature is observed throughout the study period.
Since this signal is associated with global warming, it is necessary to apply a 
<b>detrend</b> prior to calculating climate anomalies.
Furthermore, since the magnitude of the trend differs between regions, this detrend must be applied
<b>point-by-point</b> in each spatial grid cell.



The two analyzed datasets,
<span style="color:#ADD8E6;"><b>HadISST</b></span> and
<span style="color:#FFA500;"><b>ERSST</b></span>,
present results consistent with expectations.
ERSST systematically shows slightly higher values, although within a reasonable margin.
These differences are explained by the different observation systems, temporal frequency,
spatial resolution, and reconstruction methodologies employed in each product,
which introduces a small <i>offset</i> between both datasets.


Temperature values above <b>35&nbsp;°C</b> are discarded to avoid contamination by land points,
as well as values below <b>−1.79&nbsp;°C</b>.
This latter threshold is especially relevant in ERSST, where the region covered by ice in the Arctic
presents values close to −1.8&nbsp;°C that distort the mean and subsequent calculations.

For the calculation of the mean temperature in each region, the direct mean of the data matrix
was initially used.
However, this approximation is not strictly correct, as the area represented by each cell
depends on latitude. The physically correct way to calculate the spatial mean is to weight each cell
by the cosine of the latitude.
This weighting is necessary because the Earth is a sphere and the area of the cells decreases with latitude.
For low latitudes, such as those considered in this study, the error committed by not applying this correction
is very small (on the order of <b>0.5&nbsp;%</b>), so the approximation is acceptable.

Similarly, in the initial calculation, direct grid indices were used instead of interpolating
exactly the geographic limits of each region.
This may introduce small discrepancies, but given that the analyzed areas are large
and are located close to the equator, the impact due to the change in latitude (selecting different latitude values because they are on our grid) is minimal. Furthermore, not studying the exact zones down to tenths of a degree is not a problem since meridional gradients near the equator are smooth.
>

---

![SST_mean_interpoled](img/2.png)

---

<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
line-height:1.5;
">
<b>Methodological note.</b><br><br>

As we had already anticipated, spatial interpolation is not strictly necessary for the considered study regions. The effective area of each cell depends on the cosine of the latitude; given that our regions extend at most to ±5°, this factor takes values close to 0.996. Consequently, the relative error introduced by not weighting the area is less than 0.4 % even in the worst case.

This effect does not modifies the estimated trends and only introduces very small differences in maximum values, always less than 0.05 °C. Even so, and for methodological consistency, we will employ area-weighted mean definitions and maintain the same index selection criterion as used in interpolated case.

The direct selection by coordinates is simpler and more robust than selection by indices, as it avoids depending on the exact structure of the original coordinates of each dataset. To homogenize all products, we will use the function <code>interp2d_to_target</code> to interpolate the fields to a common grid with the following characteristics:

<ul style="margin-top:8px;">
  <li>Longitude: −180° to 180°</li>
  <li>Latitude: −90° to 90°</li>
  <li>Spatial resolution: <code>ddeg = 0.25°</code></li>
</ul>
</div>


---

![Data anomalies max](img/3.png)

---

<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">

This figure is used to evaluate the presence of outliers in the sea surface temperature anomalies corresponding to each dataset. It is observed that, in the case of **HadISST**, polar regions present extremely intense and physically inconsistent anomalies. In particular, maximum anomaly values on the order of **1318 °C** appear, which lacks physical sense and evidences the presence of errors in this database that must be filtered prior to analysis.

Conversely, in the other three analyzed databases, no comparable anomalous values are identified, showing consistent and physically reasonable behavior throughout the spatial domain. In this context, it is appropriate to apply a filtering threshold of **±10 °C**, given that the maximum anomaly observed at a point throughout the entire analyzed period is **9.27 °C**, which ensures the elimination of spurious values without affecting the real climate signal.

</div>


---

![Clean Outliers Haddist](img/4.png)

---

<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">

In this step, a global filter is applied that removes anomalies with absolute values greater than **±10 °C**. This threshold is adopted based on physical and empirical criteria, given that the maximum anomaly observed at a point throughout the entire analyzed period is **9.27 °C**. Thus, the filtering removes spurious values associated with data errors without affecting the real climate signal.

The application of this criterion significantly reduces the presence of physically inconsistent extreme anomalies, allowing us to obtain coherent and comparable spatial maps between the different analyzed datasets.

</div>


---

![Variabilidad Anom_SST](img/5.png)

---

<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">

<b>Monthly mean SST variability (61 years)</b><br><br>
Here, the mean variability of SST anomalies calculated from 61 years of data is shown
for each month of the year in the <b>ATL3</b> and <b>Niño3.4</b> regions, comparing the datasets
<span style="color:#d62728;"><b>HadISST</b></span> and 
<span style="color:#1f77b4;"><b>ERSST</b></span>.

This variability identifies the periods of the year in which ocean-atmospheric phenomena
present the greatest intensity:

<ul>
<li>
<b>Atlantic Niño (ATL3):</b>
maximum activity during the boreal summer, with peaks in
<b>June and July</b>.
</li>

<li>
<b>Pacific Niño (Niño3.4):</b>
maximum activity during the boreal winter, with peaks in
<b>December and January</b>.
</li>
</ul>

The differences between both databases are within expectations.
In the case of ATL3, 
<span style="color:#d62728;">HadISST</span> presents slightly higher peaks and minimums
than <span style="color:#1f77b4;">ERSST</span>.

The <b>relative</b> separation between 
<span style="color:#d62728;">HadISST</span> and 
<span style="color:#1f77b4;">ERSST</span>
is larger in the Atlantic Niño, which is visually appreciated in the graph.
In contrast, the Pacific Niño shows a much more similar signal between both databases.


However, in absolute terms, the differences between HadISST and ERSST are comparable in both
cases (≈ 0.05 °C). Therefore, ATL3 is not more inconsistent in absolute terms; it is just that the same data bias
has a greater relative weight when climate variability is smaller.


</div>



---

![Variabilidad Anom_PCP](img/6.png)

---

<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">
Unlike SST, the monthly variability of precipitation shows a greater dependence on the product used. NOAA PCP and NCEP-NCAR present coherent seasonal cycles in ATL3 and Niño-3.4, but with notable differences in amplitude and phase, especially in the equatorial Pacific. These discrepancies are expected given the highly non-linear nature of precipitation and the limitations of older reanalyses in tropical regions.

</div>



---

![Correlacion/Slope Anom_SST-index](img/7.png)

---

<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">
In the panels corresponding to the <b>Atlantic Niño</b> (left, <b>JJ</b>), a
<b>very localized</b> warming is observed in the <b>equatorial Atlantic</b>, clearly
<b>centered on the ATL3 region</b>.
The amplitude of the anomalies is <b>moderate in absolute terms</b> and significantly
<b>lower than that associated with ENSO</b>.
The spatial pattern is fundamentally <b>regional</b> and does not dominate the rest of the
ocean basins.
The stippled areas indicate regions with <b>statistical significance</b>, although their
spatial extent is <b>limited</b>, which reinforces the localized and seasonal character
of the phenomenon.
Overall, the Atlantic Niño manifests as a <b>seasonal, regional, and small spatial scale</b> event,
without evidencing <b>robust global interconnections</b>.
<br><br>

Conversely, in the panels corresponding to the <b>Pacific Niño / ENSO</b>
(right, <b>ND</b>), a <b>much more intense</b> warming is appreciated in the
<b>equatorial Pacific</b>, characterized by the presence of the <b>typical equatorial
warm tongue</b>.
The signal <b>extends widely</b> throughout the tropical Pacific and presents
<b>clear impacts in other ocean basins</b>.
The spatial pattern is more <b>zonally symmetric</b> and clearly
<b>dominant on a global scale</b>.
The stippled regions cover extensive areas, confirming the <b>statistical robustness</b>
of the pattern associated with ENSO.
In this sense, the Pacific Niño is identified as the <b>main mode of tropical interannual
variability</b>, characterized by the presence of <b>interconnections on a global
scale</b> that modulate climate variability in multiple regions of the planet.
</div>



---

![Correlacion/Slope Anom_PCP-index](img/8.png)

---

<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">
In the panels corresponding to the <b>Atlantic Niño</b> (left, <b>JJ</b>), in both the
<b>NOAA</b> and <b>NCEP</b> databases, precipitation anomalies are observed
<b>concentrated mainly in the equatorial Atlantic</b> and adjacent regions.
The rainfall pattern presents a predominantly <b>regional</b> structure, with
coherent signals in the Atlantic equatorial belt, but with a
<b>limited spatial extent</b>.
The stippled areas indicate regions with <b>statistical significance</b>, which are
restricted mostly to the tropical Atlantic and nearby continental zones.
This behavior reinforces the interpretation of the Atlantic Niño as a
<b>coupled ocean–atmosphere phenomenon of regional scope</b>.
<br><br>

However, the maps show that the <b>Atlantic Niño</b> can induce
<b>secondary remote atmospheric responses</b>, visible as weaker precipitation anomalies
in other regions, such as the <b>tropical Pacific</b>
(negative anomalies), <b>southern South America</b>, and sectors of the <b>Indian Ocean and Southeast
Asia</b>.
These signals present a <b>more irregular and fragmented</b> distribution,
with lower coherence between regions and <b>more limited statistical robustness</b>,
in addition to a greater dependence on the specific event and the database used.
<br><br>

Conversely, the panels corresponding to the <b>Pacific Niño / ENSO</b>
(right, <b>ND</b>) show <b>much more intense and
spatially extensive</b> precipitation anomalies, dominated by the <b>typical equatorial wet tongue</b> in the
Pacific.
This ocean warming induces a <b>highly organized atmospheric response</b>,
with clear compensations between regions, such as the characteristic pattern of a
<b>wet central Pacific</b> and <b>drier regions of Asia and the western Pacific</b>.
The stippled areas cover <b>wide regions of the globe</b>, confirming the
<b>statistical robustness</b> and consistency of the pattern between datasets.
<br><br>

These differences reveal that the key distinction between both phenomena
<b>does not lie in the presence or absence of remote responses</b>, but in their
<b>coherence, organization, and dynamic dominance</b>.
<b>ENSO</b> generates <b>robust and repeatable climate teleconnections</b>, associated with
a <b>clear reconfiguration of the Walker circulation</b> and adjustments in the
<b>Hadley</b> circulation, giving rise to a global reorganization of the precipitation field.
<br><br>

The <b>Atlantic Niño</b>, on the other hand, can induce remote responses, but these are
<b>weaker, less symmetric, less persistent</b>, and
<b>not dominant against the internal variability of the climate system</b>.
This dynamic difference constitutes the <b>physical justification</b> for requiring, in the
identification of <b>Atlantic Niño</b> events, <b>independence regarding ENSO</b>.
Even when thermal and temporal criteria are met in <b>ATL3</b>, the simultaneous
presence of an active ENSO can give rise to induced atmospheric responses,
generating <b>false positives</b> if the state of the
Pacific is not explicitly considered.
</div>


---

<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">
<b>Identification of years of maximum thermal intensity</b><br><br>

In this section, the <b>five years with the highest temperature peaks</b> in the
<b>Niño&nbsp;3.4</b> and <b>ATL3</b> regions during the period 1960–2020 are identified.
Given that warming episodes associated with these phenomena present a characteristic recurrence,
the detected thermal maximums can be interpreted as
<b>indicators of the possible occurrence of Niño events</b> in each of the regions.
<br><br>
These years are subsequently used to analyze if
<b>Pacific Niño</b> events actually occurred in the Niño&nbsp;3.4 region and <b>Atlantic Niño</b> events in the ATL3 region,
as well as to investigate possible interactions between both systems.
It is worth noting that <b>thermal peaks, on their own, do not constitute conclusive proof</b>
of the occurrence of these events.
However, by analyzing SST anomalies and comparing them with the
<b>monthly mean variability</b> characteristic of each region,
it is possible to determine if said years effectively correspond to Niño episodes.
This approach allows us to deepen the detection and characterization of these climate events
in a robust and consistent manner.
</div>







<b>Characterization of event intensity</b><br>

The relationship between the mean of anomalies in the peak months and the standard deviation
(interannual) is used to calculate a standardized index <b>Z</b>, which allows for
evaluating both the intensity and rarity of the event, once it is verified that the distributions
present reasonable statistical normality.
The following classification is adopted:
<ul>
<li><b>Z &lt; 0.5:</b> event not considered as a case study.</li>
<li><b>0.5 ≤ Z &lt; 1.0:</b> weak event.</li>
<li><b>1.0 ≤ Z &lt; 1.5:</b> moderate event.</li>
<li><b>Z ≥ 1.5:</b> strong event.</li>
</ul>

</div>

---

![Histograma ATL3 y Niño3.4](img/9.png)

---

<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">
Although many studies directly assume the normality of the data, in this work
it has been explicitly verified that, for the <b>61 years</b> analyzed and for the
<b>JJ</b> and <b>ND</b> months of each series, the anomalies present an
<b>approximately Gaussian trend</b>.
In the case of the <b>Atlantic Niño</b>, the fit to the normal distribution is clearer,
although both series remain within a regime of
<b>reasonable statistical normality</b>.
<br><br>

This verification is relevant, as it allows us to consistently quantify
the <b>rarity of thermal anomalies</b>.
The values represented in the histogram indicate the frequency with which certain
mean anomalies occur in each region and set of months, considering one value per year.
As is expected in an approximately normal distribution, the frequency decreases towards
the extremes, reflecting that more intense anomalies are less common.
<br><br>

In the context of this study, the interest focuses mainly on
<b>positive anomalies</b>, given that both the <b>Pacific Niño</b> and the
<b>Atlantic Niño</b> are characterized by increases in sea surface temperature.
For this reason, the analysis of the positive tail of the distribution is especially relevant.
<br><br>

The <b>84th and 90th percentiles</b> constitute useful statistical measures to evaluate the
rarity of an event, as they indicate the values above which only
<b>16%</b> and <b>10%</b> of cases are found, respectively.
These thresholds allow us to contextualize the intensity of a specific event within the
historical variability of the region and facilitate the identification of
exceptionally intense episodes.
</div>

---

<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">

<b>Methodology for Pacific Niño events</b><br><br>

For the case of ENSO, the convention of the <b>ONI (Oceanic Niño Index)</b> defined by NOAA is adopted:
<ul>
<li><b>Threshold:</b> anomaly ≥ 0.5&nbsp;°C in the Niño&nbsp;3.4 region.</li>
<li><b>Duration:</b> at least 5 consecutive running quarters (overlapping 3-month averages).</li>
</ul>
In addition to determining the events, we seek to know their <b>intensity</b> based on the months of maximum development
(<b>November–December</b>), calculating the mean of the anomalies in those months and
comparing it with their <b>interannual standard deviation</b> in those months.
From this relationship, the standardized index <b>Z</b> is obtained, previously used for the functions that classify event intensity.
<br><br>

From a qualitative point of view, it is expected that, in the presence of an event,
the shape of the graph reproduces the <b>temporal variability characteristic</b> of the Pacific Niño,
with interannual anomalies concentrated in the boreal winter and peaks in the last months
of the first year. When the maximums occur in the expected months and the temporal evolution
is consistent, the event is classified as <b>canonical</b>.
<br><br>

However, there may be cases that strictly meet the ONI criterion but present
a different temporal evolution. In these cases, the event is not considered canonical,
although <b>it is still classified as a Niño event</b>.

To facilitate the identification of these situations, the anomalies are represented in an
interval of <b>two consecutive years</b>; that is, the graph is made for two years in a row,
which allows for correctly visualizing the transition and temporal development of the phenomenon.


Events of longer duration may exist, in which the criterion of five consecutive running quarters
extends beyond two years. In these cases, the months of maximum development
may not coincide with the expected climatology, reinforcing their non-canonical character.
To adequately analyze these events, it is necessary to apply the function in two overlapping intervals
(years 1–2 and years 2–3), in order to reconstruct their complete evolution.

Since thermal peaks do not necessarily coincide with typical months, the comparison
with the standard deviation becomes less direct. However, a homogeneous criterion is maintained
and anomalies are evaluated in the months of <b>November–December</b>, even when these do not
correspond exactly to the maximum peaks of the event.


As an alternative approach, the maximum anomaly value of the event could be directly compared
with the maximums of the standard deviation, regardless of the time of year they
occur. <b>This alternative approach is not performed in the present function</b> and I mention it only
as a possible methodological extension, especially relevant for non-canonical
or prolonged duration events.

All these calculations —event detection, intensity, and Z value— are performed
consistently for both databases employed (<b>HADISST</b> and <b>ERSST</b>).
</div>


---

#Possible ENSO between 1972-1973

![Detection_Plot_ENSO_ONI_with_intensity(1972, 1973)](img/10.png)

---

<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">
Between <b>1972 and 1973</b>, a clear case of <b>canonical Pacific Niño</b> is identified.
The temporal evolution of the anomalies coincides with the expected form of the phenomenon,
with maximums concentrated at the end of the year, and up to
<b>11 consecutive running quarters</b> with anomalies greater than <b>0.5&nbsp;°C</b> are observed,
amply meeting the ONI criterion.
<br><br>

The mean temperature in the months of maximum development is on the order of
<b>2&nbsp;°C</b>, and the standardized index <b>Z</b> reaches a value close to <b>1.8</b>,
which places this episode at the upper limit of the category of
<b>strong events</b>.

Likewise, the event is clearly above the
<b>90th percentile</b> (<b>0.911&nbsp;°C</b>), indicating that anomalies of this magnitude
occur in less than <b>10%</b> of the analyzed years,
confirming its exceptional character within the study period.
</div>

---

#Possible ENSO between 1982-1983

![Detection_Plot_ENSO_ONI_with_intensity(1982, 1983)](img/11.png)

---

<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">
Between <b>1982 and 1983</b>, a clear case of <b>canonical Pacific Niño</b> is identified.
The temporal evolution of the anomalies coincides with the expected form, and up to
<b>14 consecutive running quarters</b> with anomalies greater than <b>0.5&nbsp;°C</b> are observed,
meeting the 5 consecutive month criterion of the ONI.
<br><br>

The mean temperature in the months of maximum development is greater than
<b>2&nbsp;°C</b>, and the standardized index <b>Z</b> reaches a value close to <b>1.9</b>,
which places this episode at the upper limit of the category of
<b>strong events</b>, having greater development and intensity than the previous case.


</div>

---

#Possible ENSO between 1987-1988

![Detection_Plot_ENSO_ONI_with_intensity(1987, 1988)](img/12.png)

---

<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">
Here, between <b>1987 and 1988</b>, we see a <b>Pacific Niño</b> event with particular
characteristics. The episode comfortably meets the <b>ONI</b> criterion, so it is
classified as a Niño event; however, its anomaly maximums do not coincide with those
of a <b>canonical event</b>.
<br><br>

While in typical ENSO events the maximums are concentrated in the winter
boreal, in this case, <b>persistent positive anomalies are observed throughout
much of the year</b>, although with lower intensities than those recorded in the
most extreme events.
<br><br>

In particular, the mean temperature anomalies in the months of
<b>November–December</b> reach values of <b>1.14&nbsp;°C</b> in the
<b>HADISST</b> database and <b>1.11&nbsp;°C</b> in <b>ERSST</b>, with a <b>Z</b> index close to <b>1</b>,
at the limit of a weak event, which confirms some thermal relevance
of the episode despite its non-canonical character.
<br><br>

In order to analyze the full temporal structure of the event in greater detail,
the years <b>1986–1987</b> will be represented in the following cell, which
will allow us to visualize its complete development and determine its duration.
</div>

---

#Study of ENSO between 1987-1988

![Detection_Plot_ENSO_ONI_with_intensity(1987, 1988)](img/13.png)

---

<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">
From the shape of the anomalies, it is confirmed that the event starts in <b>1986</b> and
ends in <b>1988</b>. It is a peculiar <b>Pacific Niño</b>, which extends over
<b>three consecutive years</b> with positive anomalies.
<br><br>

The temporal structure is, in reality, similar to that of a canonical event both at
the beginning (<b>1986</b>) and at the end (<b>1988</b>), with anomaly peaks close to
<b>1&nbsp;°C</b> and <b>Z</b> index values indicating a <b>weak event</b>.
What distinguishes this episode is that the level of moderate anomaly is maintained
persistently throughout <b>1987</b>.
</div>

---

#Possible ENSO between 1997-1998

![Detection_Plot_ENSO_ONI_with_intensity(1997, 1998)](img/14.png)

---

<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">
Here, another episode of the <b>Pacific Niño</b> is identified, corresponding to the period
<b>1997–1998</b>, of a <b>very intense</b> character.
The mean anomaly in the months of <b>November–December</b> reaches values of
<b>2.17&nbsp;°C</b> in <b>HADISST</b> and <b>2.22&nbsp;°C</b> in <b>ERSST</b>,
much higher than its typical variability, which results in a <b>Z</b> index
<b>greater than 2</b>.
<br><br>

This value places the episode among the <b>strongest Pacific Niño events</b>
recorded in the study period.
</div>


---

#Possible ENSO between 2015-2016

![Detection_Plot_ENSO_ONI_with_intensity(2015, 2016)](img/15.png)

---

<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">
The anomalies corresponding to the period <b>2015–2016</b> comfortably meet the
<b>ONI</b> criterion of <b>five consecutive running quarters</b> above
<b>0.5&nbsp;°C</b>.
It is an especially intense <b>Pacific Niño</b>, with a mean anomaly in the
months of <b>November–December</b> of <b>2.32&nbsp;°C</b>.
<br><br>

This episode constitutes the <b>most intense Niño event</b> recorded in the period
<b>1960–2020</b>, with a <b>Z</b> index greater than <b>2.2</b>, confirming its
extremely exceptional character.
</div>

---

<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">

<b>Methodology for Atlantic Niño events</b><br><br>

The <b>Atlantic Niño</b> is characterized by presenting its maximum relevance during the
<b>boreal summer</b>, unlike the <b>Pacific Niño</b>, which is a phenomenon of
<b>interannual</b> nature. The Atlantic Niño not only presents a <b>considerably shorter duration</b>,
but also shows <b>slightly lower intensity</b> and a <b>more local character</b>,
as discussed in previous sections.

In the case of the <b>Atlantic Niño</b>, being a less persistent and intense phenomenon,
it is considered sufficient to record <b>at least three consecutive months</b> with anomalies
greater than <b>0.4 °C</b> in the <b>ATL3</b> region in the summer.
<br><br>

Since the use of quarterly running means is not necessary, the representation of
<b>monthly anomalies</b> is suitable for the identification of the event.
Furthermore, the representation of the <b>characteristic climate variability</b> of the
region, previously analyzed in earlier sections, is included. From a qualitative point of view,
it is expected that, in the presence of an event, the shape of the graph reproduces said variability,
but with a thermal signal clearly highlighted during the months of maximum development.

To characterize the <b>intensity</b> of the episode, the mean of the anomalies
in the months of maximum development (<b>June–July</b>) is considered. Comparing it with the
<b>interannual standard deviation</b> corresponding to those same months yields the
standardized index <b>Z</b>, which allows for objectively quantifying the magnitude of the event.
<br><br>

Additionally, since the Atlantic Niño is a <b>more local and much less influential</b> phenomenon
than <b>ENSO</b>, an additional condition is introduced: <b>independence regarding ENSO</b>.
This implies that the absence of an active ENSO during the same observation period must be explicitly verified.
Otherwise, even if the episode meets the established thermal and temporal criteria, the warming
observed in the Atlantic must be interpreted as an <b>induced or modulated response by ENSO</b>,
and not as an <b>Atlantic Niño proper</b>.

All these calculations —event detection, intensity, and Z value— are performed
consistently for both databases employed (<b>HADISST</b> and <b>ERSST</b>).

</div>

---

#Possible Atlantic Niño in 2010

![Detection_Plot_ATL3(2010)](img/16.png)

---

<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">
In none of the databases is the criterion of
<b>three consecutive months with positive anomalies greater than 0.4&nbsp;°C</b> met.
Furthermore, the observed intensity is low, so the episode
<b>does not meet the established criteria</b> to be classified as an event.
<br><br>

However, in the **HADISST** database, at least
<b>two consecutive peaks</b> are observed in the expected months, which, under
less restrictive criteria, would allow this case to be considered as a
<b>very weak Atlantic Niño</b>.
</div>

---

#Possible Atlantic Niño in 2016

![Detection_Plot_ATL3(2016)](img/17.png)

---

<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">
These anomalies present a more coherent shape than in the previous cases,
but the peaks are <b>very low intensity</b>.
In the <b>HADISST</b> database, not even
<b>two consecutive peaks</b> above the established threshold of <b>0.4&nbsp;°C</b> are observed.
<br><br>

In <b>ERSST</b>, peaks are identified in the months of <b>July</b> and <b>August</b>
greater than said threshold; however, these do not meet the
<b>necessary requirements</b> to confirm the occurrence of an <b>Atlantic Niño</b>.
</div>

---

#Possible Atlantic Niño in 2018

![Detection_Plot_ATL3(2018)](img/18.png)


---

<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">
The anomalies of 2018 have a very different shape than expected and the requirements of 3 months above the 0.4 C threshold are not met; their peaks are very low intensity, also with values lower than the Z index threshold = 0.5.
</div>

---

#Possible Atlantic Niño in 2019

![Detection_Plot_ATL3(2018)](img/19.png)


---

<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">
The anomalies of <b>2019</b> present a totally different shape than expected.
Although a high peak is observed at the end of the year, this does not coincide with the time when
the maximum should occur in the ATL3 region.
Furthermore, in 2019 the criterion of <b>three consecutive months</b> with anomalies
greater than the established threshold is not met.
<br><br>

However, <b>2020</b> will be analyzed below to evaluate if this case could
correspond to a possible <b>interannual Atlantic Niño</b>.
</div>

---

#Possible Atlantic Niño in 2020

![Detection_Plot_ATL3(2029)](img/20.png)

---

<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">
As expected, the anomalies of <b>2020</b> still do not resemble the typical structure
of the <b>Atlantic Niño</b>, with values close to <b>0&nbsp;°C</b> during the boreal summer.
<br><br>

However, if the anomalies of <b>2019</b> and <b>2020</b> are considered jointly,
one could speculate on the existence of a warm episode between the end and beginning of the year.
In this case, the criterion of <b>three consecutive months</b> is met, and the anomalies in
said interval reach values close to <b>1&nbsp;°C</b>, which would allow it to be classified,
from a purely statistical point of view, as a <b>moderate event</b> with a
<b>temporal lag</b>.
<br><br>

However, the <b>Atlantic Niño</b> is characterized by being a
<b>seasonal</b> phenomenon, associated with the <b>boreal summer</b>. Although the
temporal duration condition is met when considering months of consecutive years, the
<b>physical condition</b> that the event develops during the summer months is not satisfied.
For this reason, the episode <b>is not considered an Atlantic Niño event</b>.

We see that the selection of <b>Atlantic Niño</b> events has not identified
study years as representative as in the case of the <b>Pacific Niño</b>.
This is because the initial selection was made based on
<b>mean temperatures</b> and not <b>anomalies</b>, which introduces a bias towards
more recent years as a consequence of <b>global warming</b>.
Furthermore, an <b>annual mean</b> has been used, which dilutes the seasonal signal characteristic
of the Atlantic Niño.
<br><br>

In the case of the <b>Pacific Niño</b>, this bias is less relevant, since it is a more
intense, persistent, and interannual phenomenon, whose anomalies clearly dominate over the
global warming trend. Even when using annual means, the event signal remains representative
of the months of maximum development.
This does not occur in the <b>Atlantic Niño</b>, whose signal is weaker, localized, and strongly
seasonal.
<br><br>

For this reason, we will proceed to calculate a new selection of **Atlantic Niño** events, and this new selection is based on two main adjustments.
<br><br>

<ul>
  <li>
    <strong>Use of seasonal anomalies instead of absolute SST.</strong><br>
    Anomalies of SST are employed to minimize the effect of background warming and avoid
    a bias towards recent years. This aspect is especially relevant in the
    Atlantic Niño, whose thermal signal is weaker and localized, and does not dominate the annual mean.
    Consequently, years with high annual SST may not correspond to ATL3 events
    properly speaking.
  </li>

  <li>
    <strong>Selection centered on the months of maximum development.</strong><br>
    Instead of the annual mean, the mean of the anomalies during the characteristic months
    of the phenomenon (<strong>June–July–August, JJA</strong>) is calculated and the
    <strong>five years with the greatest seasonal intensity</strong> are selected.
    This criterion allows identifying events associated with the physical mechanism of the
    Atlantic Niño and discarding anomalies outside its seasonal window. 
  </li>
</ul>

The selection of <strong>Pacific Niño</strong> years is barely modified, which highlights the
<strong>robustness of the original criterion</strong> for this event. This
robustness is explained by the <strong>highly influential, intense, and interannual character</strong>
of the Pacific Niño, whose anomalies dominate the climate signal on a global scale during much
of the year. As a consequence, even when employing annual means, the identification of
episodes proves little sensitive to both the averaging method and the
<strong>progressive increase of the mean thermal level associated with climate change</strong>.
Only the year <strong>1987</strong> is excluded, corresponding to the least canonical episode,
and the year <strong>1965</strong> is incorporated.
<br><br>

Conversely, the selection of <strong>Atlantic Niño</strong> years changes substantially,
confirming that the identification based on <strong>annual mean SST</strong>
is not suitable for this phenomenon. Due to its <strong>lower intensity</strong>,
<strong>shorter duration</strong>, and <strong>markedly seasonal character</strong>, the Atlantic
Niño is much more sensitive to the selection method, which reinforces the need for a
<strong>seasonal approach based on anomalies</strong> to identify physically
consistent episodes.

</div>


---

#Possible ENSO between 1965-1966

![Detection_Plot_ENSO_ONI_with_intensity(1965, 1966)](img/21.png)

---

<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">
Between <b>1965 and 1966</b>, another <b>canonical Pacific Niño</b> is observed.
The temporal evolution of the anomalies coincides with the expected form of the phenomenon,
with maximums concentrated at the end of the year, and up to
<b>11 consecutive running quarters</b> with anomalies greater than <b>0.5&nbsp;°C</b> are identified,
amply meeting the ONI criterion.

The mean temperature in the months of maximum development is on the order of
<b>1.5&nbsp;°C</b>, and the standardized index <b>Z</b> reaches a value close to <b>1.4</b>,
which places this episode at the upper limit of the category of
<b>moderate events</b> and close to being classified as a <b>strong event</b>.

It is worth noting that, even being the <b>least intense</b> episode within this
<b>TOP&nbsp;5</b>, it presents a thermal signal clearly relevant and coherent with
a Pacific Niño of great magnitude.
</div>

---

#Possible Atlantic Niño in 1963

![Detection_Plot_ATL3(1963)](img/22.png)

---

<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">
The anomalies corresponding to the year <b>1963</b> meet the established criterion of
<b>three consecutive months</b> with anomalies greater than <b>0.4&nbsp;°C</b> in both databases.
The temporal evolution presents a structure coherent with a <b>canonical event</b>,
and the intensity of the episode is high, with <b>Z</b> index values of
<b>2.17</b> for <b>HADISST</b> and <b>2.33</b> for <b>ERSST</b>.
<br><br>

This episode is situated among the <b>most intense Atlantic Niño events</b> recorded
in the period <b>1960–2020</b>, with a mean anomaly in the months of maximum development
of <b>1.29&nbsp;°C</b> for <b>HADISST</b> and <b>1.36&nbsp;°C</b> for <b>ERSST</b>.
These values are comparable, in terms of thermal magnitude, to those of some
<b>Pacific Niño</b> events, despite the latter being, in general, more intense and lasting.
<br><br>

As observed later in the <b>global anomalies (Year-Criteria)</b> figure, the anomalies
associated with the <b>Niño&nbsp;3.4</b> region during 1963 are of <b>lesser magnitude</b> and do not
present a characteristic structure of active ENSO, while the warming in the
<b>equatorial Atlantic</b> is dominant and spatially coherent.
This difference in magnitudes reinforces the interpretation of <b>1963</b> as a
<b>strong and independent Atlantic Niño</b>.
<br><br>

Overall, this case confirms that the <b>new seasonal selection based on anomalies</b>
identifies in a more consistent manner the representative years of the <b>Atlantic Niño</b>,
even in episodes less persistent than those of the <b>Pacific Niño</b>.
</div>


---

#Possible Atlantic Niño in 1966

![Detection_Plot_ATL3(1966)](img/23.png)

---

<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">
In <b>1966</b>, an increase in anomalies in <b>ATL3</b> is observed during the
<b>boreal summer</b>, with a <b>moderate</b> intensity, given that the <b>Z</b> index reaches
values of <b>1.34</b> in <b>HADISST</b> and <b>1.36</b> in <b>ERSST</b>.
The presence of well-defined peaks reinforces the interpretation of this episode as a
possible <b>Atlantic Niño</b>; however, the requirement of
<b>three consecutive months</b> above the threshold of <b>0.4&nbsp;°C</b> is not met, due to the
rapid decrease of anomalies starting in <b>August</b>.
<br><br>

It is worth noting that this episode occurs during the weakening phase of the
<b>Pacific Niño 1965–1966</b>. During the summer months, the anomalies in
<b>Niño&nbsp;3.4</b> are already reduced, which suggests that the warming observed in
<b>ATL3</b> is not being directly forced by an active ENSO.

As a sensitivity analysis, if an alternative, looser threshold
(<b>0.35&nbsp;°C</b>) were considered, this episode would meet the duration condition and could
be classified as a <b>canonical Atlantic Niño</b>, although of a <b>very fleeting</b> character.
</div>


---

#Possible Atlantic Niño in 1968

![Detection_Plot_ATL3(1968)](img/24.png)

---

<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">
The <b>Atlantic Niño of 1968</b> is identified, which meets the criterion of
<b>three or more consecutive months</b> with anomalies greater than <b>0.4&nbsp;°C</b> during the
<b>boreal summer</b>.
The intensity of the episode is high, with a mean temperature in the months of maximum
development of <b>1.31&nbsp;°C</b> in <b>HADISST</b> and <b>1.10&nbsp;°C</b> in <b>ERSST</b>,
giving rise to <b>Z</b> index values greater than <b>2</b> in <b>HADISST</b> and
<b>1.88</b> in <b>ERSST</b>.
According to the adopted classification, this episode is considered a <b>strong event</b>.
<br><br>

As shown later in the <b>global anomalies (Year-Criteria)</b> figure,
no significant anomalies are observed in the <b>Niño&nbsp;3.4</b> region during this year,
which reinforces the interpretation of <b>1968</b> as an <b>independent Atlantic Niño</b>,
not associated with an active ENSO.
</div>


---

#Possible Atlantic Niño in 1987

![Detection_Plot_ATL3(1987)](img/25.png)

---

<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">
The year <b>1987</b> meets the thermal and temporal criterion defined for the detection of
<b>ATL3</b> events; however, its coincidence with a <b>prolonged Pacific Niño</b> and its
<b>non-canonical</b> character suggest that it is an Atlantic warming
<b>modulated by ENSO</b>, rather than an <b>independent Atlantic Niño</b>.
<br><br>

This episode is not part of the <b>TOP5</b> selected events, although it is found
among the years with the highest anomalies in <b>JJ</b>. It is included as a case study because
it illustrates that the tropical Atlantic can respond during an active ENSO, which constitutes
a relevant methodological warning: even when thermal thresholds are met and
moderate intensities are obtained, it is necessary to evaluate the <b>complete dynamic context</b>.
<br><br>

For this reason, in the final interpretation of the results,
<b>independence regarding ENSO</b> is introduced as an <b>additional classification criterion</b>,
used to distinguish between genuine Atlantic events and warmings induced
or modulated by the Pacific Niño.
Consequently, for <b>all years in which an Atlantic Niño is declared</b>,
it is necessary to explicitly check whether or not there is an <b>active ENSO</b> in the
Pacific, in order to avoid the identification of <b>false positives</b> and ensure
a physically consistent interpretation of the detected events.
</div>


---

#Possible Atlantic Niño in 1988

![Detection_Plot_ATL3(1988)](img/26.png)

---

<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">
Unlike <b>1987</b>, the <b>1988</b> episode presents a <b>well-defined seasonal
structure</b>, with maximums concentrated in the <b>boreal summer</b> and anomalies that clearly exceed
the climatological variability.
Furthermore, the event develops once the <b>Pacific Niño 1986–1988</b> has finished, which
reduces the probability of direct forcing by ENSO and reinforces its interpretation as an
<b>Atlantic Niño proper</b>.
<br><br>

The intensity of the episode is situated between <b>moderate and strong</b>, depending on the database
considered.
Although <b>ERSST</b> tends to present slightly higher values than <b>HADISST</b>, in this
case the difference is more marked, with a discrepancy between means greater than
<b>0.2&nbsp;°C</b>.
The <b>Z</b> index reaches values of <b>1.43</b> in <b>HADISST</b> and <b>1.85</b> in
<b>ERSST</b>, confirming the relevance of the episode.
</div>


---

#Possible Atlantic Niño in 1996

![Detection_Plot_ATL3(1996)](img/27.png)

---

<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">
In <b>1996</b>, a <b>typical case of Atlantic Niño</b> is observed.
The conditions of <b>three consecutive months</b> with anomalies greater than
<b>0.4&nbsp;°C</b> are met, and the event intensity is <b>moderate</b>.
Both databases show a very similar evolution, which reinforces the
<b>coherence and robustness</b> of the observed signal.
<br><br>

Likewise, in the <b>“Year-Criteria”</b> figure, it is appreciated that anomalies in the
<b>Pacific</b> during 1996 are <b>insignificant</b>, which confirms that this
<b>Atlantic Niño</b> can be considered an <b>independent event</b>, not forced by
an active ENSO.
</div

---

<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">
This function integrates <b>two main functionalities</b>:
<br><br>

<ul>
  <li>
    <b>Representation of global anomalies.</b><br>
    Allows visualizing <b>global SST anomalies</b> corresponding to
    <b>four different events</b> (four different years) in a set of
    <b>selected months</b>.
    It is possible to choose the <b>database</b>, the <b>years to analyze</b>, the
    <b>months of interest</b>, and the <b>color scale</b>, which facilitates the graphical comparison
    of the relative intensity of the studied events.
    This type of representation shows all anomalies present in each year, not only
    those associated with the main event, which allows identifying cases like <b>1987</b>,
    where a <b>prolonged ENSO</b> coexisted together with anomalies in the <b>ATL3</b> region.
  </li>
  <br>

  <li>
    <b>Animation generation (GIF).</b><br>
    Reproduces an animation showing the <b>temporal evolution of the anomalies</b>
    month by month, using <b>two months per frame</b>.
    For <b>Atlantic Niño</b> events, the selection of <b>a single year</b> is sufficient;
    in this case, it suffices to enter the study year as <b>year 1</b> and assign
    a value <b>0</b> to <b>year 2</b>.
    In the case of <b>ENSO</b>, where the development is <b>interannual</b>, two consecutive years
    must be indicated.
    The parameters <b>year 3</b>, <b>year 4</b>, and the selection of months are not relevant
    for the generation of the GIF.
  </li>
</ul>
</div>


---

#Figure YEAR-CRITERIA  

![Plot_global_mean_anoms_with_Z("a", 1963, 1968, 1987, 1996, months_sel=[5,6], min_abs_temp=1.5, event=None) ](img/28.png)

---

<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">
This is the <b>YEAR-CRITERIA</b> figure, built from the <b>HADISST</b> database,
and used to evaluate whether, during the study years of the
<b>Atlantic Niño</b>, the presence of an <b>active ENSO</b> in the Pacific is observed.
<br><br>

First, the case of <b>1963</b> is shown, in which
<b>weak positive anomalies</b> are appreciated in the <b>Niño&nbsp;3.4</b> region that could suggest the
existence of an incipient ENSO.
However, the anomalies in the <b>equatorial Atlantic</b> are clearly of
<b>greater magnitude</b>, which confirms that the dominant event that year corresponds to a
<b>strong Atlantic Niño</b>, while the signal in the Pacific is interpreted as a
<b>secondary perturbation</b>.
<br><br>

Next, the year <b>1987</b> is presented, where an <b>active Pacific Niño</b> is clearly observed,
reflected in significant anomalies in the equatorial Pacific.
This case illustrates a scenario in which the Atlantic can respond during a prolonged ENSO,
giving rise to a <b>non-independent</b> event.
<br><br>

Finally, the years <b>1996</b> and <b>1968</b> are shown, in which no relevant
positive anomalies are identified in the Pacific, confirming the absence of an active ENSO.
These years constitute examples of <b>independent Atlantic Niños</b>, not forced by the
variability of the Pacific.
</div>



---

#Altanic Niño in 1960-1996-1968-1963

![Plot_global_mean_anoms_with_Z("b", 1960,1996 ,1968 ,1963 , [5,6], min_abs_temp=1.5)](img/29.png)

---

<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">
In this figure, using the <b>ERSST</b> database, different
<b>Atlantic Niño events</b> are compared, represented during the months of <b>June–July</b>,
with the aim of evaluating their intensity and spatial extent.
<br><br>

<ul>
  <li>
    <b>First image (1960).</b><br>
    Corresponds to a <b>neutral year</b>, without notable anomalies in the equatorial
    Atlantic. The <b>Z</b> index is close to <b>0</b>, confirming the absence of
    an Atlantic Niño event.
  </li>
  <br>

  <li>
    <b>Second image (1996).</b><br>
    Shows a <b>moderate Atlantic Niño</b>, characterized by a
    <b>Z ≈ 1.3</b> index. The warming is visible in the <b>ATL3</b> region, but does not stand out
    significantly on a global scale against other anomalies present in
    different areas.
  </li>
  <br>

  <li>
    <b>Third image (1968).</b><br>
    Corresponds to a <b>strong Atlantic Niño</b>, with a
    <b>Z ≈ 1.88</b> index. The warming is intense but <b>very focused</b> in the equatorial
    Atlantic, with limited spatial extent.
  </li>
  <br>

  <li>
    <b>Fourth image (1963).</b><br>
    Represents the <b>most intense event</b> of the analyzed set, with a
    <b>Z ≈ 2.33</b> index. In this case, the anomalies are <b>wider and more intense</b>,
    clearly dominating the thermal signal in the equatorial Atlantic.
  </li>
</ul>
</div>


---


![Plot_global_mean_anoms_with_Z("a", 1963, 0, 1972, 2015, months_sel=[10,11], min_abs_temp=2, event="Atlantic Niño")](gif/1.gif)

---

<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">
The GIF, built from the <b>HADISST</b> database, shows the
<b>temporal evolution of the Atlantic Niño of 1963</b>, allowing us to follow month by month the
spatial development of SST anomalies.
It is clearly observed how the <b>anomaly maximums are concentrated during the boreal summer</b>,
in coherence with the seasonality characteristic of the phenomenon in the region
<b>ATL3</b>.
This event has been selected illustratively because it presents the
<b>highest Z index</b> of all analyzed cases (<b>Z ≈ 2.2</b>), which facilitates
a clear visual identification of the phenomenon and its spatial structure.
<br><br>

Furthermore, together with the Atlantic maximum in <b>JJ</b>, a <b>slight simultaneous
warming</b> is appreciated in the <b>Niño&nbsp;3.4</b> region, which subsequently strengthens towards
<b>ND</b>. Given that the magnitude of the anomalies in the Pacific is significantly lower than
that observed in the Atlantic, this pattern suggests that the <b>Atlantic Niño</b> could have
acted as a <b>modulation or preconditioning mechanism</b> of the Pacific, rather than
as a fully developed ENSO.
<br><br>

This evolution is compatible with a delayed response of the Pacific to atmospheric
perturbations induced in the Atlantic, possibly through modifications in the
Walker circulation. However, this relationship is interpreted as a
<b>plausible physical hypothesis</b> and not as conclusive evidence of direct forcing.
</div>



---

#Pacific Niño in 1960-1987-1972-2015


![Plot_global_mean_anoms_with_Z("a", 1960, 1987, 1972, 2015, months_sel=[10,11], min_abs_temp=3)](img/29.png)


---

<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">
In this figure, using the <b>HADISST</b> database, different
<b>Pacific Niño events</b> are compared, represented during the months of
<b>November–December</b>, with the aim of evaluating their intensity and spatial extent.
<br><br>

<ul>
  <li>
    <b>First image (1960).</b><br>
    Corresponds to a <b>neutral year</b>, without notable anomalies in the equatorial
    Pacific. The <b>Z</b> index is close to <b>0</b>, confirming the absence of
    an active <b>ENSO</b> during that year.
  </li>
  <br>

  <li>
    <b>Second image (1987).</b><br>
    Shows a <b>weak to moderate Pacific Niño</b>, corresponding to the case of a
    <b>prolonged Niño</b>, in which positive anomalies are maintained throughout the
    year, weakening progressively towards <b>1988</b>.
    The characteristic <b>warm tongue</b> over the equatorial Pacific is visible,
    although less intense than in strong canonical events.
  </li>
  <br>

  <li>
    <b>Third image (1972).</b><br>
    Corresponds to a <b>strong Pacific Niño</b>, with a <b>Z ≈ 1.78</b> index.
    The temperature anomalies in the equatorial Pacific region are
    significantly more intense than in the previous case, placing this episode
    among the <b>most intense Niños</b> of the analyzed period.
  </li>
  <br>

  <li>
    <b>Fourth image (2015).</b><br>
    Represents the <b>most intense Pacific Niño</b> of the data sample, with a
    <b>Z ≈ 2.13</b> index.
    In this case, the anomalies are more extensive and intense than in <b>1972</b>, although
    the difference between both events is not extremely large in spatial terms.
  </li>
</ul>
</div>



---


![Plot_global_mean_anoms_with_Z("a", 2015, 2016, 1972, 2015, months_sel=[10,11], min_abs_temp=3, event="Pacific Niño")](gif/2.gif)


---

<div style="
background-color:#f7f7f7;
border-left:5px solid #444;
padding:14px;
border-radius:4px;
">
The GIF, built from the <b>HADISST</b> database, shows the
<b>temporal evolution of the Pacific Niño of 2015</b>, allowing us to follow month by month the
spatial development of SST anomalies in the <b>Niño&nbsp;3.4</b> region.
It is clearly observed how the <b>anomaly maximums are concentrated in the boreal winter</b>,
in coherence with the seasonality characteristic of <b>ENSO</b> events.
<br><br>

This event has been selected illustratively because it presents the
<b>highest Z index</b> of the analyzed period (<b>Z ≈ 2.13</b>), which facilitates a
clear visual identification of the phenomenon and its spatial structure.
During the peak of the event, the <b>thermal anomalies reach values greater than
<b>2&nbsp;°C</b></b>, evidencing the exceptional magnitude of the warming and confirming
its classification as one of the <b>most intense Pacific Niños</b> recorded.
</div>
