### Files used by Guard

#### Project-specific Guard DSL files:

  `Guardfile` (in current directory) - can contain DSL statements, evaluated by Guard during startup

  `.Guardfile` (in current directory) - if it exists, it is used instead of the `Guardfile`

#### Global Guard DSL files:

`~/.guard.rb` (in home directory) - can contain DSL statements. If it exists, it is always evaluated by Guard (before evaluating the project-specific DSL).

#### Pry-only config

`~/.guardrc` (in home directory) - if it exists, it is evaluated by the Pry interator (and should not contain DSL statements)
