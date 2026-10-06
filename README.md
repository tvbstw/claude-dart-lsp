# claude-dart-lsp

A [Claude Code](https://code.claude.com/docs) plugin that connects Claude Code to the Dart analysis server (`dart language-server`, shipped with the Dart SDK and the Flutter SDK). With it, Claude Code can use LSP operations such as find references, go to definition, and go to implementation on `.dart` files, instead of relying on text search.

The plugin contains no code: it is a manifest plus an `.lsp.json` that tells Claude Code to start `dart language-server` for `.dart` files.

## Requirements

- Claude Code
- `dart` on the `PATH` of the shell you start `claude` from. Installing the Flutter SDK is enough; check with `which dart`.

## Install

```bash
claude plugin marketplace add tvbstw/claude-dart-lsp
claude plugin install dart-lsp@claude-dart-lsp
```

This installs at user scope, so it applies to every Dart / Flutter project you open.

### Enable it for a whole team

Add this to the project's `.claude/settings.json` and commit it:

```json
{
  "extraKnownMarketplaces": {
    "claude-dart-lsp": {
      "source": { "source": "github", "repo": "tvbstw/claude-dart-lsp" }
    }
  },
  "enabledPlugins": {
    "dart-lsp@claude-dart-lsp": true
  }
}
```

This declares the marketplace and enables the plugin for the project, but as of Claude Code 2.1.290 it does not prompt teammates to install it: opening the project interactively showed no install prompt, and the marketplace did not appear in `/plugin`. Each teammate still needs to run the two install commands above once.

## Notes

- The analysis server only sees files that `analysis_options.yaml` does not exclude. If your project excludes `test/**`, find references will silently return nothing for tests.
- Run `flutter pub get` first; without a resolved `.dart_tool/package_config.json` the analysis server cannot resolve `package:` imports.

## 繁體中文說明

讓 Claude Code 透過 Dart SDK 內建的 Analysis Server 查 Dart 符號的引用、定義與實作。前提是 PATH 上要有 `dart`，裝了 Flutter SDK 就有。每人手動執行一次上方「Install」的兩行指令（裝在 user scope，所有 Dart／Flutter 專案都生效）；專案 settings 裡的宣告不會自動提示安裝。

## License

[MIT](LICENSE)
