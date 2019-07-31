+++
title = "Scala Part-1"
publishDate = 2019-06-19
subtitle = "What is SBT?"


# View.
#   1 = List
#   2 = Compact
#   3 = Card
view = 3

+++

SBT is a popular tool for compiling, running, and testing Scala projects of any size. Using a build tool such as sbt (or Maven/Gradle) becomes essential once you create projects with dependencies or more than one code file.

When you write small programs that consist of only one, or just two or three source files, then it's easy enough to compile those source files by typing scalac MyProgram.scala in the command line.

But when you start working on a bigger project with dozens or maybe even hundreds of source files, then it becomes too tedious to compile all those source files manually. You will then want to use a build tool to manage compiling all those source files.

sbt is such a tool. There are other tools too, some other well-known build tools that come from the Java world are Ant and Maven.

How it works is that you create a project file that describes what your project looks like; when you use sbt, this file will be called build.sbt. That file lists all the source files your project consists of, along with other information about your project. Sbt will read the file and then it knows what to do to compile the complete project.

Besides managing your project, some build tools, including sbt, can automatically manage dependencies for you. This means that if you need to use some libraries written by others, sbt can automatically download the right versions of those libraries and include them in your project for you.

Let’s look at how to use published libraries to add extra functionality to our apps.

Open up build.sbt and add the following line:
libraryDependencies += "org.scala-lang.modules" %% "scala-parser-combinators" % "1.1.0"

Here, libraryDependencies is a set of dependencies, and by using +=, we’re adding the scala-parser-combinators dependency to the set of dependencies that sbt will go and fetch when it starts up. Now, in any Scala file, you can import classes, objects, etc, from scala-parser-combinators with a regular import.
