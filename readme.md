# 🚀 Photino.Blazor Desktop App Template (.NET 9)

This repository provides a straightforward template and setup guide for creating desktop applications using **Photino.Blazor** with **.NET 9**, including support for the **MudBlazor** UI framework.

---

## 📌 Prerequisites

Make sure you have:

- [.NET 9 SDK](https://dotnet.microsoft.com/download/dotnet/9.0)
- [Visual Studio Code](https://code.visualstudio.com/) or [Visual Studio](https://visualstudio.microsoft.com/)

---

## ⚙️ Initial Project Setup

Follow these steps to initialize your **Photino.Blazor** project:

### **Step 1: Create a Blazor Project**

Open a terminal and run:

```bash
dotnet new blazor -n Photino.Blazor.net9_template
```

### **Step 2: Install Photino.Blazor**

Add the Photino.Blazor NuGet package:

```bash
dotnet add package Photino.Blazor
```

---

## 📂 Project Configuration

### **Step 3: Add Minimal `index.html`**

Create a new file at:

```bash
wwwroot/index.html
```

Add the following content:

```html
<!DOCTYPE html>
<html>
<head>
</head>
<body>
    <app>Loading...</app>
    <script src="_framework/blazor.webview.js"></script>
</body>
</html>
```

### **Step 4: Update `App.razor`**

Remove this line from `App.razor` if present:

```html
<script src="_framework/blazor.web.js"></script>
```

### **Step 5: Update `.csproj` File**

Update your project file (`.csproj`) as follows:

```xml
<Project Sdk="Microsoft.NET.Sdk.razor">

  <PropertyGroup>
    <OutputType>WinExe</OutputType>
    <TargetFramework>net9.0</TargetFramework>
    <Nullable>enable</Nullable>
    <ImplicitUsings>enable</ImplicitUsings>
  </PropertyGroup>

  <ItemGroup>
    <Content Update="wwwroot\**">
      <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
    </Content>
  </ItemGroup>

  <ItemGroup>
    <PackageReference Include="Photino.Blazor" Version="4.0.13" />
  </ItemGroup>

</Project>
```

---

## 🛠️ Application Setup

### **Step 6: Update `Program.cs`**

Replace your `Program.cs` file contents with:

```csharp
using Microsoft.Extensions.DependencyInjection;

namespace Photino.Blazor.net9_template
{
    class Program
    {
        [STAThread]
        static void Main(string[] args)
        {
            var appBuilder = PhotinoBlazorAppBuilder.CreateDefault(args);

            appBuilder.Services.AddLogging();

            appBuilder.RootComponents.Add<App>("app");

            var app = appBuilder.Build();

            app.MainWindow.SetTitle("Photino Blazor Sample");

            AppDomain.CurrentDomain.UnhandledException += (sender, error) =>
            {
                app.MainWindow.ShowMessage("Fatal Exception", error.ExceptionObject.ToString());
            };

            app.Run();
        }
    }
}
```

---

## 🧹 Cleanup & Adjustments

### **Step 7: Remove Server-side Directives**

- Remove `@rendermode InteractiveServer` from `Counter.razor`.
- Remove `@attribute [StreamRendering]` from `Weather.razor`.

### **Step 8: Final Project Adjustments**

- Ensure `.csproj` uses Razor SDK:

```xml
<Project Sdk="Microsoft.NET.Sdk.razor">
```

- Add the following using directive in `Program.cs`:

```csharp
using Microsoft.Extensions.DependencyInjection;
```

- Delete unnecessary files:

  - `./Components/Pages/Error.razor`
  - Remove `<ImportMap />` from `./Components/App.razor`

---

## 🎨 MudBlazor Integration (Optional)

To enhance your app with the **MudBlazor UI Framework**, follow these steps:

### **Install MudBlazor**

```bash
dotnet add package MudBlazor
```

### **Add Imports**

Add the following line to your `./Components/_Imports.razor`:

```razor
@using MudBlazor
```

### **Include Styles and Scripts**

In your HTML `<head>` section (`./Components/App.razor`), add:

```html
<link href="https://fonts.googleapis.com/css?family=Roboto:300,400,500,700&display=swap" rel="stylesheet" />
<link href="_content/MudBlazor/MudBlazor.min.css" rel="stylesheet" />
```

At the end of the HTML `<body>` section, add the MudBlazor JS script:

```html
<script src="_content/MudBlazor/MudBlazor.min.js"></script>
```

### **Register MudBlazor Services**

Update `Program.cs` by adding:

```csharp
using MudBlazor.Services;

// Add MudBlazor services
appBuilder.Services.AddMudServices();
```

### **Update MainLayout**

In your `MainLayout.razor`, include these providers:

```razor
@* Required Providers *@
<MudThemeProvider />
<MudPopoverProvider />

@* Optional Providers *@
<MudDialogProvider />
<MudSnackbarProvider />
```

---

## ▶️ Running Your Application

Launch your application using:

```bash
dotnet run

dotnet publish -c Release

dotnet publish -c Release -p:PublishReadyToRun=true
```

Your Photino.Blazor desktop app should now be up and running!

---

## 📚 Helpful Resources

- [Photino.Blazor GitHub](https://github.com/tryphotino/photino.Blazor)
- [MudBlazor Documentation](https://mudblazor.com/)
- [Blazor Documentation](https://learn.microsoft.com/en-us/aspnet/core/blazor)
- [.NET 9 Official Site](https://dotnet.microsoft.com/)

---

Happy coding! 🚀✨
