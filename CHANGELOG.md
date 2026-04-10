# Changelog

## [1.0.6] - 2026-04-09

### Fixed

- **Orphaned tool_use/tool_result after compression** — Compression ranges that touched part of an assistant→toolResult group could leave orphaned `tool_use` or `tool_result` blocks, causing Anthropic API 400 errors (`unexpected tool_use_id found in tool_result blocks`). The backward and forward expansion logic now correctly skips PI-internal passthrough roles (`compaction`, `branch_summary`, `custom_message`) when scanning for paired messages, ensuring atomic removal of complete tool groups.
- **Content mutation across context events** — `applyPruning` now deep-clones message content instead of shallow-copying, preventing injected `dcp-id` blocks from accumulating on shared message objects across successive context events.

### Added

- **Post-compression repair function** — `repairOrphanedToolPairs` runs after all compression blocks are applied as a safety net. It removes orphaned `toolResult`/`bashExecution` messages whose `toolCallId` has no matching `toolCall` in any assistant message, and strips orphaned `toolCall` blocks from assistant messages whose results no longer exist.
- **New test cases** — Tests 5–9 covering passthrough role handling (backward and forward expansion), content mutation isolation, multi-block orphan repair, and direct orphan cleanup.

## [1.0.5] - 2026-04-06

### Fixed

- Prevent orphaned tool_use blocks from compression and harden autocomplete.

## [1.0.4] - 2026-04-05

### Fixed

- Tool crash on compression.

## [1.0.3] - 2026-04-04

### Fixed

- Various errors and issues.

## [1.0.2] - 2026-04-03

### Changed

- Added pi package details to package.json.

## [1.0.1] - 2026-04-02

### Added

- Initial release.
