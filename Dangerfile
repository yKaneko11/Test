# Sometimes it's a README fix, or something like that - which isn't relevant for
# including in a project's CHANGELOG for example
declared_trivial = github.pr_title.include? "#trivial"

# Make it more obvious that a PR is a work in progress and shouldn't be merged yet
warn("PR is classed as Work in Progress") if github.pr_title.include? "[WIP]"

# Warn when there is a big PR
warn("Big PR") if git.lines_of_code > 500

# Don't let testing shortcuts get into master by accident
fail("fdescribe left in tests") if `grep -r fdescribe specs/ `.length > 1
fail("fit left in tests") if `grep -r fit specs/ `.length > 1

## assigneeが未割り当てかのチェック
if github.pr_json['assignee'] == nil
  ## github.api 経由で GitHubの操作可能
  github.api.add_assignees(
    github.pr_json['base']['repo']['full_name'],
    github.pr_json['number'],
    [github.pr_author] ## <- 起票者は github.pr_author
  )
end