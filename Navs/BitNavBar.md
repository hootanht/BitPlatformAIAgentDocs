<!--
AI Agent Reference File: BitNavBar Component

Purpose: This file provides detailed information about the Blazor `BitNavBar` component.
Use this reference when generating, analyzing, or modifying code involving BitNavBar.
Focus on its purpose (tab-like navigation), data binding methods (BitNavBarItem, Custom Generic, BitNavBarOption),
key properties (Mode, Items, SelectedItem, Templates, Styles), and event handling.
Note its similarity in API structure (especially data input) to BitNav, but its distinct visual presentation (horizontal tabs/bar).
-->

# BitNavBar Component Reference (Blazor)

## Overview

The `BitNavBar` component renders a navigation control that typically appears as a horizontal bar of selectable items (similar to tabs). It's commonly used for primary or secondary navigation within an application, often placed at the top or bottom of a view (like a bottom navigation bar in mobile apps).

It provides links or triggers actions associated with the main areas or sections of an application. Unlike `BitNav`, it does not display hierarchical structures; it's designed for a flat list of navigation items.

**Related Terms:** NavMenu, TabPanel

## Core Concepts: Multi-API Data Input

Like `BitNav`, `BitNavBar` offers flexibility in how navigation items are provided:

1.  **`List<BitNavBarItem>`:** Define a C# `List` where each element is an instance of the `BitNavBarItem` class. This class holds properties like `Text`, `Url`, `IconName`, `IsEnabled`, etc. This list is bound to the `Items` parameter.
2.  **Custom Generic Class (`List<TItem>`)**: Use your own custom C# class. Provide the `NameSelectors` parameter to map your class's properties (e.g., `Label`, `TargetUrl`) to the expected `BitNavBarItem` properties (`Text`, `Url`).
3.  **`BitNavBarOption` Component**: Define items declaratively within the `.razor` markup using `<BitNavBarOption>` components inside `<BitNavBar>`.

---

## Usage

### 1. Basic Usage with `BitNavBarItem` List

This is the standard method, binding a `List<BitNavBarItem>` to the `Items` parameter.

```razor
@* In your .razor file *@
<BitNavBar Items="BasicNavBarItems" />

@code {
    private static readonly List<BitNavBarItem> BasicNavBarItems = new()
    {
        new() { Text = "Home", IconName = BitIconName.Home, Url = "/" },
        new() { Text = "Products", IconName = BitIconName.ProductVariant, Url = "/products" },
        new() { Text = "Academy", IconName = BitIconName.LearningTools, Url = "/academy" },
        new() { Text = "Profile", IconName = BitIconName.Contact, Url = "/profile" }
    };
}
```

**Explanation:**

* A `List<BitNavBarItem>` named `BasicNavBarItems` holds the navigation data.
* Each `BitNavBarItem` represents a selectable navigation button/tab.
* Properties like `Text`, `IconName`, `Url`, `IsEnabled` define the item's appearance and behavior.
* The list is passed to the `Items` parameter of `<BitNavBar>`.

### 2. Usage with Custom Generic Class (`List<TItem>`)

Define your own class and use `NameSelectors` for property mapping.

```razor
@* In your .razor file *@
<BitNavBar Items="CustomNavItems" NameSelectors="CustomNameSelectors" />

@code {
    public class MyNavBarLink
    {
        public string DisplayName { get; set; }
        public string Href { get; set; }
        public string Symbol { get; set; } // Custom property for icon
        public bool IsActive { get; set; } // Could be used with manual selection
        public bool Clickable { get; set; } = true;
    }

    private static readonly List<MyNavBarLink> CustomNavItems = new() { /* ... populate list ... */ };

    // Define how MyNavBarLink properties map to BitNavBar expectations
    private static readonly BitNavBarNameSelectors<MyNavBarLink> CustomNameSelectors = new()
    {
        Text = { Name = nameof(MyNavBarLink.DisplayName) }, // Map DisplayName to Text
        Url = { Name = nameof(MyNavBarLink.Href) },         // Map Href to Url
        IconName = { Name = nameof(MyNavBarLink.Symbol) },  // Map Symbol to IconName
        IsEnabled = { Name = nameof(MyNavBarLink.Clickable) } // Map Clickable to IsEnabled
        // Key, Target, Title, etc., can also be mapped if needed.
    };
}
```

**Explanation:**

* A custom class `MyNavBarLink` stores the navigation details.
* `NameSelectors` maps properties like `DisplayName` (in `MyNavBarLink`) to `Text` (expected by `BitNavBar`).
* Allows using existing data models directly.

### 3. Declarative Usage with `BitNavBarOption`

Define items directly in the markup. Note that `BitNavBar` is typically flat, so nesting `<BitNavBarOption>` usually doesn't create sub-menus like in `BitNav`.

```razor
<BitNavBar>
    <BitNavBarOption Text="Files" IconName="@BitIconName.FabricFolder" Url="/files" />
    <BitNavBarOption Text="Shared" IconName="@BitIconName.Share" Url="/shared" />
    <BitNavBarOption Text="Recycle Bin" IconName="@BitIconName.RecycleBin" Url="/recyclebin" IsEnabled="false" />
    <BitNavBarOption Text="Settings" IconName="@BitIconName.Settings" Url="/settings" />
</BitNavBar>
```

**Explanation:**

* Items are defined using `<BitNavBarOption>` tags inside `<BitNavBar>`.
* Properties are set directly as attributes.
* This method is convenient for static or simple navigation structures defined directly in the view.

---

## Key Configurations & Features

### Navigation Mode (`Mode`)

Determines how item selection is visualized and handled.

* `BitNavMode.Automatic` (Default): `BitNavBar` highlights the item whose `Url` (or `AdditionalUrls`) matches the current browser URL via `NavigationManager`.
* `BitNavMode.Manual`: Selection highlighting is controlled externally. Use `DefaultSelectedItem` for initial selection or `@bind-SelectedItem` for two-way binding, often with `OnSelectItem`.

```razor
@* Manual mode with initial selection *@
<BitNavBar Items="BasicNavBarItems"
           Mode="BitNavMode.Manual"
           DefaultSelectedItem="BasicNavBarItems[0]" />

@* Manual mode with two-way binding *@
<BitNavBar Items="BasicNavBarItems"
           Mode="BitNavMode.Manual"
           @bind-SelectedItem="CurrentSelectedItem" />

<BitChoiceGroup Items="ChoiceGroupItems" @bind-Value="CurrentSelectedItem" Horizontal />

@code {
    private BitNavBarItem CurrentSelectedItem = BasicNavBarItems[0];
    // ... List<BitNavBarItem> BasicNavBarItems definition ...

    private IEnumerable<BitChoiceGroupItem<BitNavBarItem>> ChoiceGroupItems =>
        BasicNavBarItems.Select(i => new BitChoiceGroupItem<BitNavBarItem>()
        {
            Id = i.Key ?? i.Text, Text = i.Text, Value = i, IsEnabled = i.IsEnabled
        });
}
```

### Icon-Only Mode (`IconOnly`)

Renders only the icons for each item, hiding the text. Useful for compact navigation bars.

```razor
<BitNavBar Items="BasicNavBarItems" IconOnly />
```

### Sizing (`FitWidth`, `FullWidth`)

* `FitWidth`: Makes the NavBar component only as wide as necessary to fit its items horizontally.
* `FullWidth`: Makes the NavBar component expand horizontally to fill its parent container. (Mutually exclusive with `FitWidth`).

```razor
<div style="width: 500px; border: 1px dashed grey;">
    @* Will likely be narrower than 500px *@
    <BitNavBar Items="BasicNavBarItems" FitWidth />
</div>

<div style="width: 500px; border: 1px dashed grey;">
    @* Will fill the 500px width *@
    <BitNavBar Items="BasicNavBarItems" FullWidth />
</div>
```

### Disabling Items (`IsEnabled`)

* Set `IsEnabled="false"` on the `<BitNavBar>` component to disable the entire bar.
* Set `IsEnabled = false` on an individual `BitNavBarItem` (in the C# list) or `IsEnabled="false"` on a `<BitNavBarOption>` tag to disable a specific item.

```razor
@* Disable entire component *@
<BitNavBar Items="BasicNavBarItems" IsEnabled="false" />

@* Disable specific item via C# list *@
@code {
    private static readonly List<BitNavBarItem> ItemsWithDisabled = new()
    {
        new() { Text = "Home", IconName = BitIconName.Home },
        new() { Text = "Disabled Link", IconName = BitIconName.Blocked, IsEnabled = false },
        new() { Text = "Profile", IconName = BitIconName.Contact }
    };
}
<BitNavBar Items="ItemsWithDisabled" />

@* Disable specific item via declarative option *@
<BitNavBar>
    <BitNavBarOption Text="Enabled" IconName="Accept" />
    <BitNavBarOption Text="Disabled" IconName="Blocked" IsEnabled="false" />
</BitNavBar>
```

### Reselectable (`Reselectable`)

By default (`false`), clicking an already selected item does nothing. If `Reselectable="true"`, the `OnItemClick` and `OnSelectItem` events will fire even when clicking the currently selected item. Useful if clicking the active tab should trigger a refresh or reset action.

```razor
<BitNavBar Items="BasicNavBarItems"
           Mode="BitNavMode.Manual"
           Reselectable="true"
           OnItemClick="(item) => Console.WriteLine($"Clicked {item.Text} again!")" />
```

### Color (`Color`)

Applies a theme color to the NavBar, primarily affecting the selected item's indicator/highlight and potentially icon/text colors depending on the theme. Uses the `BitColor` enum.

```razor
<BitNavBar Items="BasicNavBarItems" Color="BitColor.Success" DefaultSelectedItem="BasicNavBarItems[0]" Mode="BitNavMode.Manual" />
<BitNavBar Items="BasicNavBarItems" Color="BitColor.Warning" DefaultSelectedItem="BasicNavBarItems[0]" Mode="BitNavMode.Manual" />
```

### Right-to-Left (`Dir`)

Renders the component layout and item order for RTL languages.

```razor
<BitNavBar Items="RtlItems" Dir="BitDir.Rtl" />

@code {
    private static readonly List<BitNavBarItem> RtlItems = new() { /* ... items with RTL text ... */ };
}
```

---

## Customization

### Custom Templates

* **`ItemTemplate`**: A global template applied to *all* items in the NavBar. The `Context` provides the `BitNavBarItem` (or your `TItem`).
* **Item-Specific `Template`**: Defined on an individual `BitNavBarItem` instance (in C#) or `<BitNavBarOption>` tag. Overrides the global `ItemTemplate` for that specific item.

```razor
@* Global ItemTemplate *@
<BitNavBar Items="BasicNavBarItems">
    <ItemTemplate Context="item">
        <div style="display: flex; flex-direction: column; align-items: center; padding: 2px 0;">
            <BitIcon IconName="@item.IconName" Color="BitColor.Warning" />
            <span style="font-size: 0.8em; color: purple;">@item.Text</span>
        </div>
    </ItemTemplate>
</BitNavBar>

@* Item-Specific Template via C# List *@
@code {
    private static readonly List<BitNavBarItem> ItemsWithSpecificTemplate = new()
    {
        new() { Text = "Normal", IconName = BitIconName.Home },
        new() { Text = "Custom", IconName = BitIconName.Brush, Template = (item) => @<div style="color: red; font-weight: bold;">🎨 @item.Text!</div> },
        new() { Text = "Normal Too", IconName = BitIconName.Settings }
    };
}
<BitNavBar Items="ItemsWithSpecificTemplate" />
```

### Styling

* **`Style` / `Class`:** Apply standard inline styles or CSS classes to the root `nav` element of the NavBar.
* **`Styles` / `Classes` Parameters:** Provide `BitNavBarClassStyles` objects to target internal elements (root, container, item, icon, text, selected item) for granular CSS control.

```razor
@* Inline style on root *@
<BitNavBar Items="BasicNavBarItems" Style="background-color: #f0f0f0; border-top: 1px solid #ccc;" />

@* CSS class on root *@
<BitNavBar Items="BasicNavBarItems" Class="my-custom-navbar-styles" />

@* Granular styling via Styles parameter *@
<BitNavBar Items="BasicNavBarItems"
           Styles="@(new BitNavBarClassStyles {
                         Root = "box-shadow: 0 -2px 5px rgba(0,0,0,0.1);",
                         Item = "padding: 8px 12px;",
                         ItemIcon = "font-size: 1.2em;",
                         ItemText = "font-size: 0.9em; margin-top: 2px;",
                         SelectedItem = "background-color: transparent; border-bottom: 3px solid blue; color: blue;"
                     })" />

@* Granular styling via Classes parameter (assuming CSS exists) *@
<BitNavBar Items="BasicNavBarItems"
           Classes="@(new BitNavBarClassStyles {
                         Item = "custom-navbar-item",
                         ItemIcon = "custom-navbar-icon",
                         SelectedItem = "custom-navbar-item--selected"
                     })" />
```

*(See `BitNavBarClassStyles` definition in the API section for available selectors).*

---

## Key Parameters (`BitNavBar<TItem>`)

<!-- AI: Focus on these common parameters when generating BitNavBar code. -->

| Parameter             | Type                          | Default                            | Description                                                               |
| :-------------------- | :---------------------------- | :--------------------------------- | :------------------------------------------------------------------------ |
| `Items`               | `IList<TItem>`                | `new List<TItem>()`                | Collection of items (`BitNavBarItem` or custom `TItem`) to display.       |
| `ChildContent` / `Options` | `RenderFragment?`           | `null`                             | Used for declaring items via `<BitNavBarOption>` instead of `Items`.        |
| `Mode`                | `BitNavMode`                  | `BitNavMode.Automatic`             | Controls selection highlighting (Automatic URL matching vs. Manual).      |
| `SelectedItem`        | `TItem?`                      | `null`                             | The currently selected item. Use `@bind-SelectedItem` for two-way binding. |
| `DefaultSelectedItem` | `TItem?`                      | `null`                             | Item selected initially when `Mode` is `Manual`.                          |
| `IconOnly`            | `bool`                        | `false`                            | Renders only icons, hiding text.                                          |
| `FitWidth`            | `bool`                        | `false`                            | Sizes the NavBar to fit its content width.                                |
| `FullWidth`           | `bool`                        | `false`                            | Sizes the NavBar to fill its container's width.                           |
| `Color`               | `BitColor?`                   | `null`                             | Applies a theme color, affecting selected item style.                     |
| `IsEnabled`           | `bool`                        | `true`                             | Enables/disables the entire NavBar component.                             |
| `Reselectable`        | `bool`                        | `false`                            | Allows `OnItemClick`/`OnSelectItem` to fire for already selected items.   |
| `OnSelectItem`        | `EventCallback<TItem>`        | -                                  | Callback invoked when an item is selected (especially in Manual mode).    |
| `OnItemClick`         | `EventCallback<TItem>`        | -                                  | Callback invoked when *any* item is clicked.                              |
| `ItemTemplate`        | `RenderFragment<TItem>?`      | `null`                             | Custom template applied to all items.                                     |
| `NameSelectors`       | `BitNavBarNameSelectors<TItem>?`| `null`                             | Maps properties when using a custom `TItem` class.                        |
| `Styles`              | `BitNavBarClassStyles?`       | `null`                             | Custom inline styles for internal elements.                               |
| `Classes`             | `BitNavBarClassStyles?`       | `null`                             | Custom CSS classes for internal elements.                                 |
| `Dir`                 | `BitDir?`                     | `null`                             | Sets the text direction (Ltr, Rtl, Auto).                                 |

---

## `BitNavBarItem` Structure (for `Items` parameter)

| Property         | Type                       | Default          | Description                                                              |
| :--------------- | :------------------------- | :--------------- | :----------------------------------------------------------------------- |
| `Text`           | `string`                   | `string.Empty`   | Display text for the item.                                               |
| `Url`            | `string?`                  | `null`           | URL the item links to.                                                   |
| `IconName`       | `string?`                  | `null`           | Name of the BitIcon to display.                                          |
| `IsEnabled`      | `bool`                     | `true`           | Whether the item is clickable/interactive.                               |
| `Key`            | `string?`                  | `null`           | Unique identifier for the item. Used for selection tracking.             |
| `Target`         | `string?`                  | `null`           | HTML `target` attribute for the link (`_blank`, `_self`, etc.).           |
| `Title`          | `string?`                  | `null`           | Tooltip text (HTML `title` attribute).                                   |
| `Style`          | `string?`                  | `null`           | Custom inline CSS style for this specific item.                          |
| `Class`          | `string?`                  | `null`           | Custom CSS class for this specific item.                                 |
| `AdditionalUrls` | `IEnumerable<string>?`     | `null`           | Additional URLs to consider for matching in Automatic mode.              |
| `Data`           | `object?`                  | `null`           | Custom data payload associated with the item.                            |
| `Template`       | `RenderFragment<BitNavBarItem>?`| `null`       | Specific template for *this individual item*, overriding `ItemTemplate`. |

---

## `BitNavBarOption` Structure (for Declarative Usage)

Attributes correspond closely to `BitNavBarItem` properties.

| Attribute        | Type                       | Description                                              |
| :--------------- | :------------------------- | :------------------------------------------------------- |
| `Text`           | `string`                   | Display text.                                            |
| `Url`            | `string?`                  | Link URL.                                                |
| `IconName`       | `string?`                  | Icon name.                                               |
| `IsEnabled`      | `bool`                     | Enable/disable state.                                    |
| `Key`            | `string?`                  | Unique key.                                              |
| `Target`         | `string?`                  | Link target.                                             |
| `Title`          | `string?`                  | Tooltip text.                                            |
| `Style`          | `string?`                  | Inline style.                                            |
| `Class`          | `string?`                  | CSS class.                                               |
| `AdditionalUrls` | `IEnumerable<string>?`     | Additional URLs for matching.                            |
| `Data`           | `object?`                  | Custom data.                                             |
| `Template`       | `RenderFragment<BitNavBarOption>?`| Individual item template override.                 |

---

## Event Handling

* **`OnSelectItem(TItem item)`**: Fires when an item becomes *selected* (highlighted). In `Automatic` mode, this fires when the URL matches. In `Manual` mode, it fires when an item is clicked *and* becomes the `SelectedItem`. The `item` argument is the selected `BitNavBarItem` (or custom `TItem`).
* **`OnItemClick(TItem item)`**: Fires whenever an item in the NavBar is clicked, regardless of whether it becomes selected or was already selected. The `item` argument is the clicked `BitNavBarItem` (or custom `TItem`).

---

## Relevant Enums

* `BitNavMode`: `Automatic`, `Manual` (Shared with `BitNav`)
* `BitDir`: `Ltr`, `Rtl`, `Auto`
* `BitColor`: Used for `Color` parameter (e.g., `Primary`, `Success`, `Error`).
* `BitVisibility`: Used for `Visibility` parameter (`Visible`, `Hidden`, `Collapsed`).

---

## AI Agent Guidance Summary

* Use `<BitNavBar>` for horizontal, tab-like navigation (primary or bottom bar). It handles a flat list of items.
* **Data Input:** Choose one method:
  * Bind `List<BitNavBarItem>` to `Items`.
  * Bind `List<YourCustomClass>` to `Items` and provide `NameSelectors`.
  * Use `<BitNavBarOption>` elements within `<BitNavBar>` (via `ChildContent` or `Options`).
* **Selection:** Use `Mode="BitNavMode.Automatic"` for URL-based highlighting (default) or `Mode="BitNavMode.Manual"` with `@bind-SelectedItem` and/or `OnSelectItem` for external control.
* **Appearance:**
  * Use `IconOnly="true"` for a compact icon view.
  * Use `FitWidth` or `FullWidth` for sizing.
  * Use `Color` parameter for theming the selected item.
  * Use `Styles` or `Classes` for custom styling of internal parts (item, icon, text, etc.).
  * Use `ItemTemplate` (global) or `Template` (item-specific) for custom rendering.
* **Events:** Use `OnSelectItem` to react to selection changes and `OnItemClick` to react to any click on an item.
* **Disabling:** Disable the whole bar via `IsEnabled` on `<BitNavBar>` or individual items via the `IsEnabled` property/attribute on the item/option.
* Use `Reselectable="true"` if clicks on already-selected items should trigger events.
* Define item properties (text, url, icon, enabled state, etc.) via `BitNavBarItem` properties, custom class properties (with `NameSelectors`), or `<BitNavBarOption>` attributes.