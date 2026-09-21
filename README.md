# ComfyUI_OmniXPU

Thin Intel XPU integration for upstream ComfyUI, with prestartup provider
selection, capability checks and focused call-site adapters.

Initial source: `intel/llm-scaler@38d9a3dbbfecd3a5293a8acd75efef54f9bb3719`,
`omni/ComfyUI-OmniXPU`. Runtime source and package identities are unchanged;
component tests are included with their paths adapted to this standalone layout.
Original attribution and the Apache-2.0 license are retained; this is not an Intel release.

## Install

Clone this public repository directly into ComfyUI's `custom_nodes` directory:

```bash
git clone https://github.com/shinosawabot/ComfyUI_OmniXPU.git /path/to/ComfyUI/custom_nodes/ComfyUI_OmniXPU
```

The node requires the matching `omni_xpu_kernel` wheel, official Kitchen/AIMDO
packages and compatible optional XPU provider wheels. Cloning this repository
does not install those native dependencies. Their source homes and initial
snapshots are recorded in [component-sources.json](component-sources.json).

`prestartup_script.py` owns provider selection; `runtime_bootstrap.py` validates
compatibility and canonical runtime identity. `adapters/` owns ComfyUI-specific
bridges, `fixes/` contains opt-in legacy fixes, and `nodes/` provides diagnostics.
Generic operators belong in Kitchen, native kernels in `omni_xpu_kernels`, and
allocator lifecycle in AIMDO. See [ARCHITECTURE.md](ARCHITECTURE.md).

Provider bootstrap retains its existing `auto`, `off` and `required` modes.
AIMDO requires the explicit DynamicVRAM and allocator-lifecycle prerequisites.
Detailed controls remain in [UPSTREAM_README.md](UPSTREAM_README.md).

## Development

```bash
python -m pytest tests
```

Tests need pytest and a compatible Torch installation. Real ComfyUI/XPU compile
integration tests require those external runtimes and may skip without them.
Repository initialization does not establish new workflow, image or device
acceptance. See [SOURCE_PROVENANCE.json](SOURCE_PROVENANCE.json) for source hashes.
