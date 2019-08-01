+++
title = "Containerization Vs Virtualization"
featured = true
publishDate = 2019-07-20

# View.
#   1 = List
#   2 = Compact
#   3 = Card
view = 3

+++

## Containerization :
Containerization is a lightweight alternative to full machine virtualization that involves encapsulating an application in a container with its own operating environment.
Containers use the same host operating system (OS) repeatedly, instead of installing an OS for each guest VM.

## Virtualization : 
A virtual machine is a copy of a complete server basically it has its own OS which is treated as a guest OS on host OS.

![Example image](/img/containerization-vs-virtualization.png)

### Use case of Containers : 
Suppose we have two applications written on different versions of same language.It is possible that if we deploy both on same VM, one of those may break due to unsupported version of language.But if we deploy them in Containers,every container will have the required version and both apps will run in isolated environments.


![Example image](/img/use-case.png)

### Security Level : 

Virtual Machines are fully isolated and hence more secure. But in case of containers, process-level isolation and hence less secure.