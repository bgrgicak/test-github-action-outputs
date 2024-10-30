# test-github-action-outputs

This repository is used to test the behavior of GitHub Actions outputs.

## Minimal example

```yaml
- name: Set color
  id: color-selector
  run: echo "SELECTED_COLOR=green" >> "$GITHUB_OUTPUT"
- name: Get color
  env:
    SELECTED_COLOR: ${{ steps.color-selector.outputs.SELECTED_COLOR }}
  run: echo "The selected color is $SELECTED_COLOR"
```

## Echoed values must have an `id` to set a output value

Every echoed value [must have an `id` to set a output value.](https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/workflow-commands-for-github-actions#setting-an-output-parameter)

### If a variable doesn't exist it will match '0' in a step condition

If there is no id the variable doesn't exist, but the condition `if: steps.changes.outputs.VALUE == '0'` will be true.

You can see how [this example](.github/workflows/action.yml) action [runs in a test](https://github.com/bgrgicak/test-github-action-outputs/actions/runs/11592008203/job/32272970903).