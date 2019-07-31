+++
title = "Scala Part-2"
publishDate = 2019-06-20
subtitle = "Project Structure"


# View.
#   1 = List
#   2 = Compact
#   3 = Card
view = 3

+++

.idea/— contains IntelliJ’s project specific settings files. According to JetBrains, normally there is no need to edit the contents of this folder.

build.sbt — contains build definition of the project. For example, project name, project version, scalaVersion, libraryDependencies, etc. Note that this file is written in Scala.

project/—because build.sbt is written in Scala, we need to build build.sbt. Therefore, this folder contains all the files needed for building build.sbt.

project/build.properties — this file contains build definition of build.sbt. For example, it defines sbt version.

project/target/— contains artifacts from building build.sbt.

src/—this is where we put our source files. sbt uses the same directory structure as Maven for source files by default. Other directories in src/ will be ignored in build time.

src/main/scala — contains main .scala files

src/main/java — contains main .java files

src/main/resources — contains main files other than .scala/.java files

src/test/scala — contains test .scala files

src/test/java — contains test .java files

src/test/resources — contains test files other than .scala/.java files

target/— contains artifacts from building the project

println("Hello World")
Where should we chuck it?

Normally when you run a Scala sbt project, it will use the main function as the entry point to run the project. So another question — where should we chuck the main function?

Because sbt needs to call the main function from an object, the answer is that we write it in a Scala object like this:

object HelloWorldMain {
def main(args: Array[String]): Unit = {
println("Hello World")
}
}
So, let’s create a package called com.helloworld (alternatively you can use your domain name in reverse order) in src/main/scala.

Then right-click on the package and select New -> Scala Class. We will name the class HelloWorldMain. Before you click OK, remember to change Kind from Class to Object for the reason we mentioned earlier.

You can add the code snippet we discussed earlier in the file.

Build and Run the project
Now you should be able to see two green arrows next to your main function. Clicking either of them will build and run the project.

Then you will see the “Hello World” text printed out in the Run tool window in Intellij.

And the build artifact can be found in target/scala-2.12/classes.
