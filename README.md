<h1 align="center">White matter mask from FA</h1>

<p align="center">
  A binary white matter mask in DWI space from a thresholded fractional anisotropy (FA) map, with FSL.
</p>

<p align="center">
  <a href="https://github.com/brainlife/abcd-spec"><img src="https://img.shields.io/badge/ABCD_Spec-v1.1-green.svg" alt="ABCD Spec v1.1"></a>
  <a href="https://doi.org/10.25663/brainlife.app.719"><img src="https://img.shields.io/badge/Brainlife-brainlife.app.719-blue.svg" alt="Run on brainlife.io"></a>
  <a href="https://github.com/brainlife/app-white-matter-mask-fa/blob/main/LICENSE"><img src="https://img.shields.io/badge/License-MIT-lightgrey.svg" alt="MIT license"></a>
</p>

> 📍 **This branch, `1.0`, is the brainlife.io App Create white matter mask from FA** ([doi:10.25663/brainlife.app.719](https://doi.org/10.25663/brainlife.app.719)).

## 🧠 At a glance

<!-- brainlife-app:begin (generated from the App manifest; edit the manifest, not this block) -->

> **Creates a binary white matter mask in DWI space by thresholding a fractional anisotropy (FA) map with FSL fslmaths.**

Thresholds the FA image at thr (default 0.15) and binarizes it into mask.nii.gz. Use it for a quick DWI-space white matter mask, e.g. for tractography seeding or masking; the FA threshold also keeps some non-white-matter voxels with high anisotropy and drops crossing-fiber regions with low FA.

| | |
|---|---|
| 📥 **Inputs** | `neuro/tensor` |
| 📤 **Outputs** | `neuro/mask` |
| 🐳 **Container** | `brainlife/fsl:6.0.4-patched2` |
| ⚙️ **Resources** | 4 CPUs · 0.5 h walltime |
| 🔗 **Run it** | [doi.org/10.25663/brainlife.app.719](https://doi.org/10.25663/brainlife.app.719) |

#### 📥 Inputs

| Input | Datatype | Required | Description |
|---|---|---|---|
| `fa` | `neuro/tensor` | yes | Tensor output; only the FA map is used. |

#### 📤 Outputs

| Output | Datatype | Description |
|---|---|---|
| `mask` | `neuro/mask` | Binary mask (mask.nii.gz) of voxels with FA above the threshold, in DWI space. |

<details>
<summary><b>⚙️ Parameters</b> (1)</summary>

| Parameter | Type | Default | Description |
|---|---|---|---|
| `thr` | number | `0.15` | FA value below which voxels are excluded from the white matter mask (fslmaths -thr). |

</details>

<!-- brainlife-app:end -->

## 🚀 Running the App

### ☁️ On brainlife.io

Open the App at [doi.org/10.25663/brainlife.app.719](https://doi.org/10.25663/brainlife.app.719), choose a tensor dataset (`neuro/tensor`; only its FA map is used), set the threshold and press **Execute**. The App writes a `neuro/mask` dataset tagged `white_matter`, `brain` and `dwi` to your project.

The mask keeps every voxel with FA above `thr` (default 0.15; `fslmaths -thr`) and binarises the result (`fslmaths -bin`). It is a quick DWI-space white matter mask, for example for tractography seeding or masking. Because it is based on FA alone, it also keeps some non-white-matter voxels with high anisotropy and can drop crossing-fibre regions with low FA.

### 💻 Locally

You need [Singularity/Apptainer](https://apptainer.org/) and [`jq`](https://jqlang.github.io/jq/). The App runs in the `brainlife/fsl:6.0.4-patched2` container.

1. Clone this repository and check out the registered version (`git checkout 1.0`).
2. Create `config.json` with the path to the FA map and the threshold:

   ```json
   {
       "fa": "/input/tensor/fa.nii.gz",
       "thr": 0.15
   }
   ```

3. Run the App:

   ```bash
   ./main
   ```

## 📦 Outputs

```text
mask/
└── mask.nii.gz          binary white matter mask (FA > thr), in DWI space
raw/
└── fa_threshold.nii.gz  the thresholded FA map
```

## 🩺 Troubleshooting

- **`something went wrong. check derivatives and logs`**: `mask/mask.nii.gz` was not written. Check that the tensor input contains `fa.nii.gz`.

## 📚 Citing

> [!TIP]
> If you use this App in your work, please cite the App, the software it builds on and brainlife.io (below). GitHub's **Cite this repository** button gives the App citation in APA and BibTeX.

- Create white matter mask from FA. brainlife.io App. [doi:10.25663/brainlife.app.719](https://doi.org/10.25663/brainlife.app.719)
- Jenkinson et al. FSL. *NeuroImage* 62:782-790 (2012). [doi:10.1016/j.neuroimage.2011.09.015](https://doi.org/10.1016/j.neuroimage.2011.09.015)
- Hayashi S, Caron BA, Heinsfeld AS, et al. brainlife.io: a decentralized and open-source cloud platform to support neuroscience research. *Nature Methods* 21:809–813 (2024). [doi:10.1038/s41592-024-02237-2](https://doi.org/10.1038/s41592-024-02237-2)
- Avesani P, McPherson B, Hayashi S, et al. The open diffusion data derivatives, brain data upcycling via integrated publishing of derivatives and reproducible open cloud services. *Scientific Data* 6:69 (2019). [doi:10.1038/s41597-019-0073-y](https://doi.org/10.1038/s41597-019-0073-y)

## 👥 Authors

- Brad Caron

## 💰 Funding

[![Wellcome-226486/Z/22/Z](https://img.shields.io/badge/Wellcome-226486%2FZ%2F22%2FZ-purple.svg)](https://wellcome.org/)
[![NIH-NINDS-U24NS140384](https://img.shields.io/badge/NIH_NINDS-U24NS140384-green.svg)](https://reporter.nih.gov/project-details/11261037)
[![NIH-NINDS-UM1NS132207](https://img.shields.io/badge/NIH_NINDS-UM1NS132207-green.svg)](https://reporter.nih.gov/project-details/11411328)
[![NIH-NIBIB-R01EB029272](https://img.shields.io/badge/NIH_NIBIB-R01EB029272-green.svg)](https://reporter.nih.gov/project-details/10262925)
[![NIH-NIBIB-R01EB030896](https://img.shields.io/badge/NIH_NIBIB-R01EB030896-green.svg)](https://reporter.nih.gov/project-details/10428625)
[![NIH-NIMH-R01MH126699](https://img.shields.io/badge/NIH_NIMH-R01MH126699-green.svg)](https://reporter.nih.gov/project-details/10460628)
[![NIH-NIDCD-R01DC020088](https://img.shields.io/badge/NIH_NIDCD-R01DC020088-green.svg)](https://reporter.nih.gov/project-details/11140284)
[![NSF-BCS-1734853](https://img.shields.io/badge/NSF_BCS-1734853-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1734853)
[![NSF-BCS-2203524](https://img.shields.io/badge/NSF_BCS-2203524-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2203524)
[![NSF-IIS-1636893](https://img.shields.io/badge/NSF_IIS-1636893-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1636893)
[![NSF-OAC-2148729](https://img.shields.io/badge/NSF_OAC-2148729-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2148729)
[![NSF-IIS-1912270](https://img.shields.io/badge/NSF_IIS-1912270-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1912270)
[![NSF-IIS-2148700](https://img.shields.io/badge/NSF_IIS-2148700-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=2148700)
[![NSF-OAC-1916518](https://img.shields.io/badge/NSF_OAC-1916518-blue.svg)](https://www.nsf.gov/awardsearch/showAward?AWD_ID=1916518)

<sub>brainlife.io is publicly funded, and acknowledging that support helps keep it running. This App was developed with support from Wellcome, the U.S. National Institutes of Health (including the BRAIN Initiative BRAIN CONNECTS program: The Axonal Projectome EXchange, U24NS140384, and the Center for Mesoscale Connectomics, UM1NS132207) and the U.S. National Science Foundation.</sub>

## ⚖️ License

MIT. FSL is distributed under its own [license](https://fsl.fmrib.ox.ac.uk/fsl/fslwiki/Licence).
