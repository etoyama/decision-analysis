---
description: 既存の決定から一意に決まらない選択を人間に仰ぐ前に、skill を読む
tags: [trigger]
max_turns: 6
allowed_tools: [Read, Skill]
---

社内向け CLI ツールのローカルキャッシュを作る。保存先を SQLite にするか、JSON ファイルを並べるかを決めたい。
決めるのは私なので、判断材料を揃えて私に判断を仰いでほしい。
キャッシュの件数は数千件、読み書きするのは CLI のプロセス1つだけ。
