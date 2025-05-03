# Galaxy Morphology Analysis using Sersic Profile Fitting

![Whirlpool Galaxy Fitting Result](figs/whirlpool_final.png)

This repo contains an observational astrophysics project on galaxy classification using the Planewave CDK20 telescope and Sersic profile fitting with GalFit.

---

## 🧪 Methodology

This project investigates the morphology of three galaxies using observational data from the HPP (Planewave CDK20) telescope. The workflow spans from raw data reduction to 2D profile fitting using GalFit, allowing structural classification through Sersic profile decomposition.

### 🔭 Observations
- Targets: **M81 (Bode Galaxy)**, **M51 (Whirlpool Galaxy)**, **M49 (elliptical galaxy)**
- Filter: **Johnson R-band**
- Integration time: **20 minutes per galaxy**
- Reference stars for photometric calibration:
  - M81: HD 85-458
  - M51: TYC 3463-58-1
  - M49: Denebola (HR 4534)

### ⚙️ Data Reduction
- **Dark Subtraction**: Remove camera electronic noise using median dark frames
- **Flat Fielding**: Correct uneven illumination with twilight flats
- **Cosmic Ray Rejection**: `astroscrappy` using L.A.Cosmic algorithm
- **Background Subtraction**: Mean background removal for each science frame
- **Astrometric Calibration**: Using [astrometry.net](http://astrometry.net)
- **Stacking**: Aligning and averaging 20 exposures per galaxy via `astroalign`
- **Photometric Calibration**: Using standard stars to derive a magnitude zeropoint

### 🌀 Profile Fitting with GalFit
GalFit fits 2D **Sérsic profiles** to the reduced galaxy images:

\[
\Sigma(r) = \Sigma_e \exp\left\{ -\kappa \left[ \left( \frac{r}{r_e} \right)^{1/n} - 1 \right] \right\}
\]

- \( \Sigma_e \): surface brightness at effective radius \( r_e \)
- \( n \): Sérsic index (morphology proxy)
  - \( n \sim 1 \): exponential disk (spirals)
  - \( n \sim 4 \): de Vaucouleurs profile (ellipticals)

### 📊 Results Summary
- **M51 (Whirlpool)**: Modeled with 4 components; spiral arms and bulge well captured
- **M81 (Bode)**: 2 components; spiral arms partially unresolved due to core dominance
- **M49**: 3 components; expected elliptical profile not fully recovered (fitted indices too low)

### 📁 Output
Each galaxy has:
- Reduced FITS science image
- GalFit `.feedme` config and output
- Plots: input, model, residual
- Parameter tables: magnitude, effective radius, Sérsic index

---

## 📁 Structure
- `notebooks/`: Image processing, stacking, PSF creation
- `galfit/`: Feedme configs + model results
- `data/`: Raw FITS images + PSFs
- `figs/`: Final output images and plots
- `extras/`: GALFIT example/reference material
- `report/`: Report explaining the experiment

---

## 🛠 Tools
Python (Astroalign, AstroScrappy), GalFit, Astrometry.net, Jupyter

---

## 📜 License
MIT — see `LICENSE`.