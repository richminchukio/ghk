## steps to add dotnet bundler to any project
```sh
dotnet add package BuildBundlerMinifier
```

# Pack this src for release deployment
```sh
cd src/
dotnet restore
dotnet build --configuration release
dotnet pack -c release
```

# Publishing the NuGet package
```sh
cd src/bin/release
dotnet nuget push *.nupkg -k [guid] -s "https://www.nuget.org/api/v2/package"
```