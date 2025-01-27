# Setting up a dev container for Go

* Primary author: [Kibby Hyacinth Pangilinan](https://github.com/hyacinp)

* Reviewer: [Tracy Dang](https://github.com/tmndang)

## Objective

This tutorial aims to teach you how to set up a project from sratch in the Go Programming Language!

## Prerequisites

In order to move forward with this tutorial you must have the following completed:

* Install Docker
* Instal the text editor Visual Studio Code (VSCode)
* Install Git
* Create a GitHub account

**Inspiration taken from COMP 423's ["Starting a Static Website Project with MkDocs"](https://comp423-25s.github.io/resources/MkDocs/tutorial/)**


## Setting Up Your Local and Remote Repositories

### Step 1. Create a Local Directory and Initialize Git

1) Open up your terminal on VSCode <br>
2) Create a new directory for your project using the ```mkdir```
 command and switch into your directory by using the ```cd``` command. 

```
mkdir go-tutorial-project
cd go-tutorial-project
```
3) Now, initialize a new git repository for your project:

```
git init
```

4) Create a README file for your directory and stage and commit the changes to your new repo!

```
echo "# My first Go Project" > README.md
git add README.md
git commit -m "Initial commit with README"
```

### Step 2: Create a Remote Repo on GitHub

1) Log into your GitHub account and [create a new repository](https://github.com/new)

2) When setting up your repository: <br>

* Name the repository as ```go-tutorial-project```
* In the description you can write: "Go project organized as a static website using Material for MkDocs."
* Set the visibility to **public** <br>

3) Do **NOT** initialize the repository with a README, .gitignore, or license. 

4) Create your remote repository by pressing on "Create Repository"

### Step 3: Time to Link your Local Repo to your Remote Repo on Github!

1) Inside your project in VSCode, add your remote GitHub repository as the corresponding remote repository
```
git remote add origin https://github.com/<your-username>/go-tutorial-project.git
```
**Make sure to replace ```<your-username>``` with the username associated with your GitHub!**

2) Ensure that your default branch is main by using the ```git branch``` command. If not, then use this command: ```git branch -M main```

3) Push your changes to your remote repository. Since this will be your first push to your remote repo, you will need to specify the upstream using the followung command:
```
git push --set-upstream origin main
```

4) To ensure that you have pushed your changes successfully, go back to your web browser to refresh your remote GitHub repo. If the above steps have been done successfully, you should be able to see the same commit you pushed from your local repo to your remote!

!!! note 

     If you experience any issues, it is always handy to use ```git status``` to display the state of your working directory and the staged changes. Use ```git log``` to debug!

## Time to Set up your Dev Container!

**In your ```go-tutorial-project``` directory on VSCode:**

1. Navigate to the left sidebar
2. Click on the extensions tab
3. Search for the "Dev Containers" extension and download that in VSCode

1) Create a ```.devcontainer``` directory in the root of your project folder. Inside this new directory, add the file ```devcontainer.json```
2) Within the file ```devcontainer.json```, paste the following text in order to configure your dev environment:
```
{
  "name": "Go Tutorial Project",
  "image": "mcr.microsoft.com/vscode/devcontainers/go:latest",
  "customizations": {
    "vscode": {
      "settings": {},
      "extensions": ["golang.go"]
    }
  },
  "postCreateCommand": "go mod init go-tutorial-project"
}
```

Let's break down what you have just put into that file:

* ```name``` refers to the name of your container
* ```image``` is a base image of muicorsoft associated with Go.
* ```customizations``` is where we install VSCode's Go plugin, essentially configuring VSCode
* ```postCreateCommand``` a command to run once the container is created. Here, we are initializing a go.mod file and install go


!!! note

     We do not have to run `go mod` because postCreateCommand does this for us. When it does run `go mod` for us, it creates the `go.mod` file which is responsible for managing go dependencies.

### Reopen your Project in your Dev Container

1. Press `Ctrl+Shift+P` or on Mac `Cmd+Shift+P`
2. Search and select **Dev Containers: Reopen Container**
3. Now wait for the container to build and start. This might take some time as the image gets downloaded and the requirements get installed

### Verifying the Go Installation

After reopening your conatiner, run `go version` to see the version of Go that you have!

!!! note 

     If you do not see a number corresponding to the version of your Go, or if yu receive an error, go over the steps of setting up your container again and ensure that you have completed them correctly.

If the above steps have been done successfully, then you have officially created your Go dev container! YAY!

## Writing a Basic First Go Program and Running it!

### Step 1: Writing your Program

* In your project's root directory, create your first file, we can name it `first-go-prog.go`
* In this new file, add the following:
```
package main

import "fmt"

func main() {
    fmt.Println("Hello COMP423!")
}
```
Let's breakdown what everything means from the above step:

* `package main` declares a main package that has all the files in the same directory
* `import fmt` imports a standard Go library package
* `func main()` is the main function that is executed when you run the program. When executed, it prindts out "Hello COMP423!"

### Step 2: Building and Running Your Program

**Few things to note:**

* `go run` compiles and runs your program **temporarily** and requires a Go envrionment. This command is more useful for running Go programs to quickly see the output.

* `go build` does not require a Go environment and compiles your program where an executable object file is created, containing all dependencies. 

* In short, `go run` compiles and runs your program in one step, `go build` requires two steps.


1) Once your file is saved, you have two options in running your program

(A) In your VSCode terminal, run
    ```
    go run first-go-prog.go
    ```

or

(B) Build an executable by entering the following commands:
```
go build -o <meaningful-output-name> first-go-prog.go
./<meaningful-output-name>
```

**Using the command `./<meaningful-output-name>` runs the compiled file created by the `go build` command.**

!!! note 

     After running your program, you should see the following output:
     ```
     Hello COMP423!
     ```
    
## Pushing your Changes to your Remote GitHub Repo

Once you have made your changes, you can push your edits to your remote repo! To do so you must:

1. Stage all the changes you have made by using this command:
```
git add .
```
2. Commit your changes and give a meaningful message explaining what you are committing/the changes that you have made.
```
git commit -m "<meaningful message here>>"
```
3. Push your committed changes to your remote repo
```
git push origin main
```
4. Navigate to your Github repo and refresh the page to see if your commits have been successfully pushed.

## Done!

And that's it! You have successfully set up local and remote repositories, set up your Go dev container and have written and ran your first Go program! Congrats!

### References
[1] K. Jordan, “Starting a static website project with MkDocs,” COMP423, https://comp423-25s.github.io/resources/MkDocs/tutorial/ (accessed Jan. 26, 2025).




