---
name: code_python
description: Use before writing, changing, or running Python scripts in the sandbox. Covers reusable argparse-based tools, safe credential handling, execution, testing against a second input, and reporting failures.
---

# Reusable Python scripts

Load this skill before writing, changing, or running a Python script.

## Before writing

- If memory search and load tools are available, search for an existing script that answers this kind of question. Reuse it when suitable; extend it with arguments when needed.
- Write a reusable tool for the kind of question, not a one-off answer.

## Writing

1. Put every value that may change between runs in a named `argparse` argument. Use defaults only for values that remain constant across questions.
2. Name the file for what it does, using a verb-first name. Avoid generic names such as `script.py`, `test.py`, and `tmp.py`.
3. Start with a docstring describing the question the script answers. Use the same description in `argparse`, and provide `help=` for every argument.
4. Print results to stdout and diagnostics to stderr. Exit non-zero with a clear error message when the script cannot answer. Write output files only to the path supplied by `--output`.
5. Read credentials from environment variables. Never hard-code secrets or put them in argument defaults.
6. Use only dependencies already present in the sandbox image. Do not install packages from the script or before running it.
7. Save the script to a file and run that file with `python`; do not use `python -c` or heredocs to execute Python.

## Before relying on the result

- Run the script and inspect its output. If it fails or produces an incorrect result, fix the script rather than manually altering the output.
- Test it with a different input of the same kind. If that requires editing the code instead of passing different arguments, move the remaining hard-coded value into an argument.
- If memory-commit tools are available, save the working script as a file node with a description of the question it answers and its arguments.

## Reporting

Report the script path, the arguments used, the observed result, and any failures or limitations. Do not claim a script was tested unless it was run and its output inspected.
