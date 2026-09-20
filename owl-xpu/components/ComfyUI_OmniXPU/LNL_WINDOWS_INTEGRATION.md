# Windows Lunar Lake integration

The `dev` branch is the Windows/LNL integration line for the OWL provider
stack.  It does not make a generic XPU wheel claim target-specific coverage:
the provider manifest must contain `lnl`, the installed Omni wheel must report
`__xpu_target__ == "lnl"`, and the core AOT identity must also be `lnl`.

On the local Lunar Lake machine the validated route is:

- INT8 ConvRot dequant and fused feed-forward paths through `omni_xpu_kernel`;
- Kitchen XPU dispatch for the supported INT8/SVDQuant contracts;
- CUTE attention only for the standalone validated shapes; Qwen Image 2.1's
  unsupported shape continues through PyTorch SDPA;
- AIMDO remains opt-in because its Windows VBAR path did not show a stable
  end-to-end gain in the recorded experiments.

Set `OMNI_IMAGE_XPU_TARGET=lnl` when testing provider discovery.  A provider
that omits `lnl` is rejected before it can replace the canonical package.
