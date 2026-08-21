---
name: venv
description: >-
  Activate the correct project .venv and run Python in project environments.
  Use when running Python, uv pip, training scripts, tests, or jobs under
  /home/$USER/<project>; when handling checkpoints, data, results, or symbolic
  links; or when the user mentions .venv.
---

# Project `.venv`

Each project has its **own** `.venv` at the project root. Always activate that project's venv before running Python.

## 1. Find and activate `.venv`

**Rules:**
1. Use the `.venv` belonging to the project you are working in. Do not reuse another project's venv.
2. Activate from that project's root (or use the absolute path):

```bash
cd /home/$USER/<project>
source .venv/bin/activate
```

3. Prefer invoking the venv Python directly when a non-interactive shell may not keep activation. Use `uv pip` for all package operations after activating the project `.venv`:

```bash
/home/$USER/<project>/.venv/bin/python ...
cd /home/$USER/<project>
source .venv/bin/activate
uv pip install ...
```

4. If `.venv` is missing, look one level up for the owning project root, or ask before creating a new venv.
5. Confirm the environment before long jobs:

```bash
which python
```

## 2. Standard run pattern

```bash
cd /home/$USER/<project>
source .venv/bin/activate
python <script> ...
```

## 3. Common mistakes

- Running system `python` or plain `pip` instead of the project `.venv` and `uv pip`
- Using another project's `.venv` (wrong packages)
- Using an unchecked relative path or a broken symbolic link
