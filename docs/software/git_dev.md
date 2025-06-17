# Gitを使用した開発

### コミットメッセージのルール

[Angular JSのガイドライン](https://github.com/angular/angular.js/blob/master/DEVELOPERS.md#-git-commit-guidelines)を参考。（たぶんMITライセンスのはず）

```
[種別]: [概要]
===空行===
[本文]
===空行===
[フッター]
```

[種別]と[概要]は必須で、それ以降は任意。

**例**

```
feat: なにかのUIを追加

* ふがふがページを追加
* ほげほげロジックを追加

Closes #1
```

**種別**

* feat: 機能の追加
* fix: バグの修正
* ドキュメントの追加・更新
* style: コードに影響を及ぼさないスタイル修正（コードフォーマット）
* refactor: feat/fix以外のコードの修正
* perf: パフォーマンスの改善
* test: テストケースの追加・修正
* chore: その他（ビルド設定などの変更）
* revert: コミットのリバーと
* bump: releaseブランチでのバージョンアップ作業

