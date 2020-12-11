#### 1. Create new location in GRASS GIS

- New
- GIS Data Directory: grassdata
- Project Location: BadenWuerttemberg
- Weiter
- Read projection and datum terms from a georeferenced data file
- Weiter
- Georeferenced file: GHS_POP_E2015_GLOBE_R2019A_54009_250_V1_0_18_3.tif
- Weiter und fertigstellen
- Neu erstellte Location und PERMANENT-Mapset auswählen, dann Session starten

#### 2. Import data

##### 2.1 Motorways

`cd A2_GRASS_GIS\data`

`v.import motorways.shp`

##### 2.2 Administrative Districts of Baden-Württemberg

`v.in.ogr input=gadm28_adm2_germany.shp where="ID_1 =  1  AND  ENGTYPE_2 = 'District'" location=gadm`

`v.proj location=gadm mapset=PERMANENT input=gadm28_adm2_germany`

##### 2.3 Global Human Settlement Layer

Entfällt

#### 3. Calculate the total population of the districts

##### 3.1 Set the region

`g.region -p raster=GHS_POP_E2015_GLOBE_R2019A_54009_250_V1_0_18_3@PERMANENT vector=gadm28_adm2_germany@PERMANENT res=250`

##### 3.2 Rasterize the districts

`v.to.rast input=gadm28_adm2_germany@PERMANENT output=bw_raster use=attr attribute_column=OBJECTID`

##### 3.3 Calculate the population of each district

`r.stats.zonal base=bw_raster@PERMANENT cover=GHS_POP_E2015_GLOBE_R2019A_54009_250_V1_0_18_3@PERMANENT method=sum output=bw_raster_sum`

##### 3.4 Evaluate the population estimate

| Kreis  | Global Human Settlement Layer  |  offizielle Daten | Unterschied berechneter Wert/offiziele Daten  |
|---|---|---|---|
| Stuttgart  | N/A  | 635.872  | N/A  |
| Rhein-Neckar-Kreis  | 536.017,7  | 548.139  | -12.121,3 (-2,2%)  |
| Ludwigsburg  | 522.075,22  | 545.151  | -23.075,78 (-4,2%)  |
| Esslingen  | N/A  | 534.501  | N/A  |
| Karlsruhe (Land) | 430.938,5  | 444.997  | -14.058,5 (-3,2%)  |
| Ortenaukreis  | 415.417,13  | 430.244  | -14.826,87 (-3,4%)  |
| Rems-Murr-Kreis  | 408.340,66  | 426.635  | -18.294,34 (-4,3%)  |
| Böblingen  | 368.348,7  | 392.830  | -24.481,3 (-6.2%)  |
| Heilbronn (Land) | *  | 344.143  | *  |
| Ostalbkreis  | 306.513,66  | 314.108  | -7.594,34 (-2,4%)  |
| Karlsruhe (Stadt) | 301.348,03  | 312.305  | -10.956,97 (-3,5%)  |
| Mannheim  | 290.400,88  | 309.090  | -18.689,12 (-6,0%)  |
| Reutlingen  | 274.511,28  | 286.580  | -12.068,72 (-4,2%)  |
| Konstanz  | 268.676,1  | 286.016  | -17.339,9 (-6,1%)  |
| Ravensburg  | 272.951,03  | 285.285  | -12.333,97 (-4,3%)  |
| Breisgau-Hochschwarzwald  | N/A  | 263.346  | N/A  |
| Göppingen  | 246.213,02  | 257.716  | -11.502,98 (-4,5%)  |
| Rastatt  | 225.214,84  | 231.680  | -6.465,16 (-2,8%)  |
| Freiburg im Breisgau  | N/A  | 230.219  | N/A  |
| Lörrach  | 239.561,53  | 228.823  | +10.738,53 (+4,7%)  |
| Tübingen  | 216.754,4  | 227.484  | -10.729,6 (-4,7%)  |
| Bodenseekreis  | 201.773,8  | 217.570  | -15.796,2 (-7,3%)  |
| Schwarzwald-Bar-Kreis  | 203.981,61  | 212.616  | -8.634,39 (-4,1%)  |
| Biberach  | 191.369,67  | 200.574  | -9.204,33 (-4,6%)  |
| Enzkreis  | N/A  | 199.245  | N/A  |
| Alb-Donau-Kreis  | 189.201,75  | 196.786  | -7.584,25 (-3,9%)  |
| Schwäbisch Hall  | 188.828,72  | 196.521  | -7.692,28 (-3,9%)  |
| Zollernalbkreis  | 184.673,84  | 189.235  | -4.561,16 (-2,4%)  |
| Waldshut  | 172.994,9  | 170.954  | +2040,9 (+1,2%)  |
| Emmedingen  | N/A  | 165.788  | N/A  |
| Heidelberg  | 154.587,55  | 159.975  | -5.387,45 (-3,4%)  |
| Calw  | 148.887,73  | 158.732  | -9.844,27 (-6,2%)  |
| Neckar-Odenwald-Kreis  | 142.012,77  | 143.614  | -1.601,23 (-1,1%)  |
| Tuttlingen  | 133.317,34  | 140.575  | -7.257,66 (-5,2%)  |
| Rottweil  | 135.648,3  | 139.732  | -4.083,7 (-2,9%)  |
| Heidenheim  | 125.850,03  | 132.791  | -6.940,97 (-5,2%)  |
| Main-Tauber-Kreis  | 129.505,12  | 132.567  | -3.061,88 (-2,3%)  |
| Sigmaringen  | 126.647,09  | 130.960  | -4.312,91 (-3,3%)  |
| Ulm  | 118.469,7  | 126.164  | -7.694 (-6,1%)  |
| Heilbronn (Stadt)  | *  | 126.164  | *  |
| Pforzheim  | N/A  | 125.873  | N/A  |
| Freudenstadt  | 113.974  | 116.053  | -2.079 (-1,8%)  |
| Hohenlohekreis  | 107.711,7  | 112.451  | -4.739,3 (-4,2%)  |
| Baden-Baden  | 51.919,09  | 55.040  | -3.120,91 (-5,7%)  |

*Land- und Stadtkreise Heilbronn werden als ein einzelner Kreis mit 443.829,06 Einwohnern aufgeführt. Die offiziellen Daten für diese Kreise summiert ergeben eine Einwohnerzahl von 470.307. Daraus ergibt sich eine Differenz von -26.477,94 (-5,6%).

*Datenquelle*: Statista (2020): Einwohnerzahl der Land- und Stadtkreise in Baden-Württemberg 2019 (https://de.statista.com/statistik/daten/studie/1071004/umfrage/einwohnerzahl-der-kreise-in-baden-wuerttemberg/)

*Auswertung*: Die aus dem Global Human Settlement Layer berechneten Werte weisen einen maximalen Fehler von 7,3% (Kreis Bodensee) auf; die minimale Abweichung beträgt 1,1% (Neckar-Odenwald-Kreis). Somit können die Werte als relativ genau betrachtet werden, was allerdings stark von der Fragestellung abhängt, für welche sie Verwendung finden sollen. Zudem fällt auf, dass die Angaben meist niedriger als die offiziellen Daten (Ausnahmen: Kreis Waldshut und Kreis Lörrach) sind.
Da es sich um berrechnete Werte handelt, besitzen sie Nachkommastellen, die jedoch in Anbetracht der Tatsache, dass es sich bei dem Untersuchungsgegenstand um Einwohnerzahlen handelt, unlogisch erscheinen.

#### 4. Calculate total population living within 1km of motorways

- set region to motorways: `g.region -p vector=motorways@PERMANENT res=250`
- get 1km motorways buffer: `v.buffer input=motorways@PERMANENT output=motorways_1km distance=1000`
- rasterize buffer: `v.to.rast input=motorways_1km@PERMANENT output=motorways_rasterized_1km use=v`
- `r.stats.zonal base=motorways_rasterized_1km@PERMANENT cover=GHS_POP_E2015_GLOBE_R2019A_54009_250_V1_0_18_3@PERMANENT method=sum output=districts_bw_pop_motorways1km_sum`
- `r.stats input=districts_bw_pop_motorways1km_sum@PERMANENT` Ergebnis: 299503.5625 Personen leben im Bufferbereich