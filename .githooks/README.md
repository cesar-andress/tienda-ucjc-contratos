# Git hooks (profesor)

Tras clonar:

```bash
git config --local core.hooksPath .githooks
git config --local user.email cesar.andress@ucjc.edu
git config --local user.name 'César Andrés'
```

- `pre-commit`: falla si autor, committer o `user.email` local ≠ `cesar.andress@ucjc.edu`
- `prepare-commit-msg`: elimina `Co-authored-by: Cursor`
- `commit-msg`: rechaza Cursor / aiserv en el mensaje
