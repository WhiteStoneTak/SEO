# seo（日本語版）

リポジトリにコミットできる立場でSEOをやるための手順。

SEOの文書のほとんどは、助言しかできない立場の人に向けて書かれている。ここではリポジトリを開いてテンプレートを直し、そのままデプロイできることを前提にする。前提が変わると、やる価値のある作業も、その順番も、結果の報告の仕方も変わる。

中身は文書・チェックリスト・テンプレート・エージェント用プレイブック。クローラもCLIもスコアリングエンジンも含まない。公開ツール（Search Console、Lighthouse、`curl`、[OpenSEO](https://github.com/every-app/open-seo)）だけで再現できる手順にしてある。

本文は英語。日本語市場に固有の話は [japanese-market.md](japanese-market.md) にまとめた。

## 5つのフェーズ

Phase 0で計測基盤を作る。ここが終わるまで何も直さない。ベースラインのない変更は、後から評価できない。Phase 1は現状の事実を集める。良し悪しの判断はしない。Phase 2で事実を順序のついた作業リストに変える。Phase 3で実装する。1施策1コミット。Phase 4で観測窓が閉じるのを待ち、結果を記録する。効かなかったものも書く。

Phase 2は意図的な停止点にしてある。値付けと順序のついた診断書は、それだけで完結した成果物になる。

## 文書一覧

**方法論**

| ファイル | 内容 |
| --- | --- |
| [01-principles](../docs/01-principles.md) | 5原則 |
| [02-scope-and-limits](../docs/02-scope-and-limits.md) | 対象範囲、対象外、約束しないこと |
| [03-phase0-baseline](../docs/03-phase0-baseline.md) | 計測基盤とベースラインの固定 |
| [04-phase1-technical-audit](../docs/04-phase1-technical-audit.md) | 技術診断の全チェック項目 |
| [05-phase1b-onpage-content](../docs/05-phase1b-onpage-content.md) | クエリとページの対応、title、内部リンク |
| [06-phase2-prioritization](../docs/06-phase2-prioritization.md) | 優先順位の式と、それを上書きする条件 |
| [07-phase3-implementation](../docs/07-phase3-implementation.md) | 1施策1コミットの運用 |
| [08-phase4-measurement](../docs/08-phase4-measurement.md) | 観測窓、事前閾値、交絡因子 |

**外部SEO会社が構造的にやれない部分**

| ファイル | 内容 |
| --- | --- |
| [09-data-layer](../docs/09-data-layer.md) | データ層を借りずに自前で持つ |
| [10-javascript-sites](../docs/10-javascript-sites.md) | SPA・ハイブリッドレンダリング固有の破綻 |
| [11-ai-search-visibility](../docs/11-ai-search-visibility.md) | AI回答での引用、クローラ方針を事業判断として扱う |
| [12-ci-gates](../docs/12-ci-gates.md) | 直したものが3リリース後に静かに戻るのを止める |
| [13-antipatterns](../docs/13-antipatterns.md) | 売られているが効かないもの |

**再利用する材料**

[skills/](../skills/) にエージェント用プレイブックが5本、[templates/](../templates/) に4種、[checklists/](../checklists/) に公開前と移行時のチェックリストがある。

## エージェントから使う

プレイブックをエージェントのスキルディレクトリにコピーする。Claude Codeの場合:

```bash
cp -r skills/seo-technical-audit ~/.claude/skills/
```

リポジトリを読み、シェルを実行し、URLを取得できるエージェントを前提にしている。人が手で読んで実行しても同じことができる。

## 約束しないこと

検索順位は誰も保証できない。流入数もコンバージョン数も同じ。被リンク獲得の営業活動は範囲外。コアアップデートへの耐性は、Google社外の誰にも事前には分からない。

[08-phase4-measurement](../docs/08-phase4-measurement.md) に書いた観測窓の日数は実務上の仮定であり、検索エンジンが公表した値ではない。自分のデータで較正して書き換えて使う。

## ライセンス

MIT。[LICENSE](../LICENSE) を参照。
