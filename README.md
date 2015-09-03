# Building CLI Applications in Ruby

## Objectives

1. Understand the Structure of a CLI Application
2. Run a CLI Application
3. Understand the CLI User Interface
4. Accept input from the user.
5. Use the input within your program.

## CLI File Structure

As our applications increase in complexity we'll have to keep our project files well organized. There's a pretty standard convention for where to put code in a project based on what the code does.

We're going to learn a simplified pattern for organizing code in a ruby application. We'll build on this structure.


### A Simple Ruby CLI Application

From the root directory of a ruby applications, you should see a folder structure similar to the following:

```
├── bin
│   └── tictactoe
├── config
│   └── environment.rb
├── lib
│   └── tic_tac_toe.rb
└── spec
    ├── tic_tac_toe_spec.rb
    └── spec_helper.rb
```

You might not have all those folders or those exact files, but you'll have a similar structure. You'll see top-level directories (the top most folders within your project) such as: `bin`, `lib`, `config`, `spec` and sometimes `app`. You'll also might see some top-level files (files located directly within your project) such as: `.learn`, `.rspec`, `Gemfile`, or `Rakefile`.

`cd` into the directory of a lab you recently solved in terminal. Within that directory type `ls -lah` to list all the files in the current directory, including hidden files, in a human order. You should see something similar.

*Mac OS X ONLY**

From within a project directory in terminal, type `open .` to open the project folder graphically in Finder.

Let's talk about what kind of code goes where.

#### `bin/`

Executables

#### `config/`

Environment

#### `lib/` (`app/`)

Code

#### `spec/`

Tests

#### `.rspec`, `.learn`, `Gemfile`, `Gemfile.lock`, `Rakefile`

Developer tools

## Running CLI Applications



## The CLI Interface

## User input via `gets`

## A Complete CLI Application
