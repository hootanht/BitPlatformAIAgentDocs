# Bit BlazorUI Theming Reference

**Purpose:** This document serves as a reference guide for an AI assistant regarding the theming capabilities of the `bit BlazorUI` library. It covers concepts, setup, customization methods (CSS variables, C# ThemeManager, JS API), and specific features like system theme detection and persistence.

---

## Theming

In `bit BlazorUI`, you can customize the look and feel of your app using the theme features by specifying the color of the components, the darkness of the surfaces, the level of shadow, the appropriate opacity of elements, etc.

Different aspects of the UI element styles are pre-defined in CSS variables that let you apply a consistent tone to your app. It allows you to customize all design aspects of your project to meet the specific needs of your business or brand.

The default theme is based on the Microsoft Fluent design system with light and dark theme types available to choose from. By default, components use the light theme type.

---

## Quick setup

To get started with `bit BlazorUI Theme` as fast as possible, you can try the `system theme` feature of it.

First you need to register the `bit BlazorUI services` as follows:

```csharp
// In Program.cs or equivalent startup configuration
builder.Services.AddBitBlazorUIServices();
```

And then add a specific attribute named `bit-theme-system` to the `html` tag (usually in `App.razor` or `_Host.cshtml`/_Layout.cshtml):

```cshtml
<html bit-theme-system>
  ...
</html>
```

Now with this setup, the app will follow the system theme (dark or light) automatically.

---

## CSS variables

All CSS variables defined in the Theme system of the `bit BlazorUI` are attached to the root element (`:root`) and scoped using the `bit-theme` attribute.

Here's an example snippet showing primary color variables for the default light/fluent theme:

```css
:root,
:root[bit-theme="light"],
:root[bit-theme="fluent"],
:root[bit-theme="fluent-light"] {

/* ... other variables ... */

    --bit-clr-pri: #1A86D8; /* Primary color */
    --bit-clr-pri-hover: #197FCD; /* Primary color on hover */
    --bit-clr-pri-active: #1779C2; /* Primary color when active/pressed */
    --bit-clr-pri-dark: #096FBD; /* Darker shade of primary */
    --bit-clr-pri-dark-hover: #0969B4; /* Darker shade on hover */
    --bit-clr-pri-dark-active: #0864AA; /* Darker shade when active */
    --bit-clr-pri-light: #A3CFEF; /* Lighter shade of primary */
    --bit-clr-pri-light-hover: #8CC3EC; /* Lighter shade on hover */
    --bit-clr-pri-light-active: #76B6E8; /* Lighter shade when active */
    --bit-clr-pri-text: #FFF; /* Text color for primary backgrounds */

/* ... other variables ... */

}
```

The source code of these CSS variables is available in the [bit BlazorUI GitHub repo (Styles/Fluent)](https://github.com/bitfoundation/bitplatform/blob/main/src/BlazorUI/Bit.BlazorUI/Styles/Fluent).

You can simply override these values in your own CSS/SCSS file to customize the UI. For example, to customize the dark theme for the `bitplatform.dev` website, overrides are applied like this ([source file](https://github.com/bitfoundation/bitplatform/blob/develop/src/Websites/Platform/src/Bit.Websites.Platform.Client/Styles/app.scss)):

```css
/* overridden values for the dark theme: */

:root[bit-theme="dark"] {
    --bit-clr-sec: transparent; /* Secondary color */
    --bit-clr-sec-hover: #061342; /* Secondary hover */
    --bit-clr-bg-pri: #060E2D; /* Primary background */
    --bit-clr-bg-sec: #0a153d; /* Secondary background */
    --bit-clr-bg-pri-hover: #07154a; /* Primary background hover */
    --bit-clr-bg-pri-active: #061241; /* Primary background active */
    --bit-clr-bg-sec-hover: #07154a; /* Secondary background hover */
    --bit-clr-fg-sec: #dddddd; /* Secondary foreground (text) */
}
```

**Note:** If you're using `scss` in your project, you can use the `_bit-css-variables.scss` file which introduces scss variables for each bit theme css variable. This makes overriding easier within SCSS workflows. You can find the latest version of this file [here](https://github.com/bitfoundation/bitplatform/blob/main/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Styles/abstracts/_bit-css-variables.scss).

---

## ThemeManager

The `BitThemeManager` class provides a C# API to interact with and customize the theme dynamically.

First, ensure the services are registered (as shown in Quick Setup):

```csharp
builder.Services.AddBitBlazorUIServices();
```

Then, inject `BitThemeManager` into your Blazor component or service:

```csharp
@inject BitThemeManager _bitThemeManager
```

Or in C# code-behind:

```csharp
[Inject] private BitThemeManager _bitThemeManager { get; set; } = default!;
```

You can use the following methods:

1. **`ApplyBitThemeAsync(BitTheme theme, ElementReference? element = null)`**: Applies custom theme values defined in a `BitTheme` object. If `element` is null, it applies to the `body`.

    ```csharp
    var myTheme = new BitTheme();
    myTheme.Color.Foreground.Primary = "#111111"; // Example: Change primary text color
    myTheme.Color.Background.Primary = "#777777"; // Example: Change primary background color
    await _bitThemeManager.ApplyBitThemeAsync(myTheme);
    ```

2. **`SetThemeAsync(string themeName)`**: Sets the current theme by its name (e.g., "light", "dark", "fluent-dark", or custom names).

    ```csharp
    await _bitThemeManager.SetThemeAsync("fluent-dark");
    ```

3. **`ToggleDarkLightAsync()`**: Toggles the current theme between its light and dark variants (based on configured theme names). Returns the name of the new theme.

    ```csharp
    string newTheme = await _bitThemeManager.ToggleDarkLightAsync();
    Console.WriteLine($"Theme changed to: {newTheme}");
    ```

4. **`GetCurrentThemeAsync()`**: Returns the name of the currently active theme.

    ```csharp
    var currentTheme = await _bitThemeManager.GetCurrentThemeAsync();
    Console.WriteLine($"Current theme is: {currentTheme}");
    ```

---

## System Theme Detection

To make the application automatically use the operating system's preferred theme (light or dark) on initial load, add the `bit-theme-system` attribute to the `html` tag:

```cshtml
<html bit-theme-system>
  ...
</html>
```

If both `bit-theme-system` and `bit-theme-default` are set, `bit-theme-system` takes precedence. If the user manually changes the theme later using `SetThemeAsync` or `ToggleDarkLightAsync`, the system preference is overridden for the session (unless persistence is also enabled).

---

## Persist Theme Selection

To save the user's selected theme (or the system-detected theme if `bit-theme-system` is used) in the browser's local storage and automatically apply it on subsequent visits, add the `bit-theme-persist` attribute to the `html` tag:

```cshtml
<html bit-theme-persist>
  ...
</html>
```

This uses a local storage key (e.g., `bit-theme`) to remember the last active theme name.

---

## Default Theme

If you don't use `bit-theme-system`, the default theme is `light`. You can change this initial default theme by setting the `bit-theme-default` attribute on the `html` tag:

```cshtml
<html bit-theme-default="dark">
  ...
</html>
```

This sets the theme to "dark" when the application first loads, unless overridden by `bit-theme-system` or a persisted theme from `bit-theme-persist`.

---

## Customizing Theme Names

The default names used for toggling and identification are `light` and `dark`. You can customize these names using attributes on the `html` tag, which is useful if you define custom themes (e.g., "mycorp-light", "mycorp-dark").

```cshtml
<html bit-theme-dark="custom-dark" bit-theme-light="custom-light">
  ...
</html>
```

Now, `ToggleDarkLightAsync` will switch between "custom-light" and "custom-dark", and `GetCurrentThemeAsync` will return these names.

---

## CSS in C# (`BitCss` class)

The static `BitCss` class provides strongly-typed access to theme-related CSS class names and variable names within your C# code (Razor or code-behind). This avoids magic strings.

* **`BitCss.Class`**: Access predefined CSS class names.
  * Example: Applying background and foreground color classes to the body.

    ```cshtml
    <body class="@BitCss.Class.Color.Background.Primary @BitCss.Class.Color.Foreground.Primary">
        ...
    </body>
    ```

* **`BitCss.Var`**: Access theme CSS variable names (including the `--` prefix).
  * Example: Using a theme variable for a border color in an inline style.

    ```cshtml
    <div style="border: 1px solid var(@BitCss.Var.Color.Border.Secondary)">
        Hello world!
    </div>
    ```

This class reflects the structure of the theme variables (Color, Shape, Shadow, Typography, ZIndex).

---

## ThemeProvider Component

The `BitThemeProvider` component allows you to apply a specific `BitTheme` instance to a *part* of your UI tree, overriding the global theme for its children.

```cshtml
<BitThemeProvider Theme="myCustomThemeForThisSection">
    <BitCheckbox Label="Check me! (Uses custom theme)" />
</BitThemeProvider>

@code {
    BitTheme myCustomThemeForThisSection = new()
    {
        // Example: Make checkboxes red within this provider
        Color = { Primary = { Main = "red" } }
    };
}
```

Child components within a `BitThemeProvider` can access the applied theme instance via a cascading parameter:

```csharp
// Inside a child component
[CascadingParameter] public BitTheme? Theme { get; set; }

protected override void OnParametersSet()
{
    if (Theme is not null)
    {
        // Use the theme instance, e.g., Theme.Color.Primary.Main
    }
}
```

`BitThemeProvider` components can be nested. Inner providers override or merge with outer ones based on the properties set.

```cshtml
<BitThemeProvider Theme="outerTheme">
    <BitCheckbox Label="Check me! (Uses outer theme)" />

    <BitThemeProvider Theme="innerTheme">
        <BitCheckbox Label="Check me 2! (Uses inner theme)" />
    </BitThemeProvider>
</BitThemeProvider>

@code {
    BitTheme outerTheme = new() { Color = { Primary = { Main = "red" } } };
    BitTheme innerTheme = new() { Color = { Primary = { Main = "blue" } } }; // Overrides primary color
}
```

---

## JavaScript API (`BitTheme` object)

A global `BitTheme` JavaScript object is available for interacting with the theme system from JS. This is useful for integration with non-Blazor parts of an application or for advanced scenarios.

* **`BitTheme.get()`**: Returns the name of the current theme.

    ```javascript
    const currentTheme = BitTheme.get();
    console.log(currentTheme); // e.g., "dark"
    ```

* **`BitTheme.set(themeName)`**: Sets the current theme.

    ```javascript
    BitTheme.set('dark');
    ```

* **`BitTheme.toggleDarkLight()`**: Toggles between the configured dark and light themes.

    ```javascript
    BitTheme.toggleDarkLight();
    ```

* **`BitTheme.useSystem()`**: Applies the system's preferred theme (light or dark).

    ```javascript
    BitTheme.useSystem();
    ```

* **`BitTheme.onChange((newTheme, oldTheme) => { ... })`**: Registers a callback function that executes whenever the theme changes.

    ```javascript
    BitTheme.onChange((newTheme, oldTheme) => {
        console.log(`Theme changed from ${oldTheme} to ${newTheme}`);
        // Example: Update meta theme-color tag
        const metaThemeColor = document.querySelector("meta[name=theme-color]");
        if (metaThemeColor) {
            metaThemeColor.setAttribute('content', newTheme.includes('dark') ? '#0d1117' : '#ffffff');
        }
    });
    ```

* **`BitTheme.applyBitTheme(themeVariables, element?)`**: Applies a set of CSS variables to a specific DOM element (or `document.body` if omitted). The first argument is an object where keys are CSS variable names (e.g., `'--bit-clr-pri'`) and values are their desired settings.

    ```javascript
    const customStyle = { '--bit-clr-pri': '#FF00FF', '--bit-clr-pri-text': '#000000' };
    const myElement = document.getElementById('custom-section');
    BitTheme.applyBitTheme(customStyle, myElement);
    ```

* **`BitTheme.isSystemDark()`**: Returns `true` if the system preference is dark, `false` otherwise.

    ```javascript
    if (BitTheme.isSystemDark()) {
        console.log("System prefers dark mode.");
    }
    ```

* **`BitTheme.init(options)`**: Initializes the theme system from JavaScript, usually called early in the application lifecycle (e.g., in `_Host.cshtml` or `index.html`). This mirrors the functionality of the `html` tag attributes (`bit-theme-system`, `bit-theme-persist`, etc.) and allows setting an `onChange` handler programmatically during startup.

    ```javascript
    BitTheme.init({
        system: true,                 // Equivalent to bit-theme-system
        persist: true,                // Equivalent to bit-theme-persist
        default: 'custom-dark',       // Equivalent to bit-theme-default="custom-dark"
        darkTheme: 'custom-dark',     // Equivalent to bit-theme-dark="custom-dark"
        lightTheme: 'custom-light',   // Equivalent to bit-theme-light="custom-light"
        onChange: (newTheme, oldTheme) => { // Optional initial change handler
            console.log(`Initial theme set to ${newTheme}`);
            // ... perform actions on initial theme detection ...
        }
    });
    ```

---

## Feedback

* Provide feedback via the [bitplatform GitHub repo](https://github.com/bitfoundation/bitplatform) by filing an [Issue](https://github.com/bitfoundation/bitplatform/issues/new/choose) or starting a [Discussion](https://github.com/bitfoundation/bitplatform/discussions/new/choose).
* The source file for the original page this documentation is based on is [ThemingPage.razor](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/ThemingPage.razor). You can [review](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/ThemingPage.razor) or [edit](https://github.com/bitfoundation/bitplatform/edit/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/ThemingPage.razor) it there.
