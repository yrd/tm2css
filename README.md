# Turing machines in CSS

This is a CSS-only (as in no Javascript) implementation of the (deterministic)
[Turing machine](https://en.wikipedia.org/wiki/Turing_machine) computation
model. It is expandable to a number of inputs

## Usage

See `main.scss` and `index.html`. Both files are fairly well commented which
should make it easy to expand the example. In short:

- Edit the variables at the top of the stylesheet to add more storage or inputs
  to the machine, or to modify its alphabet.
- Edit the HTML file to make sure the DOM is conform to your changed variables.
- Write a program in the stylesheet.
- Compile the CSS with `sass main.scss:main.css`.

## How it works

This simulation works by saving its current state into CSS custom properties
with a [one-hot](https://en.wikipedia.org/wiki/One-hot) encoding scheme. See the
comments in `main.scss` for more details.

As an example, given 3 simulated cells and an alphabet with the two symbols `a` and
`b`, the following CSS variables will be created:

- `--cell--1-value-a`
- `--cell--1-value-b`
- `--cell-0-value-a`
- `--cell-0-value-b`
- `--cell-1-value-a`
- `--cell-1-value-b`

Each of these evaluated to `0` or `1`, which denotes whether the corresponding
cell has that value. That also means that at most one of the `--cell-x-value-y`
for a given cell `x` will evaluate to one (since a cell may only contain one
value). The turing machine's code is then compiled to a boolean expression,
which is solved using CSS arithmetic.

### Complexity

For each step, the browser needs to evaluate about *O(r + s + n\*a)* variables,
corresponding as follows:

- *r*: Number of rules
- *s*: Number of states
- *n*: Size of the tape that is simulated
- *a*: Size of the alphabet

