# Log Timeline Studio

Load text or JSON-line logs into a searchable Windows timeline.

[![Build and verify](https://github.com/netcodermike/log-timeline-studio/actions/workflows/verify.yml/badge.svg)](https://github.com/netcodermike/log-timeline-studio/actions/workflows/verify.yml)

**Language:** C# · **Platform:** Windows desktop · **App type:** Windows searchable log timeline

First-release learning implementation, with explicit scope below. This is one independently runnable app, not a placeholder in a combined repository.

## Features

- JSON/plain-text rows
- Timestamp ordering
- Severity and text filters
- 100,000-line bounded import

## Requirements

.NET 10 SDK/Windows Desktop runtime. WPF runs only on Windows. No NuGet packages.

## Quick start

```sh
git clone https://github.com/netcodermike/log-timeline-studio.git
cd log-timeline-studio
dotnet run
```

Commands run from the repository root. Lines marked for a particular operating system apply only there. Language tools are prerequisites, not installed by the app. Close desktop windows normally; terminal/server apps stop with Ctrl+C unless their usage notes say otherwise.

## Example workflow

Enter a log file path, Load log, filter ERROR, and search a known message. Mix dated and undated rows and inspect their ordering.

## Architecture, configuration, and data

Program.cs parses each row into line/time/level/message. JSON recognizes timestamp, level, message; malformed JSON falls back to text. Plain text takes the first token as a candidate timestamp and detects common level words. WPF displays a read-only DataGrid ordered by timestamp with undated rows last. Files are capped at 10 MiB and 100,000 lines. Self-tests cover JSON, plain text, ordering, and missing timestamps.

## Verification

Build with the quick-start command where needed, then run:

```sh
dotnet run -- --self-test
```

Manual acceptance: Enter a log file path, Load log, filter ERROR, and search a known message. Mix dated and undated rows and inspect their ordering. Also test malformed inputs and an unwritable output destination.

See [validation record](docs/VALIDATION.md) for observed checks and their limits. CI results verify only what the workflow runs; they do not establish native GUI correctness or production readiness.

## Limitations and next steps

No tailing, regex queries, timezone inference, multiline stack-trace grouping, export, or editing. Parsing uses invariant date interpretation; undated rows remain unsequenced. Files are loaded into memory and UI filtering is synchronous. Filtering recognizes only the listed levels.

## Troubleshooting

Use the exact platform/toolchain above. Preserve originals and use synthetic fixtures first. Errors are displayed in the UI or stderr. A headless machine can run the model tests but cannot verify native GUI/audio behavior. Output paths are chosen explicitly; keep backups of important data.

## Source map

- `App.csproj`
- `Program.cs`

## Development and license

Read [contributing](CONTRIBUTING.md) before changing the app, and [security/privacy](SECURITY.md) before supplying private data. Use synthetic fixtures for tests. No telemetry, paid API key, or account is required by the app itself. Dependencies, when present, are stated in Requirements.

[MIT license](LICENSE), copyright 2026 netcodermike.
