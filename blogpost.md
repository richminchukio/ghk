# 2017-04-09 - Creating a dotnet core NuGet Package

My name is Rich Minchuk. I’m developing an open source project called GHK. It’s based around a few simple concepts. 

1. Develop a tool that others can use - out of the box - to grow their own personal brand.
2. Use some brand new tech to show off what I’m learning while building it.
3. Make it unbelievably simple to install.
4. Rely on mostly free tools to bring exceptional value to users.

I’m opting for a streamlined approach to this blog and further blogs, so let’s dive right in. 

## Repo

Setup a GitHub account. If you don’t know Git, I’ll point you to my [read me](https://github.com/rjminchuk/Programming-Notes/blob/develop/md/git.md) makrdown file which contains a number of commands that may help get you started.

Once you have a GitHub account you have to create a repository in which your open source project can live. Once your repo is setup and you can push commits to it, we can move on. Github makes this all pretty easy, so excuse the brevity, this article is about nuget and not git.

Let's get setup in dotnet core if you aren’t already. I’m on a Mac so the commands and steps might be a little different for your OS flavor. These steps are as of `2017-04-09` using .net core version 1.4 (IE: after they went back to .csproj files). 

1. Install Visual Studio Code and its C# extension.
2. Install Homebrew from VSCode's terminal. Brew is a Package Manager for MacOS that can install neat and necessary things.
3. Go to Microsoft for explicit additional brew commands for setup (MacOS).
4. Exec Brew setup commands obtained from step 3. ASP.Net Core requires OpenSSL to work on MacOS. these steps ensure it's installed properly. You can pretty much forget about Brew now.
5. Navigate to your project folder. `cd ~/Source/my-nuget-project`
6. Make a directory for the NuGet package source of your project. i.e.: `mkdir src`
7. Open the folder we just created (src/) in VSCode. `none File > Open Folder`
8. Hit ```Control + ` ``` to open the terminal.
9. Exec `dotnet new classlib` in VSCode Terminal. 

Neat. You created a class library, and it’s definitely something someone else could totally use. Let’s `git commit -m "my class library initial commit"`

## Pack and Push

On to the meaty part. Getting your commands right for packing your NuGet package and pushing it up to nuget.org.

sh cd into your projects src/ directory

``` 
cd src/
dotnet restore
dotnet build --configuration Release
dotnet pack --configuration Release
ls bin/Release/
```

Neat. Ya packed it. Dotnet makes this all so very easy. NuGet is obviously a big part of the backbone to dotnet core so they probably wanted to make it this easy.

Go to nuget.org and create yourself an account... which is actually a Microsoft account. After you’re all logged in. Go to your profile. Scroll to the bottom, find the API Keys section, and click the button to generate an API Key. This is where it’ll ask you to confirm. Confirm your account, then get back to the same screen, and click to generate a new key.

1. Hit `"new API Key"`
2. Add a descriptive name for the key `"the key I use for my awesome new NuGet project."`
3. Check both `"Push"` and `"Unlist package"` checkboxes. 
4. Type the name of your csproj file into the `"Glob pattern"` field. IE: `"src"`
5. Realize that a NuGet project named `"src"` (the default name when we ran `dotnet new classlib`) has probably already been created before.
6. Change your csproj file’s name to something unique and re-run the packing steps.
7. Now change `"src"` to  `"*"` in the `"Glob pattern"` field. Cause hey, let’s be safe.
8. Hit `"Add Key"`
9. Click the icon to copy the key. It’s your last chance to do this so don’t close the window yet.

Ok. Now we have the key we need to push your NuGet package to nuget.org. open the terminal in vscode. `cd ../` then `pwd` to confirm you’re in your projects root directory. Then execute `touch my-nuget-key.md` 

Open that file up in vscode, paste your key into it. Hit save. Go back to your terminal and `touch .gitignore`

Open your .gitignore file and add the line `"my-nuget-key.md"` then `git commit -m "don’t show anyone my key not never!"`

Cool. I think we’re ready for the last and best steps. `cd src/bin/Release` then execute `dotnet nuget push *.nupkg --api-key [guid] --source "https://www.nuget.org/api/v2/package"`

BAM! You should be done. You created some code that other people can `dotnet add package [your package name]`

Super simple, now you’re ready to change the way people code with an awesome new open source project!
