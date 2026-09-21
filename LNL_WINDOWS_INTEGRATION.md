# Windows Lunar Lake integration

The adapter accepts the experimental Windows `lnl` target only when the
provider manifest, installed `omni_xpu_kernel` wheel and core AOT marker agree.
A generic XPU discovery result does not establish LNL support.

The local component boundary covers INT8 ConvRot dispatch, Kitchen provider
selection and standalone CuTe attention shapes. Qwen Image 2.1 attention uses
PyTorch SDPA when its shape is outside the current CuTe contract. AIMDO remains
opt-in until its Windows allocator lifecycle has a target-local receipt.

Set `OMNI_IMAGE_XPU_TARGET=lnl` when testing provider discovery. A provider
that omits `lnl`, or a kernel wheel whose target identity differs, is rejected
before it can replace the canonical package.
