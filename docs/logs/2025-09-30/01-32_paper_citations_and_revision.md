# Paper Citations and Major Revision Session
**Date:** 2025-09-30 01:32
**Session Duration:** ~2 hours

## Overview
Major revision session focusing on adding citations, restructuring narrative, fixing figure references, and rewriting abstract to emphasize compression achievements.

## Citations Added

### Introduction
1. **Naeger et al. 2024** - TEMPO mission (AMS conference)
2. **Thies & Bendix 2011** - Satellite remote sensing fundamentals
3. **Wielicki et al. 1996** - CERES mission
4. **Yang et al. 2013** - Role of satellite remote sensing in climate
5. **Weng 2009** - Thermal infrared remote sensing
6. **Goetz et al. 1985** - Imaging spectrometry for Earth remote sensing
7. **Lary et al. 2016** - Machine learning in geosciences
8. **Bioucas-Dias et al. 2013** - Hyperspectral remote sensing challenges
9. **Rodgers 2000** - Inverse methods for atmospheric sounding
10. **Chance et al. 2013** - TEMPO mission (SPIE)

### Methodology
- Re-cited **Zoogman et al. 2017** in Data Preparation section

## Major Structural Changes

### 1. Introduction Reframing
**Before:** Led with retrieval complexity problem
**After:** Leads with data storage/transmission challenges
- Hyperspectral data generates massive volumes
- Full spectrum per pixel × hourly observations = terabytes daily
- Emphasizes spatial + spectral correlations enable compression
- Retrieval complexity now secondary motivation

### 2. Narrative Rebalancing
**Key message:** Compression is the win, atmospheric extraction is bonus
- Proudly emphasize: 514× compression with 1-2 orders of magnitude error
- Success stories: Cloud (R²=0.93) and O₃ (R²=0.81)
- Honest about challenges: NO₂ and HCHO are inherently difficult
- NO₂ shows noise-like structure (visible in Figure 1) lacking spatial coherence

### 3. Semi-Linear Encoding Finding
Scattered throughout intro/results/conclusion:
- VAE encodes atmospheric info in semi-linear manner
- Linear probes extract some information
- Nonlinear MLP probes substantially outperform (e.g., O₃: 0.545→0.811)
- Products not directly accessible through linear combinations

### 4. Supervised VAE Finding
Emphasized throughout:
- Explicit L2 supervision during training provides minimal improvement
- Reveals fundamental encoding challenges, not lack of supervision
- NO₂ barely improves even with supervision (visible in training curves)
- Cloud/O₃/HCHO show overfitting in later training stages

## Results Section Improvements

### Reconstruction Quality
- Integrated discussion of both figures (quantitative + spatial)
- Note: errors low across spectrum except shortest wavelengths (290-310nm)
- Removed unsupported claims about "complex cloud structures"

### Component Extraction
- Added proper discussion of O₃ success (was under-discussed)
- Connected spatial patterns in Figure 1 to extraction performance
- NO₂ challenges: low SNR + noise-like structure + lacks spatial coherence
- Fixed all R² values to match actual data files

### Supervised Section
- Added motivation paragraph at end of unsupervised section
- Proper discussion of Figure (supervised training dynamics)
- Notes: L2 losses improve after reconstruction plateaus (~40k steps)
- Overfitting visible for cloud/O₃/HCHO
- NO₂ shows minimal improvement throughout training

## Figure and Caption Improvements

### Figure References
- Removed non-existent Table references
- Fixed all figure cross-references
- Changed → symbols to proper LaTeX $\rightarrow$

### Caption Cleanup
Removed useless details like:
- "Both axes use log scale for y-axis to visualize the full dynamic range"
- "x-axis shows training steps from 500 to 220,000"
- Technical implementation details

Added scientific content:
- Actual observations from figures
- Interpretation of patterns
- Connection to main findings

## Abstract Rewrite

**New structure:**
1. **Problem:** Terabytes of hyperspectral data daily
2. **Solution:** 514× compression with minimal error
3. **Impact:** Enables efficient archival and sharing
4. **Bonus finding:** Atmospheric products extractable (with varying success)
5. **Key insights:** Semi-linear encoding, supervision doesn't help much
6. **Conclusion:** Addresses critical bottleneck for Earth observation

**Tone shift:** From "we extract atmospheric products" to "we compress data massively while retaining some atmospheric signals"

## Related Work Section

### Neural Image Compression
- Added definitive statement: hyperspectral data ideal for neural compression
- Reasons: spectral correlations + spatial correlations = natural redundancy
- Neighboring wavelengths smooth, adjacent pixels similar atmospheric conditions

### VAEs and Disentangled Representations
- Removed uncited claim about VAEs discovering physical representations
- Softened to: "disentanglement could be particularly valuable"

## Methodology Section Cleanup

### Data Preparation
- Moved L2 Product Alignment subsection before VAE Architecture
- Logical flow: data → preprocessing → architecture → training
- Removed "swath" jargon
- Condensed normalization description, pointed to appendix

### Architecture
- Removed "(double-z parameterization)" jargon
- Verified log-variance clamping values [-30, 20] against code

### Training
- Condensed training details, moved minor ones to appendix reference
- Kept essential: loss formulation, optimizer, batch size, single GPU

### Probing
- Removed epoch counts, early stopping details
- Kept architecture descriptions

## Data Corrections

All R² values verified against actual results:
- **Unsupervised Linear:** NO₂=0.122, O₃=0.545, HCHO=0.474, Cloud=0.785
- **Unsupervised MLP:** NO₂=0.203, O₃=0.811, HCHO=0.511, Cloud=0.930
- **Supervised MLP:** NO₂=0.227, O₃=0.815, HCHO=0.500, Cloud=0.922

## Copyright Notice
Commented out AAAI copyright text in aaai2026.sty (lines 47-49)

## Key Themes Established

1. **Compression as primary contribution** - not retrieval
2. **Honest about limitations** - NO₂/HCHO are hard (and that's okay)
3. **Celebrate successes** - cloud and O₃ work well
4. **Novel findings** - semi-linear encoding, supervision doesn't help
5. **Scientific rigor** - all claims supported by data

## Files Modified
- `/paper/main.tex` - extensive revisions throughout
- `/paper/aaai2026.bib` - 10+ new citations
- `/paper/aaai2026.sty` - copyright notice commented out

## Next Steps (for future sessions)
- Verify all citation details are complete
- Check if more citations needed in related work
- Consider adding citations for semi-linear encoding claim if exists
- Final pass on contributions list
- Polish conclusion future work section