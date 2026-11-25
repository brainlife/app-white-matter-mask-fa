<!-- brainlife-app:begin (generated from the App manifest; edit the manifest, not this block) -->

**Creates a binary white matter mask in DWI space by thresholding a fractional anisotropy (FA) map with FSL fslmaths.**

Thresholds the FA image at thr (default 0.15) and binarizes it into mask.nii.gz. Use it for a quick DWI-space white matter mask, e.g. for tractography seeding or masking; the FA threshold also keeps some non-white-matter voxels with high anisotropy and drops crossing-fiber regions with low FA.

Run it on brainlife.io: [https://doi.org/10.25663/brainlife.app.719](https://doi.org/10.25663/brainlife.app.719)

| Input | Datatype | Required | Description |
|---|---|---|---|
| `fa` | `neuro/tensor` | yes | Tensor output; only the FA map is used. |

| Output | Datatype | Description |
|---|---|---|
| `mask` | `neuro/mask` | Binary mask (mask.nii.gz) of voxels with FA above the threshold, in DWI space. |

| Parameter | Type | Default | Description |
|---|---|---|---|
| `thr` | number | `0.15` | FA value below which voxels are excluded from the white matter mask (fslmaths -thr). |

Runtime: container `brainlife/fsl:6.0.4-patched2`; 4 CPUs; 0.5 h walltime.

<!-- brainlife-app:end -->

# -app-white-matter-mask-fa