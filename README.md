# Composite Action Recipe

A GitHub composite action that greets a user and returns the answer to life, the universe and everything (42).

## Usage

```yaml
- name: Run Composite Action Recipe
  id: my-action
  uses: mzdrenka/CompositeActionRecipe@v1
  with:
    who-to-greet: '@your-username'

- name: Use the output
  run: echo "The answer is ${{ steps.my-action.outputs.answer }}"
```

## Inputs

| Input | Description | Required | Default |
|---|---|---|---|
| `who-to-greet` | Who to greet | Yes | `Świat` |

## Outputs

| Output | Description |
|---|---|
| `answer` | The answer to life, the universe and everything |

## Example workflow

```yaml
name: Example

on: [push]

jobs:
  example:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Run Composite Action Recipe
        id: my-action
        uses: mzdrenka/CompositeActionRecipe@v1
        with:
          who-to-greet: '@mateusz'
      - name: Print the answer
        run: echo "The answer is ${{ steps.my-action.outputs.answer }}"
```

## License

MIT
