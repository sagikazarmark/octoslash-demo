# Octoslash Demo

## In browser

1. Create a new repository using the template
1. Check out the repository (OR open it in Codespaces) and update `.github/octoslash/principals.json` to your GitHub details
    > [!NOTE]
    > You can get your GitHub ID by running `gh api "/user" --jq '.id'`
1. Create a new issue
1. Try one of the builtin slash commands

> [!NOTE]
> Don't forget to cleanup the repository after you're done

## In terminal

```bash
# Create and checkout a new repository using the template
gh repo create --template sagikazarmark/octoslash-demo --public --clone octoslash-test
cd octoslash-test

# Update principals.json with your GitHub details
# Without this step you won't have permission to run slash commands
gh api "/user" | jq '[{uid: {type: .type, id: (.id|tostring)}, attrs: {login: .login}, parents: [{type: "Role", id: "Collaborator"}]}]' > .github/octoslash/principals.json
git add .github/octoslash/principals.json
git commit -m "Update permissions"
git push

# Create a new issue
gh issue create --title "Testing slash commands" --body ""

# Check out the issue
gh issue view 1

# Add a label to the issue
gh issue comment 1 --body "/label enhancement"

# Wait a few seconds for the label to be applied then confirm the label was applied
gh issue view 1

# Close the issue (reason is optional)
gh issue comment 1 --body "/close not_planned"

# The issue should be closed
gh issue view 1

# Cleanup
gh repo delete --yes octoslash-test
cd ..
rm -rf octoslash-test
```
