# Serine genes in pancreatic cancer: primary tumor vs. liver metastasis

This is a small project using public data. I looked at three genes that help cells make serine (PHGDH, PSAT1 and PSPH) and asked are they switched on differently in a patient's main pancreatic tumor compared with their own liver metastasis?

## Why I did this
In 2026 a Nature paper (Ganguly et al.) reported that liver cells (hepatocytes) can supply serine to pancreatic cancer cells that have spread to the liver. That made me curious about what the serine genes look like in real patient samples. This project does not test the paper's claim. It is just a simple look at gene expression inspired by it.

## The data
- Dataset: GSE151580 from GEO. It is RNA-seq data from human pancreatic cancer.
- It comes from Yang et al., Genome Biology 2021.
- It has 33 samples from 14 patients: primary tumor, liver metastasis, and normal pancreas tissue next to the tumor.
- 13 patients have both a primary tumor and a liver metastasis, so I used those 13 pairs for the main comparison.
- I did not upload the raw count file. You can download it from the GEO page for GSE151580.

## What I did
1. Adjusted the raw counts so samples can be compared fairly (counts per million, then log2).
2. Compared each patient's primary tumor with their own liver metastasis, using a paired Wilcoxon test.
3. Because I tested 3 genes, I corrected the p-values (Bonferroni).
4. For the 6 patients who also have normal pancreas samples, I drew a simple plot of normal, primary and liver metastasis. I did not run a test on this, because 6 is too few.

## What I found
| Gene | Higher in liver in | Median change (log2) | p | Corrected p |
| PHGDH | 6 of 13 patients | -0.08 | 0.636 | 1.000 |
| PSAT1 | 8 of 13 patients | +1.29 | 0.048 | 0.144 |
| PSPH | 2 of 13 patients | -0.22 | 0.013 | 0.040 |

- **PSPH** was lower in the liver metastasis than in the primary tumor in 11 of 13 patients (corrected p = 0.04). The drop was small.
- **PSAT1 and PHGDH** did not show a difference that holds up after correction.
- In the 6 patients with normal pancreas samples (just a picture, not tested), PSPH looked higher in the tumor than in normal pancreas and lower again in the liver metastasis. PHGDH and PSAT1 looked lower in the tumor than in normal pancreas.

Files: `serine_paired_plot.png`, `serine_normal_trio_plot.png`, `serine_results.csv`

## What this project cannot tell you
- It is small.With 13 pairs, only big differences show up and one patient can push a p-value across 0.05.
- Liver cells are mixed into the metastasis samples.** Some of the change may come from normal liver tissue and not from the tumor itself. The normal samples here are pancreas, so they cannot fix this.
- The patients are a special group. They had surgery for a small number of liver metastases, so the results may not apply to most metastatic pancreatic cancer patients.
- It only measures gene activity.It does not show serine levels, or whether tumor cells take serine from the liver.
- It is exploratory. I picked 3 genes in advance, and this is not a confirmed finding.
- Literature check: I looked through the papers linked to this dataset and found no serine gene analysis. I did not do a full literature search, so I can't say this has never been done.

## Tools
Python, pandas, NumPy, SciPy, statsmodels, matplotlib (in Google Colab)

## About me
Syeda Masooma.  GitHub: masooma-bioinfo
