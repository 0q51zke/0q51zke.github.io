+++
title = "Unpacking a ConfuserEx Mod"
date = "2022-04-27T13:08:30+02:00"
description = "Solving a .NET UnPackMe protected with a ConfuserEx Mod."

tags = ["unpackme", "confuserex", ".net"]
+++

You can find the related *Tuts 4 You* topic [here](https://forum.tuts4you.com/topic/39422-confuserex-v10-modded/) or at the [archive](https://web.archive.org/web/20220427112412/https://forum.tuts4you.com/topic/39422-confuserex-v10-modded/).

---

### TODOs before publishing

- **POSTPONED** Building the version with VS2022 (Requires porting to .NET Framework 4.8) 
- Checkout every configuarble obfuscation method on its own -> Build deobfuscator for each
- Compare the PE Stub of the outputs
- Compare the IL of the outputs
- Combine all of these tools to make a dynamic unpacker for ConfuserEx v1.0.0
- Check if they work on the modded version -> adjust them to solve the modded version (maybe introduce a plugin system)
- Extra - Build a tool to compare .net executables on IL level

### Introduction

As this is the first post regarding any ConfuserEx unpacking on the blog, it will go further into the inner workings of the original ConfuserEx and developing of required tooling, because I won't use any of the popular CodeCracker tooling to enhance the learning experience.

### Question

How far differntiates the original ConfuserEx to the modded Version used in this UnpackMe?
To solve this question we first need to get a baseline understanding of the ConfuserEx version used as the foundation of the mod.
This means writing a basic UnPackMe that is packed with that version. And later build up a tooling suite to unpack it.

### Hypothesis

After we aquired this foundational knowledge and tooling, we can proceed in adapting the tooling to unpack the modded version.
That should give us insight in the specific differntiations between the original and the mod and enable us to solve the UnPackMe that is provided
in the *Tuts 4 You* topic.

### Experiment

#### Downloading ConfuserEx v1.0.0

First we need to aquire the correct ConfuserEx version from [GitHub](https://github.com/yck1509/ConfuserEx/releases/tag/v1.0.0).

To clone the project including dnlib as a submodule enter the following commands into your shell.
The last one is required to get the correct version of ConfuserEx.

```console
PS C:\> git clone https://github.com/yck1509/ConfuserEx.git
PS C:\> cd ConfuserEx/
PS C:\> git submodule update --init --recursive
PS C:\> git checkout tags/v1.0.0
```

When we open the project in Visual Studio for the first time we can ignore the popup that wants us to port the projects to the newest installed .NET Framework version,
as the code is only required to get insight in the inner workings. Building the solution is not necessary as an compiled version is provided in the release section of the repository.

In the next step we download the mentioned [package](https://github.com/yck1509/ConfuserEx/releases/download/v1.0.0/ConfuserEx_bin.zip).

#### Coding a minimal CLI CrackMe

Now we need to program a simple CrackMe suited for demonstration purposes.
Thanks to the new .NET release we don't need any top-level statemants, so this adventure can be achieved in a few lines of code.
Feel free just to copy & paste and compile the following snippet if you want to follow along.

```csharp
Console.WriteLine("EasyCrackMe");
Console.Write("\nEnter a passphrase: ");

string? input;
input = Console.ReadLine();

while(input == null)
{
    Console.WriteLine("\nEnter a passphrase:");
    input = Console.ReadLine();
}

if (input.Equals("easy"))
{
    Console.WriteLine("Solved!");
}
```



### Observation

### Analysis

### Conclusion

---

General tooling used:

---

#### Credits:

[Washi](https://github.com/Washi1337/) For his work on AsmResolver.