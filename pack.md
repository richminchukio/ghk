# Pack this src for release deployment
```sh
cd src/
dotnet restore
dotnet build --configuration Release
dotnet pack --configuration Release
```

# Publishing the NuGet package
```sh
cd src/bin/Release
dotnet nuget push *.nupkg -k [guid] -s "https://www.nuget.org/api/v2/package"
```