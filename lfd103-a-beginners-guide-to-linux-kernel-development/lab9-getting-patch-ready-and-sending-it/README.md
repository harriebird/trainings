# lab9-getting-patch-ready-and-sending-it

This activity guides in getting patches ready and sending it.

Using get_maintainer.pl to know the people involved:
./scripts/get_maintainer.pl 

Generate a patch with the correct receipients from the get_maintainer.pl:
git format-patch -1 <commit ID> --to=maintainer1 --to=maintainer2 --cc=maillist1 --cc=mailist2

`to` for the people involved
`cc` for the mailings lists

Send patch using git:
git send-mail <patch-file>

When sending new version of patch:
- Add version history after the `---` below the `Signed-off-by` tag

Preparing and sending patches:
- Run `checkpatch.pl` before sending the patch. 
- `Signed-of-by` should be the last tag
- Copy mailings lists and people involved suggested by `get_maintainer.pl`
- When patch is based on an idea or suggested by someone else, give credit using the `Suggested-by` tag. Other tags like `Testted-by` and `Reported-by` may be also used.
- When needed to send multiple related patches, grouping them into a patch series is useful:
    - git format-patch -2 -s --cover-letter --thread --subject-prefix="PATCH v3" --to="name" --cc="name"

Working with Reviewers:
- Be patient and wait for at least one week before requesting comments
- Always thank the reviewers for their feedback and address each comment
- Do not take feedback personally
- When responding to emails, don't top-post. Responses should be inlined
- Be prepared to make changes and work through multiple versions of patch before it is accepted
- If you disagree with other people involved, present your reasons clearly and include supporting technical data such as benchmarks or other evidence of improvement

After Patch is accepted:
- Stay engaged and be ready to fix problems
- When a patch gets accepted, an email will be received from the maintainer or automated patch accept email
- After acceptance, the could stay in the `linux-next` until the next merge window. If the patch is a fix for a bug in Linus' tree, it may go directly in his tree without waiting for the next merge window
- Be prepared for differences between maintainers

Git includes hooks, which are scripts that can be run automatically along with specific git commands

Install codespell:
sudo dnf install codespell

Put the code below inside `.git/hooks/post-commit`:

```
#!/bin/bash
exec git show --format=email HEAD | ./scripts/checkpatch.pl --strict --codespell
```

Make the post-commit executable:
chmod a+x .git/hooks/post-commit

After post-commit execution:
git commit --amend
