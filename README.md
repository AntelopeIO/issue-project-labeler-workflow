## Add Label & Project To Issue

This reusable workflow can add a label and/or project to an issue, as well as set one field in the project. The motivation behind it is to assign an initial triage status to new issues as they are created.

### Inputs
* **issue-id** - The node_id of the issue to act upon, required.
* **label** - The name of the label to add to the issue, optional.
* **repo-project**, **user-project**, **org-project** - Define one (projects can live at the repo, user, or org level) or none of these; the name of the project to add the issue to.
* **project-field** - An optional definition of a `field-name=value` pair to set on the project's entry for this issue. Only `TEXT` & `SINGLE_SELECT` field types are supported.
* **token** - A required secret. This needs to have permissions to write to issues (if `label` is set), and write permission to projects if the project related options are set.

Example:
```yaml
jobs:
  handle_new_issue:
    uses: AntelopeIO/issue-project-labeler-workflow/.github/workflows/issue-project-labeler.yaml@v1
    with:
      issue-id: ${{github.event.issue.node_id}}
      label: triage
      org-project: 'My Org Project'
      project-field: Status=Todo
    secrets:
      token: ${{secrets.REPO_PROJECT_TOKEN}}
```

