# Building CLI Applications in Ruby

## Objectives

1. Understand the Structure of a CLI Application
2. Run a CLI Application
3. Understand the CLI User Interface

## CLI File Structure

As our applications increase in complexity we'll have to keep our project files well organized. There's a pretty standard convention for where to put code in a project based on what the code does.

We're going to learn a simplified pattern for organizing code in a Ruby application. We'll build on this structure.

### A Simple Ruby CLI Application

From the root directory of a Ruby application, you should see a folder structure similar to the following:

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
├── Gemfile    
├── ttt.rb    
```

You might not have all those folders or those exact files, but you'll have a similar structure.

You'll see top-level directories (the top most folders within your project) such as: `bin`, `lib`, `config`, `spec` and sometimes `app`.

You also might see some top-level files (files located directly within your project) such as: `.learn`, `.rspec`, `Gemfile`, or `Rakefile`. On some labs you might see an actual program file on the top level, like `ttt.rb`.

We try to always tell you where the files you need to read or edit are located in a particular lab. This is just *in general*.

`cd` into the directory of a lab you recently solved in terminal. Within that directory type `ls -lah` to list all the files in the current directory, including hidden files, in a human order. You should see something similar.

Let's talk about what kind of code goes where.

#### `bin/`

Within the `bin/` directory we generally put code that relates to running our actual program. Our executable files that we put in bin are described below, [running CLI applications](#running-cli-applications).

#### `config/`

A complex program might require 100s of individual files containing source code, method definitions, classes, and more that together constitute all the code required to run the application. We call this code the application's environment. We generally put all the code required to initialize the environment within `config/`. We might see that in a `config/environment.rb` file or even an entire `config/environments/` directory.

What does it mean to "initialize a program's environment?" Establishing the environment for your program can involve a number of things, but on the most basic level, the config file or directory is responsible for things like file requirements (i.e. making sure your different files have access to one another), establishing connections to your database (if you have one) and ensuring that your test suite has access to the files that contain the code it is testing.

#### `lib/` (`app/`)

The `lib/` or Library directory in most Ruby programs and the `app/` directory in Rails projects or complex Ruby programs, is where the majority of our code lives. Within this directory are all the files that define what our program can do. All of the methods and classes our program needs are defined within the files in this directory. One file might define a group of methods that can search for a song by an artist, another file might define a group of methods that can search for a song by a genre. Together these methods might interact to create a Music Search application. We spend the majority of our time building code in this directory.

#### `spec/` (`test/`)

Great developers write tests for their code. Whether through the practice of [Test-Driven Development](https://github.com/learn-co-curriculum/intro-to-tdd-rspec-and-learn/blob/master/README.md) or not, it's important to be able to write tests that make sure your code behaves as expected. It's also crucial to be able to read tests and understand the requirements they define for your code. All of our tests go into the `test/` or `spec/` directory.

#### `.rspec`, `.learn`, `Gemfile`, `Gemfile.lock`, `Rakefile`

There are a collection of files in most Ruby applications that provide tooling and support for your application. A common such file is `Gemfile`, used by [Bundler](http://bundler.io/) to manage gem dependencies. Another is a `Rakefile` for defining application tasks. Don't worry too much about these files for now.

**Advanced:** A gem is a library of code that you can include in your Ruby program to lend it the capabilities of that library. 

## Running CLI Applications

In order to run our program from the command line and allow our user to interact with our program as described above, we need to set up a few things.

First, your program needs a `bin` directory. "Bin" is short for "binary" and is just another way to refer to executable files. Accordingly, your executable files belong in this directory.

**Executable files** are any files that contain instructions in a form that a computer's operating system or application can understand and follow. Any executable files we place in our bin directory need to begin with the following line:

`#!/usr/bin/env ruby`

This is often referred to as a "shebang line" and it tells the shell which interpreter to use to execute the remainder of the file.

Using the above setup, you can run your program by typing `ruby bin/< your file name >` into the command line.

Alternatively, you can execute your program by simply typing `./bin/< your file name >` into the command line, since the shebang line at the top of your executable file is already telling the shell to use Ruby to interpret the rest of the file.

Generally our executable file is responsible for running our program. That might include loading required libraries and starting off an execution flow, like telling Ruby to start a game of Tic Tac Toe.

#### File Permissions and `chmod`

For security purposes, a shell environment, including BASH, running within your terminal, requires that executable files are given explicit permission to execute.

When we execute code through the ruby interpreter with the `ruby` command, your shell or terminal has already given the `ruby` command permission to execute code.

But in order for your shell to execute a file via a command like `./bin/<file name>`, you have to grant it execute permissions. We do this using the `chmod` command. You can grant a file execute permissions with:

```
$ chmod +x <file_name>
```

So to grant a file `bin/tictactoe` permissions to execute, you would run: `chmod +x bin/tictactoe`. Depending on your shell environment and user, you might need to run `chmod` with `sudo` (`sudo chmod +x bin/tictactoe`).

All the files provided by Learn already have the correct permissions and this should never cause you a problem. But in the event you need to ever create your own executable, we thought we'd tell you.

## The CLI Interface

CLI Applications generally follow a similar interface or user experience pattern. Imagine a CLI version of Tic Tac Toe. From a player's perspective, they would start the game by executing the `bin` for the game.

```
$ bin/tictactoe
```

The program will execute and generally greet the user with some text output:

```
$ bin/tictactoe

Hi! Welcome to Command Line Tic Tac Toe! Would you like to play? (Y/n)

```

The CLI will prompt the user for input and will hang until the user types something and presses enter. The CLI generally gives instructions for the expected input at a given prompt. In the example above, the greeting ends by asking the user if they would like to play.

### User Input

The `(Y/n)` at the end is a common convention for telling the user that the following prompt is looking for a "Yes" or "No" input as an answer. It is also saying it expects that input as a single character, either `y` or `n`. The capital `Y` is suggesting the default input if the user types nothing and simply presses enter. Generally CLIs will accept "Yes"/"No" in many forms (`yes`, `no`, `N`, `n`) and still use the `y/n` convention.

```
$ bin/tictactoe

Hi! Welcome to Command Line Tic Tac Toe! Would you like to play? (Y/n)
y ↵
Great! Starting a new game...

   |   |   
-----------
   |   |   
-----------
   |   |   

Please select a square by entering 1-9, 1 for the top left and 9 for the bottom right:

```
*↵ is a Carriage Return symbol and simply means the "Enter" key was pressed. It is not literal. In the line above it is used to mean that the user entered in the `y` character at an input prompt and then pressed enter.*

For more complex interactions, the CLI must inform the user about the custom input prompt, just like in the example above: `Please select a square by entering 1-9, 1 for the top left and 9 for the bottom right:`. We just tell the player to enter a number, 1 through 9, to represent the square.

```
$ bin/tictactoe

Hi! Welcome to Command Line Tic Tac Toe! Would you like to play? (Y/n)
y ↵
Great! Starting a new game...

   |   |   
-----------
   |   |   
-----------
   |   |   

Please select a square by entering 1-9, 1 for the top left and 9 for the bottom right:
5↵

 O |   |   
-----------
   | X |   
-----------
   |   |   

Please select a square by entering 1-9, 1 for the top left and 9 for the bottom right:
7↵

 O |   |   
-----------
   | X |   
-----------
 X |   |   
```
*Etc...*

That is a simple CLI interface pattern. Whenever you ask the user for input, you will need to:

1. Prompt the user for input: `Would you like to play? (Y/n)`
2. Define the input interface: `Please select a square by entering 1-9, 1 for the top left and 9 for the bottom right:`
3. Accept user input by yielding to a prompt and waiting patiently for the user to press enter. *If the user never enters anything, the program will wait at this state forever until the process is otherwise terminated.*
4. Take the user input and execute the appropriate sub-routine or procedure that represents that feature.

Another pattern is to provide your CLI with a [main program loop](https://github.com/learn-co-curriculum/cli-interfaces-readme#program-loop) so that it can provide a bigger set of menus and features.

<p data-visibility='hidden'>View <a href='https://learn.co/lessons/ruby-cli-applications-readme' title='Building CLI Applications in Ruby'>Building CLI Applications in Ruby</a> on Learn.co and start learning to code for free.</p>
