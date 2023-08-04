# Unity.Mathematics.Serializable

Serialization for [Unity.Mathematics](https://github.com/Unity-Technologies/Unity.Mathematics):

* FlatBuffer through [FlatSharp](https://github.com/jamescourtney/FlatSharp)
* JSON serialization through [System.Text.Json](https://learn.microsoft.com/en-us/dotnet/api/system.text.json?view=net-7.0)

## Package references

Unity.Mathematics is referenced:

* as NuGet via [Unity.Mathematics.NuGet](https://github.com/KageKirin/Unity.Mathematics.NuGet).
* as Unity package via UPM.

## Usage in regular C# applications (via NuGet)

## Usage in Unity applications (via UPM)

## Implementation details for JSON

### Vector types

A vector type, e.g. `math.float3` can technically be serialized in 2 forms:

* object type, i.e. `{ "x" = 1, "y" = 2, "z" = 3}`
* array type, i.e. `[1, 2, 3]`

Both serializers are implemented, but the default configuration is to use the array type.

## Git informations

### Follow [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/)

The most common ones are:

* `feature (tag): subject`
* `fix (tag): subject`
* `refactor (tag): subject`
* `doc (tag): subject`

* `repo: subject` represents changes on the repo level (e.g. submodule update, lfs attributes, etc).
* `chore: subject` is reserved for whitespace and formatting changes (_if and only if_ they could not be squashed into other commits).
* `build: subject` is reserved for project and solution changes, e.g. adding/removing/updating a dependency.

### Merge as Squash-Merge

Commit message yielded by the git-alias below:

```git
hub-squash = "!f() { j=\"$(gh pr status --json title,number,headRefName,body)\"; num=$(jq -r .currentBranch.number <<< $j); title=\"$(jq -r .currentBranch.title <<< $j) ($(jq -r .currentBranch.headRefName <<< $j)) [#$num]\"; body=\"$(jq -r .currentBranch.body <<< $j)\n\n$(jq -r .currentBranch.body <<< $j)\"; gh pr merge -d --squash --subject \"$title\" --body \"$body\";}; f"
```

* `$title` is the PR title. It must follow Conventional Commits style.
* `$body` is the PR body. Ideally created automatically through `gh pr create --fill`. It should contain a bullet point list of the squashed commits.

#### Why squash-merge?

Squash-merges offer 2 non-negligeable benefits over regular merges:

* they are easy to rebase (regular merges get unrolled if not taken care)
* they hide a sometimes messy feature-branch

Squash-merges offer 2 non-negligeable benefits over regular rebase-merges:

* they hide a sometimes messy feature-branch
* they do not spam the repo history with detail commits

Further, they are similar to Perforce Submits, and as such offer a better understanding
to Perforce users.
