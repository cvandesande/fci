# fci

This repository owns the shared packaged FCI source consumed by both the
OpenWrt `ask-fci` kernel package and the `libfci` userspace library package.

The source boundary is intentionally shared and lives under `fci-9.00.12/`.
OpenWrt fetches one pinned git revision of this repository, unpacks it into
`build_dir`, and then builds:
- `ask-fci` from `fci-9.00.12/`
- `libfci` from `fci-9.00.12/lib`

`openwrt/package/kernel/ask-fci/` and `openwrt/package/libs/libfci/` remain
responsible for:
- package metadata and dependency declarations
- OpenWrt init/service integration under `ask-fci/files/`
- any future OpenWrt-local patch queues, if they are added intentionally

For reproducible packaging, OpenWrt should pin an exact commit or tag from this
repository through `PKG_SOURCE_VERSION` and verify the generated source archive
with `PKG_MIRROR_HASH`. Tags should identify packageable source states; commits
referenced by released packages must remain immutable.
