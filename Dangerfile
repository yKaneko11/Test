# Check PR
warn("PRがWIPになってるよ！🐶") if github.pr_title.include? "[WIP]"

warn("PRのタイトルが短すぎるよ！🐶") if github.pr_title.length < 5

warn("PRにタイトルが書かれてないよ！🐶") if github.pr_title.length == 0

warn("PRの説明が短すぎるよ！レビュアーが見て分かる説明を書いてね！🐶") if github.pr_body.length < 5

warn("PRにassigneeが設定されてないよ！🐶") unless github.pr_json["assignee"]

pr_has_screenshot = github.pr_body =~ /https?:\/\/\S*\.(png|jpg|jpeg|gif){1}/
warn("UIレビューの時はスクリーンショットを添付してね！🐶") if !pr_has_screenshot

## assigneeが未割り当てかのチェック
if github.pr_json['assignee'] == nil
  ## github.api 経由で GitHubの操作可能
  github.api.add_assignees(
    github.pr_json['base']['repo']['full_name'],
    github.pr_json['number'],
    [github.pr_author] ## <- 起票者は github.pr_author
  )
end

if github.pr_title.include? 'WIP'
    markdown(
      "@#{github.pr_author} タイトルの[WIP]は非推奨です。GitHubのDraft Pull Request機能を使ってください。途中からでもDraftにできます。"
    )
  end

# 修正範囲外をチェック対象から外します。
github.dismiss_out_of_range_messages

# Swiftlint
# swiftlint.config_file = '.swiftlint.yml'
# swiftlint.lint_files inline_mode: true
