---
type: llm
---

PASS if the final response contains all of: problems numbered with IDs (課題1, 課題2, ...); a criteria table where every criterion has a source (出典) and every Want is classified as 解決 or 費用 with who set its weight (人間 or Claude の推測); a "do nothing" option; an evaluation written as sentences, not summed scores, that names which criteria differentiate the options; a sensitivity line; risks for every option, not only the recommended one; and a recommendation.
FAIL if any of these is missing, if the options are compared by a score total, or if the decision is handed over only as AskUserQuestion option descriptions.
