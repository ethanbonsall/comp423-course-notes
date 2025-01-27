# Setting up a dev container for Rust

* Primary author: [Ethan Bonsall](https://github.com/ethanbonsall)
* Reviewer: [Kasra Zamani](https://github.com/Kasra84)

## What You Will Learn
### By completing this tutorial, you will:

1. Set up a basic Rust Development Container in VS Code to streamline development.
2. Create a basic Rust program
3. Gain insight into the tools and practices used in open-source and professional software projects.

## Prerequisites
### Before we dive in, make sure you have:

1. A GitHub account: If you don’t have one yet, sign up at [GitHub](https://github.com/).
2. Git installed: [Install Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) if you don’t already have it.
3. Visual Studio Code (VS Code): Download and install it from [here](https://code.visualstudio.com/).
4. Docker installed: Required to run the dev container. [Get Docker here](https://www.docker.com/products/docker-desktop/).
5. Command-line basics

## Part 1. Project Setup: Creating the Repository
### Step 1. Create a Local Directory and Initialize Git
#### (A) Open your terminal or command prompt.

#### (B) Create a new directory for your project. (Note: Of course, if you'd like to organize this tutorial somewhere else on your machine, go ahead and change into that parent directory first. By default this will be in your user's home directory.):


```
mkdir rust-tutorial
cd rust-tutorial
```

#### (C) Initialize a new Git repository:

`git init`

#### D) Create a README file:


```
echo "# Rust Tutorial" > README.md
git add README.md
git commit -m "Initial commit with README"
```
### Step 2. Create a Remote Repository on GitHub
#### (1) Log in to your GitHub account and navigate to the Create a New Repository page.

#### (2) Fill in the details as follows:

- Repository Name: Rust Tutorial
- Description: "Tutorial to setup a rust container."
- Visibility: Public

#### (3) Do not initialize the repository with a README, .gitignore, or license.

#### (4) Click Create Repository.

### Step 3. Link your Local Repository to GitHub
#### (1) Add the GitHub repository as a remote:


`git remote add origin https://github.com/<your-username>/rust-tutorial.git`
!!! info "Replace <your-username> with your GitHub username."

#### (2) Check your default branch name with the subcommand git branch. If it's not main, rename it to main with the following command: git branch -M main. Old versions of git choose the name master for the primary branch, but these days main is the standard primary branch name.

#### (3) Push your local commits to the GitHub repository:


`git push --set-upstream origin main`

#### (4) Back in your web browser, refresh your GitHub repository to see that the same commit you made locally has now been pushed to remote. You can use git log locally to see the commit ID and message which should match the ID of the most recent commit on GitHub. This is the result of pushing your changes to your remote repository.

## Part 2. Setting Up the Development Environment

### Step 1. Add Development Container Configuration
- In VS Code, open the rust-setup directory. You can do this via: File > Open Folder.
- Install the Dev Containers extension for VS Code.
- Create a .devcontainer directory in the root of your project with the following file inside of this "hidden" configuration directory:
- .devcontainer/devcontainer.json

#### The devcontainer.json file defines the configuration for your development environment. Here, we're specifying the following:

- name: A descriptive name for your dev container.
- image: The Docker image to use, in this case, the latest version of a Rust environment. Microsoft maintains a collection of base images for many programming language environments, but you can also create your own!
- customizations: Adds useful configurations to VS Code, like installing the Rust extension. When you search for VSCode extensions on the marketplace, you will find the string identifier of each extension in its sidebar. Adding extensions here ensures other developers on your project have them installed in their dev containers automatically.
- postCreateCommand: A command to run after the container is created. In our case, it will use pip to install the dependencies listed in requirements.txt.

```
{
  "name": "Rust Tutorial",
  "image": "mcr.microsoft.com/devcontainers/rust:latest",
  "customizations": {
    "vscode": {
      "settings": {},
      "extensions": ["rust-lang.rust-analyzer"]
    }
  }
}
```
### Step 2. Reopen the Project in a VSCode Dev Container

Reopen the project in the container by pressing Ctrl+Shift+P (or Cmd+Shift+P on Mac), typing "Dev Containers: Reopen in Container," and selecting the option. This may take a few minutes while the image is downloaded and the requirements are installed.

Once your dev container setup completes, close the current terminal tab (trash can), open a new terminal pane within VSCode, and try running rustc --version to see your dev container is running a recent version of Rust without much effort! (As of this writing: 1.84.0 released in January of 2025.)

### Step 3: Create a New Rust Binary Project

To create a new Rust binary project inside your development container, use the `cargo new` command. By default, `cargo new` initializes a new Git repository for your project, but since you may already be managing version control separately or do not need a repository at this point, you can disable this behavior with the `--vcs none` flag.

Here’s how to do it:

1. Open the terminal in VS Code (inside your dev container).
2. Run the following command to create a new Rust binary project:

`cargo new hello_comp423 --vcs none`

3. Navigate to your new project directory:
`cd hello_comp423`

### Step 4: Write a New Rust Program 

- Open the src/main.rs file in your project. This file is the main entry point for your Rust application.

**Replace the contents of the file with the following code:**

```
fn main() {
    println!("Hello COMP423");
}
```
!!! info "This program defines a main function that prints the string "Hello COMP423" to standard output"


### Step 5: Compile the Program
In the terminal, ensure you are in the project directory (hello_comp423).

**Run the following command to compile your program:**

To compile your program, use the cargo build command:

`cargo build`

This command compiles your project and generates an executable file in the target/debug directory. The path to the compiled binary will look something like this:

`target/debug/hello_comp423`

You can run the compiled file directly by typing:

`./target/debug/hello_comp423`

You should see the output:

`Hello COMP423`

#### Comparison with gcc in COMP211:

<table><tr><td>With gcc, you typically compile a file using a command like gcc program.c -o program, which produces an executable named program.
In Rust, cargo build handles both the compilation and linking steps for you, placing the output in a default directory structure.</td></tr></table>

### Step 6: Run the Program
**Instead of building and running the file separately, you can use the cargo run command, which combines both steps:**

`cargo run`

**This command compiles the program (if necessary) and immediately runs the executable. The output will look like this:**

`Hello COMP423`

|Difference Between cargo build and cargo run:|
|---------------------------------------------|
|cargo build: Only compiles the program and creates the executable in target/debug. You must run the executable manually.|
|cargo run: Compiles the program (if needed) and runs it immediately.|

!!! success "Congratulations! You've successfully created, written, compiled, and run a Rust program that prints "Hello COMP423" inside a Dev Container."
