<h1 align="center">🔴 Finding Jezero on Earth</h1>
<h4 align="center">Where on Earth looks most like Jezero crater, the Mars landing site of NASA's Perseverance rover? · NASA Space Apps Challenge 2026, Paris </h4>

<p align="center">
  <a href="https://proteus2-jezero-finder-app.streamlit.app/"><b>▶ Try the live app</b></a> ·
  <a href="https://github.com/thiyapapuge/planetary-analog-finder"><b>Main code repository</b></a>
</p>

<p align="center">
  <img width="1011" height="518" alt="image" src="https://github.com/user-attachments/assets/75cae690-e034-464f-a9ee-8c2dbe72c692" />
  <br><sub><em>The top 100 candidate sites worldwide</em></sub>
</p>

> ℹ️ **This repository is a showcase.** The source code lives in the team's main repository, [thiyapapuge/planetary-analog-finder](https://github.com/thiyapapuge/planetary-analog-finder), which is the one deployed online. Please open issues and pull requests there.

---

## 🎯 The challenge

> *"Identify Earth Locations that Analog the Permanent Moon Base Locations and Mars."*

We chose to go deep on **one real mission site** rather than cover everything superficially: **Jezero crater**, an ancient lake on Mars where Perseverance has been measuring the ground since 2021. That gives us real reference values for what we are looking for.

Missions on Mars tell us **what to look for**. Earth-observing satellites tell us **where to find it**.

## 🛰️ How it works

A transparent, rule-based model in three steps, run on the whole planet in **Google Earth Engine**:

| Step | Question | Data | Land left |
|---|---|---|---|
| 1 · Climate | Is it cold, dry and lifeless like Mars? Large day–night swing, cold, no vegetation, hyper-arid | NASA MODIS, TerraClimate | 138 M km² → 4.4 M km² (3.2 %) |
| 2 · Terrain | Does it look like a crater floor? Wide flat floor, moderate relief around, lower than its surroundings | MERIT DEM 90 m (based on NASA SRTM) | → 1.4 M km² (1.0 %) |
| 3 · Rock | Are the rocks like Jezero's floor? Dark, iron- and magnesium-rich (mafic) rock | NASA/METI ASTER, 100 m | → 0.73 M km² (0.5 %) |

The result is **4,553 candidate sites** on a 0.25° grid (≈ 28 km cells).

**Final score** = climate<sup>0.35</sup> × terrain<sup>0.30</sup> × rock<sup>0.35</sup>

Because the scores are multiplied, a site has to be good at everything. Thresholds come from Perseverance measurements and UN aridity classes. The weights are team choices, and the app shows them all.

**Why no machine learning?** There are only a handful of recognised Mars analogs on Earth — far too few to train a model. A rule-based score can be read, checked and explained.

## 📈 Key results

- ✅ **Validation** — without being told, the model finds the **Qaidam basin** (China), a known Mars analog. It also rejects negative tests: the Amazon, France and the Rub' al Khali sand sea.
- 🆕 **New sites** — 87 of the top 100 are far from any of 8 well-known analogs (Atacama, Utah MDRS, Death Valley, Qaidam, Haughton, Iceland, Hawaii, Rio Tinto).
- 🧭 **Field check** — of the top 100, 10 are removed (disputed territory) and 6 flagged (protected areas). That leaves 84 sites with no restriction, and **29 usable right away** (under 6 h from a city).
- 🎯 **Our pick: site #4, a dry salt basin in the Puna, Argentina.** A 62/100 match to Jezero, the best of the new sites. It tells the same story as Jezero: a lake filled a closed basin, dried out and left salts behind. It ranks 1st for geology, 2nd for astrobiology, and sits 5.5 h from a city.
- ⚠️ **Where the analogy breaks** — a 34 K day–night swing versus ≈ 87 K at Jezero, a warmer average temperature, and Earth's gravity, air and magnetic field. The app shows these limits for every site.

<p align="center">
  <img width="1517" height="732" alt="image" src="https://github.com/user-attachments/assets/bdc4a381-97b0-4807-ad5a-69320ae8c51b" />
  <img width="1485" height="621" alt="image" src="https://github.com/user-attachments/assets/5cb5a61c-75ca-49b9-a509-aa6f601983ca" />
  <br><sub><em>Left: site #4, Puna, Argentina (Copernicus Sentinel-2). Right: Jezero crater from orbit (NASA/JPL-Caltech/MSSS/JHU-APL, PIA23239).</em></sub>
</p>

## 🖥️ The app

| Page | What you can do |
|---|---|
| **1 · The model** | Big world map or 3D globe, with a before/after slider that runs the model step by step. Click any site for its sheet. Includes the validation tests. |
| **2 · Top 100 sites** | Field-check slider (disputed territories, protected areas, travel time) and access charts. |
| **3 · Compare sites** | Best site for 6 experiments: landing, rover driving, instruments & geology, astrobiology, thermal environment, crewed-mission simulation. Includes a field filter, a heatmap and a radar chart. |
| **4 · Jezero vs new sites** | Rotating Mars globe (click Jezero to see it from orbit), a sourced Jezero fact sheet, and a side-by-side comparison of any two sites with their Jezero match. |

<p align="center">
  <img width="1535" height="709" alt="image" src="https://github.com/user-attachments/assets/a89e5d7a-18a2-4074-9c91-45ef34c33e90" />
  <br><sub><em>Which site for which experiment</em></sub>
</p>

## 📊 Data

| Use | Dataset |
|---|---|
| Climate | NASA **MODIS** (land surface temperature, NDVI), TerraClimate (aridity) |
| Terrain | MERIT DEM 90 m (built notably on NASA **SRTM**) |
| Rock | NASA/METI **ASTER** GED (mafic index, bands 12/13) |
| Water mask | JRC Global Surface Water |
| Field check | Oxford accessibility to cities (2015), WDPA protected areas (UNEP-WCMC), US State Dept. LSIB borders |
| Visual check | Copernicus Sentinel-2 |
| Mars | Perseverance **MEDA** results, **NASA Mars Trek** (Viking mosaic), NASA image **PIA23239**, NASA Mars fact sheet, published Jezero papers |

## 🛠️ Tech stack

- **Google Earth Engine** (JavaScript) for the global computation, exported as CSV and GeoTIFF
- **Python**: Streamlit, pandas, NumPy, Plotly
- **Folium / Leaflet** for maps (Esri basemaps), **three.js** for the Earth and Mars 3D globes
- Hosted on **Streamlit Community Cloud**, deployed from GitHub

## 👥 Team Proteus 2

| Member | Role |
|---|---|
| Lilian JAOUEN | Google Earth Engine processing |
| Thiya PAPUGE | Web app and interface |
| Jaime SOUSA | Model design and pitch |
| Emma TROTIGNON | *(to fill in)* |

**My contribution:** *(to fill in — 2–3 lines on what you did yourself)*

## 🚀 Next steps

- Add NASA **EMIT** mineral data (clays, carbonates, salts)
- Test how sensitive the ranking is to the weights
- Have geologists review the top sites, then field reconnaissance
- Rerun the same method with a **lunar** profile

## 🤖 Use of AI

AI tools helped write code and text. The team chose the method, criteria, thresholds and weights, ran the analyses and checked the results. This is declared in the app, as required by the Space Apps rules.

---

<sub>Built for the NASA Space Apps Challenge 2026. This is not an official NASA project, and NASA does not endorse it. Satellite data © their respective providers.</sub>

<p align="center"><a href="https://github.com/Jiboti">⬅️ Back to profile</a></p>
