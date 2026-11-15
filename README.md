# decision-analysis

Claude Code が人間に判断を仰ぐとき、課題・比較軸・Must/Want の根拠を備えた
軽量の Decision Analysis で提示させる plugin。

## なぜ

判断を仰がれても、何を基準に比べたのか、なぜその条件が外せないのかが書かれていないと、
聞き返すたびに往復が増える。この plugin は、すべての比較軸に出典（課題・ADR・人間の発言など）を
持たせ、重みを誰が決めたかを書かせる。人間は基準の立て方そのものに質問できる。

## 何が入っているか

| 部品 | 役割 |
|---|---|
| `hooks/` の SessionStart hook | 事前の対策。どんな判断で DA を使うかの発動条件を、毎回のセッションに入れる |
| `skills/decision-analysis/SKILL.md` | 形式の正本。出し直しの手順と、ADR への対応も持つ |
| `skills/decision-analysis/example.md` | この形式で書いた判断の見本 |
| `evals/` | 発動の評価ケース（`claude plugin eval .` で実行） |

事後の対策として、提示が足りなかったときは次のどれかで出し直させる。

- `/decision-analysis` を実行する（同じ名前のコマンドが他にあるときは `/decision-analysis:decision-analysis`）
- 「DA で」「Decision Analysis で出し直して」と言う
- 判断の理由を聞き返す（発動条件に入っているので、Claude が自分から出し直す）

## 形式の要点

- Problem: 課題に ID を振る。前提にした事実と、それを確かめた方法を書く。
- Criteria: Must は二択で判定できるもの。Want は「解決」か「費用」に分類する。
  すべての基準に出典を持たせ、重みを決めた人（人間 / Claude の推測）を書く。
- Evaluation: 点数の合計は出さず、セルを文で書く。差がつく基準と、結論が変わる重み（感度）を明示する。
- Risks: 推奨案だけでなく、全案について書く。

## 導入

Claude Code の中で:

```text
/plugin marketplace add etoyama/decision-analysis
/plugin install decision-analysis@decision-analysis
```

シェルから（スクリプトに書くとき）:

```bash
claude plugin marketplace add etoyama/decision-analysis
claude plugin install decision-analysis@decision-analysis
```

SessionStart hook は次に開いたセッションから効く。

更新は `claude plugin update decision-analysis@decision-analysis` のあとセッションを開き直す。
バージョンは `.claude-plugin/plugin.json` の `version` だけで持つ。変更を配るときはここを上げる
（上げないと、導入済みの環境はキャッシュを使い続ける）。

## 開発

```bash
claude plugin validate .
claude --plugin-dir . plugin details decision-analysis
claude --plugin-dir .
claude plugin eval . --no-publish
```

`--plugin-dir .` で開いたセッションでは、導入せずに手元のファイルがそのまま読まれる。
`claude plugin eval` は Claude Code v2.1.269 以降で使える。結果は `evals/results/` に書かれる（git 管理外）。

## License

MIT
