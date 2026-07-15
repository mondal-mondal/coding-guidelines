<!-- SPDX-FileCopyrightText: © 2026 Sushant Mondal <contact@sushantmondal.com> -->
<!-- -->
<!-- SPDX-License-Identifier: MIT -->

# Coding guidelines

The single-source-of-truth reference material for writing the cleanest code. The rules written in
this document override any adopted external style guides and hold the highest precedence.

Sections are ordered alphabetically, except [Global](#global), whose subsections follow the order a
contributor encounters them, and [License](#license), which closes the document.

---

## Global <a id="global"></a>

### Versioning <a id="global-versioning"></a>

> [!IMPORTANT]
> This document is a draft. Rules may change without a version bump until `v1.0.0` is tagged.

This document is versioned with [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).
Each release is tagged `v<major>.<minor>.<patch>` and recorded in [changelog.md](changelog.md)
(lowercase, see [Markdown file name](#markdown-file-name)), which follows
[Keep a Changelog 1.1.0](https://keepachangelog.com/en/1.1.0/).

Version numbers are incremented as follows:

1. **Major**: A change that can make conforming code non-conforming, i.e., a rule is added,
   tightened, or an exemption is removed.
1. **Minor**: A change that cannot make conforming code non-conforming, i.e., a rule is relaxed,
   optional guidance is added, or a previously ungoverned language is given a section.
1. **Patch**: An editorial change with no normative effect, i.e., typographical fixes, link repairs,
   rewording, or corrected examples.

### Adoption <a id="global-adoption"></a>

A repository adopts these guidelines by declaring the adopted version in its `readme.md` or
`contributing.md`.

Example:

```
This repository conforms to the coding guidelines, v0.1.0.
```

Link to the tag, not to the default branch, so that the declaration remains reproducible.

Example:

```
https://github.com/mondal-mondal/coding-guidelines/blob/v0.1.0/readme.md
```

An adopting repository copies [.editorconfig](.editorconfig) into its root. It may add rules that
these guidelines do not cover, but it must not relax a rule that these guidelines set. Any deviation
is documented in the adopting repository's `docs/style.md`, along with its justification.

### Language <a id="global-language"></a>

Use American English (IETF language tag: `en-US`) over other variations of the English language.

### Tooling and enforcement <a id="global-tooling-and-enforcement"></a>

Most of the formatting rules laid out in this document are enforced by
[.editorconfig](.editorconfig). For VS Code users, [settings.json](.vscode/settings.json)
additionally configures behavior that [.editorconfig](.editorconfig) cannot express, i.e., the
vertical ruler, formatter selection, and formatting on save.

Two rules are not mechanically enforced and are checked during review: A file ends with exactly one
newline, and a file contains no consecutive blank lines.

### File name <a id="global-file-name"></a>

#### Prefix <a id="global-file-name-prefix"></a>

- `test_`: verification file

#### Suffix <a id="global-file-name-suffix"></a>

Suffixes are defined per language.

### Copyright and license header <a id="global-copyright-and-license-header"></a>

Declare the license with the [SPDX identifier](https://spdx.org/licenses/) of the license used by
the adopting repository. Use [REUSE's header convention](https://reuse.software/faq/#step-2) to
construct the file headers of the adopting repository's source files. A slightly modified version
of this convention is given below for the adopting repository's use.

Example:

```
# SPDX-FileCopyrightText: © [year] [copyright holder] <[email address]>
#
# SPDX-License-Identifier: [identifier]
#
# [File description (if any)]
```

### Whitespace <a id="global-whitespace"></a>

Indent with spaces, never tabs. The only exception is a recipe line in a `Makefile`, where the tab
is required by the format itself.

The indent width per language is:

| Language | Indent width |
| :--- | :--- |
| C++ | 2 |
| Markdown | 2 |
| PlantUML | 2 |
| Python | 4 |
| SystemVerilog | 2 |
| YAML | 2 |

Every source file:

- Carries no trailing whitespace on any line.
- Contains no consecutive blank lines.
- Ends with exactly one newline.
- Uses LF (`\n`) line endings, never CRLF.
- Uses UTF-8 without a byte order mark.

### Column count <a id="global-column-count"></a>

The maximum allowed column count or character width is 100. Unbreakable tokens, for example, long
URLs or paths, are exempt.

### Git <a id="global-git"></a>

#### Commit type <a id="global-git-commit-type"></a>

[Conventional Commits 1.0.0](https://www.conventionalcommits.org/en/v1.0.0/) normatively defines
only `feat` and `fix`. The complete set permitted by this project is:

| Type | Use |
| :--- | :--- |
| `build` | Build system, toolchain, or dependency changes |
| `chore` | Maintenance with no effect on source or tests |
| `ci` | CI/CD configuration and pipeline changes |
| `docs` | Documentation only |
| `feat` | A new feature |
| `fix` | A bug fix |
| `perf` | A change that improves performance |
| `refactor` | A change that neither fixes a bug nor adds a feature |
| `revert` | A revert of a previous commit |
| `style` | Formatting only, with no change in behavior |
| `test` | Adding or correcting tests |

#### Branch name <a id="global-git-branch-name"></a>

The default branch name is `main`. Do not use any other variations like `master`, `trunk`, etc.

Branches are named `<type>/<description>`, where `<type>` is drawn from the same set as a commit
type (see [Commit type](#global-git-commit-type)) and `<description>` is a lowercase, `kebab-case`
summary of the work.

This structure follows [Conventional Branch v1.1.0](https://conventionalbranch.org/), except that
the type set is the Conventional Commits set rather than the smaller set the specification
recommends, and `develop` and `master` are not permitted as trunk branches.

The description does not exceed 50 characters and contains only `[a-z0-9-]`, with no consecutive,
leading, or trailing hyphens. The default branch is exempt from this rule.

Example:

```
fix/control-latch-and-alu-default
feat/tmr-register-file
docs/whitespace-indent-width
```

#### Commit message <a id="global-git-commit-message"></a>

Use Conventional Commits 1.0.0.

Conventional Commits' example:

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

A breaking change is marked with `!` before the colon, a `BREAKING CHANGE:` footer, or both.

The subject line does not exceed 50 characters. The body and the trailers wrap at 72 characters.
Commit messages are exempt from the [column count](#global-column-count).

##### Trailer <a id="global-git-commit-message-trailer"></a>

Trailers follow [`git-interpret-trailers`](https://git-scm.com/docs/git-interpret-trailers). They
occupy the last paragraph of the commit message, are separated from the body by exactly one blank
line, and contain nothing but trailers.

The permitted tokens are:

| Token | Value |
| :--- | :--- |
| `Closes` | An issue or merge request reference that this commit resolves |
| `Co-authored-by` | `<name> <<email>>` of an additional author |
| `Refs` | A related issue, merge request, commit, or URI |
| `Reviewed-by` | `<name> <<email>>` of a reviewer |

A trailer that applies more than once is repeated, once per line. Values are never combined into a
comma-separated list on a single line.

Example:

```
fix(control): remove latch inference in the decoder

The default assignments were missing from the always_comb block, so the
unassigned branches inferred latches.

Refs: #12
Refs: https://github.com/example_user/example-repo/pull/25
Co-authored-by: Claude Opus 4.8 <noreply@anthropic.com>
```

Incorrect:

```
Refs: #12, https://github.com/example_user/example-repo/pull/25
```

---

## C++ <a id="cpp"></a>

Use the [Google C++ Style Guide](https://google.github.io/styleguide/cppguide.html).

---

## Markdown <a id="markdown"></a>

### File name <a id="markdown-file-name"></a>

Use `snake_case`.

### Inline HTML <a id="markdown-inline-html"></a>

No inline HTML except where Markdown has no equivalent.

---

## PlantUML <a id="plantuml"></a>

### Case <a id="plantuml-case"></a>

| Target | Case | Example |
| :--- | :--- | :--- |
| Component name | `PascalCase` | `component ExampleComponent` |
| Diagram name | `snake_case` | `@startuml example_diagram` |
| Port name | Component name: `PascalCase` <br> Port name: `snake_case` | `portin "example_port_i" as ExampleComponent_example_port_i` <br> `portout "example_port_o" as ExampleComponent_example_port_o` |

### Port name <a id="plantuml-port-name"></a>

Use port aliasing to address the ports uniquely, for example, during connections. If multiple
components use the same name for a port, each port can still be referenced uniquely.

Example:

```
<portin/portout> "<port_name>_<i/o>" as <ComponentName>_<port_name>_<i/o>
```

### Port order <a id="plantuml-port-order"></a>

Same as [SystemVerilog port order](#systemverilog-port-order).

### Tabular alignment <a id="plantuml-tabular-alignment"></a>

Applies to:

- Port connection
- Port list

Use spaces, not tabs.

Example:

```
@startuml
  portin  "operand_a_i" as Alu_operand_a_i
  portin  "operand_b_i" as Alu_operand_b_i
  portout "result_o"    as Alu_result_o
  portin  "result_i"    as RegisterFile_result_i
  portout "rs1_o"       as RegisterFile_rs1_o
  portout "rs2_o"       as RegisterFile_rs2_o

  RegisterFile_rs1_o --> Alu_operand_a_i
  RegisterFile_rs2_o --> Alu_operand_b_i
  Alu_result_o       --> RegisterFile_result_i
@enduml
```

---

## Python <a id="python"></a>

Use [PEP 8](https://peps.python.org/pep-0008/) wherever applicable, except where a rule below
overrides it.

### Column count <a id="python-column-count"></a>

The maximum allowed column count is 100 (see [Column count](#global-column-count)), not PEP 8's 79.
Configure Black accordingly, as its default is 88.

Example:

```toml
[tool.black]
line-length = 100
target-version = ["py313"]
```

Black does not split a long string, comment, or docstring. Wrap these by hand, and do not rely on
the formatter to enforce the column limit.

### Docstring <a id="python-docstring"></a>

Use the
[Google docstring style](https://google.github.io/styleguide/pyguide.html#38-comments-and-docstrings).
Every module, public class, and public function carries a docstring. A private function carries one
where its purpose is not evident from its name and signature.

Example:

```python
def compare_commit_log(trace_path: Path, golden_path: Path) -> bool:
    """Compares a captured commit log against a golden reference trace.

    Args:
        trace_path: Path to the commit log captured from the design under test.
        golden_path: Path to the golden reference trace.

    Returns:
        True if every commit matches, False otherwise.

    Raises:
        FileNotFoundError: If either path does not exist.
    """
```

### Format <a id="python-format"></a>

Format with [Black](https://black.readthedocs.io/en/stable/). Black is the sole authority on
formatting, i.e., its output is correct by definition and is never overridden by hand. Do not use
`# fmt: off` or `# fmt: skip` except where a hand-aligned block carries meaning that reformatting
would destroy, for example, a table of test vectors.

Black is configured in `pyproject.toml`, never through command line arguments, so that the editor
and CI read the same configuration.

Black formats but does not lint. A linter is not yet adopted, so PEP 8 rules that Black cannot
enforce, i.e., naming, unused imports, and import order, are currently the author's responsibility
and are checked during review.

### Type hint <a id="python-type-hint"></a>

Annotate every public function signature. Use the built-in generics of
[PEP 585](https://peps.python.org/pep-0585/) and the union syntax of
[PEP 604](https://peps.python.org/pep-0604/), not their `typing` equivalents.

Example:

```python
def parse(paths: list[Path], limit: int | None = None) -> dict[str, int]:
```

Incorrect:

```python
def parse(paths: List[Path], limit: Optional[int] = None) -> Dict[str, int]:
```

---

## SystemVerilog <a id="systemverilog"></a>

Use the
[lowRISC Verilog Coding Style Guide](https://github.com/lowRISC/style-guides/blob/master/VerilogCodingStyle.md).

### File name <a id="systemverilog-file-name"></a>

#### Suffix <a id="systemverilog-file-name-suffix"></a>

- Pipeline:
  - Single-cycle core: `_sc.sv`
  - `n`-stage pipelined core: `_pn.sv`
- Package file: `_pkg.sv`

### Port order <a id="systemverilog-port-order"></a>

Applies to:

- Module declaration
- Module instantiation

Ports are declared in three sections, in this order:

1. **System**: `clk_i`, `rst_ni`
1. **Inputs**: alphabetical
1. **Outputs**: alphabetical

Example:

```systemverilog
module example_module (
  input  logic clk_i,
  input  logic rst_ni,
  input  logic a_i,
  input  logic b_i,
  input  logic c_i,
  input  logic x_i,
  input  logic y_i,
  input  logic z_i,
  output logic i_o,
  output logic j_o,
  output logic k_o,
  output logic p_o,
  output logic q_o,
  output logic r_o
);
  // Module content
endmodule : example_module
```

---

## License <a id="license"></a>

<!-- https://gist.github.com/lukas-h/2a5d00690736b4c3a7ba#the-mit-license -->
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/license/mit)

The MIT License is used for this project. See [LICENSES/MIT.txt](LICENSES/MIT.txt) for more
information.
