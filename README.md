# CompositeActionRecipe

Przykładowa GitHub Action typu composite, gotowa do przygotowania pod publikację w GitHub Marketplace.

## Co robi ta akcja

- wypisuje powitanie dla wskazanego użytkownika,
- ustawia output `answer` na wartość `42`,
- przy zdarzeniu `issues.opened` może dodać komentarz z podziękowaniem za zgłoszenie.

## Wymagania i uprawnienia

Akcja korzysta z `actions/github-script@v6`.

Jeżeli chcesz używać funkcji komentowania zgłoszeń, workflow musi mieć uprawnienie:

```yaml
permissions:
  issues: write
```

Jeżeli akcja ma tylko wypisać powitanie i zwrócić output, dodatkowe uprawnienia nie są wymagane.

## Użycie

### Podstawowy przykład

```yaml
name: Example

on:
  workflow_dispatch:

jobs:
  demo:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - id: recipe
        uses: mzdrenka/CompositeActionRecipe@v1
        with:
          who-to-greet: "@mateusz"

      - run: echo "Answer: ${{ steps.recipe.outputs.answer }}"
```

### Użycie dla nowych issue

```yaml
name: Thank issue reporter

on:
  issues:
    types: [opened]

jobs:
  thank-reporter:
    runs-on: ubuntu-latest
    permissions:
      issues: write
    steps:
      - uses: mzdrenka/CompositeActionRecipe@v1
        with:
          who-to-greet: "${{ github.actor }}"
```

## Inputs

| Nazwa | Wymagane | Domyślnie | Opis |
| --- | --- | --- | --- |
| `who-to-greet` | tak | `Świat` | Nazwa lub handle osoby, którą akcja ma przywitać |

## Outputs

| Nazwa | Opis |
| --- | --- |
| `answer` | Zwraca wartość `42` |

## Wersjonowanie i publikacja

Przed publikacją w GitHub Marketplace:

1. upewnij się, że repozytorium jest publiczne,
2. utwórz release, na przykład `v1.0.0`,
3. dodaj stabilny tag główny, na przykład `v1`,
4. używaj akcji w workflow przez `mzdrenka/CompositeActionRecipe@v1`.

To repo zawiera już plik `action.yml`, więc po przygotowaniu opisu, release i tagów może zostać wystawione w Marketplace jako GitHub Action.