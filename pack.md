# Pack this src for release deployment
```sh
cd src/
dotnet restore
dotnet build --configuration Release
dotnet pack --configuration Release
```

# Publishing the NuGet packages
```sh
cd src/bin/Release
dotnet nuget push *.nupkg -k [guid] -s "https://www.nuget.org/api/v2/package"
dotnet nuget push *.nupkg -k "25c72166-0112-476a-8c27-ae4053e45bac" -s "https://www.nuget.org/api/v2/package"
```