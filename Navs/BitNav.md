<!--
AI Agent Reference File: BitNav Component

Purpose: This file provides detailed information about the Blazor `BitNav` component.
Use this reference when generating, analyzing, or modifying code involving BitNav.
Focus on its purpose (navigation, tree view), data binding methods (BitNavItem, Custom Generic, BitNavOption),
key properties (Mode, RenderType, Items, SelectedItem, Templates, Styles), and event handling.
Pay close attention to the different ways items can be provided and customized.
-->

# BitNav Component Reference (Blazor)

## Overview

The `BitNav` component serves as a versatile navigation pane (often called a Nav) or a TreeView within Blazor applications. It's designed to display a hierarchical list of links or items, typically used for:

*   Main application navigation (sidebars, menus).
*   Displaying hierarchical data structures (like file systems, organization charts) in a tree format.

## Core Concepts: Multi-API Data Input

A key feature of `BitNav` is its flexibility in accepting the list of items to display. This is referred to as "Multi-API":

1.  **`List<BitNavItem>`:** The most common approach. You define a C# `List` where each element is an instance of the `BitNavItem` class. This class holds properties like `Text`, `Url`, `IconName`, `ChildItems`, etc. This list is then bound to the `Items` parameter of `BitNav`.
2.  **Custom Generic Class (`List<TItem>`)**: You can use your own custom C# class to represent navigation items. To make this work, you must provide the `NameSelectors` parameter to `BitNav`, which tells the component how to map properties from your custom class to the expected `BitNavItem` properties (like `Text`, `Url`, `ChildItems`, etc.).
3.  **`BitNavOption` Component**: You can define navigation items declaratively directly within the `.razor` markup using nested `<BitNavOption>` components inside the `<BitNav>` tags. Each `<BitNavOption>` acts like a `BitNavItem` and can contain further nested `<BitNavOption>` elements for hierarchical structures.

---

## Usage

### 1. Basic Usage with `BitNavItem` List

This is the standard method using a predefined C# list of `BitNavItem` objects.

```razor
@* In your .razor file *@
<BitNav Items="NavMenuItems" />

@code {
    private static readonly List<BitNavItem> NavMenuItems = new()
    {
        new() { Text = "Home", IconName = BitIconName.Home, Url = "/" },
        new()
        {
            Text = "Documents",
            IconName = BitIconName.Document,
            IsExpanded = true, // Start expanded
            ChildItems = new List<BitNavItem>
            {
                new() { Text = "Getting Started", Url = "/docs/getting-started" },
                new() { Text = "Components", Url = "/docs/components", IsEnabled = false }, // Disabled item
                new()
                {
                    Text = "Advanced",
                    ChildItems = new List<BitNavItem>
                    {
                        new() { Text = "Customization", Url = "/docs/advanced/customization" }
                    }
                }
            }
        },
        new() { Text = "About", IconName = BitIconName.Info, Url = "/about" }
    };
}
```

**Explanation:**

* A `List<BitNavItem>` named `NavMenuItems` is defined in the `@code` block.
* Each `BitNavItem` represents a link or a collapsible group.
* Properties like `Text`, `IconName`, `Url`, `IsEnabled`, `IsExpanded`, and crucially `ChildItems` (for nesting) are used.
* The list is passed to the `Items` parameter of `<BitNav>`.

*(For a detailed example of `BitNavItem` structure, see the "Basic" example in the provided HTML or the `BitNavItem` section below).*

### 2. Usage with Custom Generic Class (`List<TItem>`)

Define your own class and use `NameSelectors` to map its properties.

```razor
@* In your .razor file *@
<BitNav Items="CustomNavItems" NameSelectors="CustomNameSelectors" />

@code {
    public class MyNavItem
    {
        public string Label { get; set; }
        public string DestinationUrl { get; set; }
        public string Glyph { get; set; } // Custom property for icon
        public bool InitiallyOpen { get; set; }
        public List<MyNavItem> SubItems { get; set; }
        public bool IsDisabled { get; set; }
    }

    private static readonly List<MyNavItem> CustomNavItems = new() { /* ... populate list ... */ };

    // Define how MyNavItem properties map to BitNav expectations
    private static readonly BitNavNameSelectors<MyNavItem> CustomNameSelectors = new()
    {
        Text = { Name = nameof(MyNavItem.Label) }, // Map Label to Text
        Url = { Name = nameof(MyNavItem.DestinationUrl) }, // Map DestinationUrl to Url
        IconName = { Name = nameof(MyNavItem.Glyph) }, // Map Glyph to IconName
        IsExpanded = { Name = nameof(MyNavItem.InitiallyOpen) }, // Map InitiallyOpen to IsExpanded
        IsEnabled = { Name = nameof(MyNavItem.IsDisabled) }, // Map IsDisabled to IsEnabled
        ChildItems = { Name = nameof(MyNavItem.SubItems) } // Map SubItems to ChildItems
        // Other properties like Key, Target, etc., can also be mapped if needed
    };
}
```

**Explanation:**

* A custom class `MyNavItem` holds the navigation data.
* `NameSelectors` maps properties like `Label` (in `MyNavItem`) to `Text` (expected by `BitNav`).
* This allows using existing data models without converting them to `BitNavItem`.

### 3. Declarative Usage with `BitNavOption`

Define items directly in the markup.

```razor
<BitNav>
    <BitNavOption Text="Home" IconName="@BitIconName.Home" Url="/" />
    <BitNavOption Text="Products" IconName="@BitIconName.ShopServer">
        <BitNavOption Text="Widgets" Url="/products/widgets" />
        <BitNavOption Text="Gadgets" Url="/products/gadgets" IsEnabled="false" />
    </BitNavOption>
    <BitNavOption Text="Separator Example" IsSeparator="true" />
    <BitNavOption Text="Contact" IconName="@BitIconName.Contact" Url="/contact" />
</BitNav>
```

**Explanation:**

* Items are defined using `<BitNavOption>` tags nested within `<BitNav>`.
* Hierarchy is created by nesting `<BitNavOption>` elements.
* Properties are set directly as attributes on the `<BitNavOption>` tags.
* `IsSeparator="true"` creates a visual separator.

---

## Key Configurations & Features

### Render Type (`RenderType`)

Controls the overall visual structure.

* `BitNavRenderType.Normal` (Default): Standard tree/list rendering.
* `BitNavRenderType.Grouped`: Renders top-level items as distinct group headers, visually separating their child items.

```razor
<BitNav Items="CarNavMenu" RenderType="BitNavRenderType.Grouped" />
```

### Navigation Mode (`Mode`)

Determines how item selection is handled.

* `BitNavMode.Automatic` (Default): `BitNav` automatically determines the selected item based on the current browser URL matching an item's `Url` or `AdditionalUrls`. It uses Blazor's `NavigationManager`.
* `BitNavMode.Manual`: Selection is controlled externally. `BitNav` does not automatically change selection based on URL. You typically use `DefaultSelectedItem` to set an initial selection or `@bind-SelectedItem` for two-way binding, often combined with the `OnSelectItem` event.

```razor
@* Manual mode with initial selection *@
<BitNav Items="FoodNavMenu"
        Mode="BitNavMode.Manual"
        DefaultSelectedItem="FoodNavMenu[0].ChildItems[2]" />

@* Manual mode with two-way binding *@
<BitNav Items="FoodNavMenu"
        Mode="BitNavMode.Manual"
        @bind-SelectedItem="CurrentSelectedItem"
        OnSelectItem="HandleSelection" />

@code {
    private BitNavItem CurrentSelectedItem;
    // ... List<BitNavItem> FoodNavMenu definition ...

    private void HandleSelection(BitNavItem item)
    {
        // Optional: Logic to run when an item is selected
        Console.WriteLine($"Selected: {item.Text}");
    }

    // You might update CurrentSelectedItem from other parts of your UI too
}
```

### Icon-Only Mode (`IconOnly`)

Collapses the Nav to show only icons, usually expanding item text on hover or when the Nav is expanded.

```razor
<BitToggle @bind-Value="isIconOnlyMode" Label="Icon Only" />
<BitNav Items="NavMenuItems" IconOnly="isIconOnlyMode" />

@code {
    private bool isIconOnlyMode = false;
    // ... List<BitNavItem> NavMenuItems definition ...
}
```

### Sizing (`FitWidth`, `FullWidth`)

* `FitWidth`: Makes the Nav component only as wide as necessary to fit its content.
* `FullWidth`: Makes the Nav component take the full width of its parent container. (Mutually exclusive with `FitWidth`).

```razor
<div style="width: 300px; border: 1px dashed grey;">
    <BitNav Items="NavMenuItems" FitWidth /> @* Will be narrower than 300px *@
</div>

<div style="width: 300px; border: 1px dashed grey;">
    <BitNav Items="NavMenuItems" FullWidth /> @* Will fill the 300px width *@
</div>
```

### Right-to-Left (`Dir`)

Renders the component in RTL mode for languages like Arabic or Hebrew.

```razor
<BitNav Items="RtlNavMenuItems" Dir="BitDir.Rtl" />
```

---

## Customization

### Custom Templates

You can override the default rendering of items or group headers.

* **`ItemTemplate`**: Customizes the rendering of individual navigation items (leaves or expandable nodes *except* group headers in `Grouped` mode).
* **`HeaderTemplate`**: Customizes the rendering of group headers when `RenderType` is `BitNavRenderType.Grouped`.

```razor
<BitNav Items="FoodNavMenu" Mode="BitNavMode.Manual">
    <ItemTemplate Context="item">
        <div style="display: flex; align-items: center; gap: 5px; color: @(item.IsEnabled ? "blue" : "grey");">
            <BitIcon IconName="@(item.IconName ?? BitIconName. গ্রহ)" /> @* Default icon if none provided *@
            <span>@item.Text</span>
            @if (item.ChildItems?.Any() == true)
            {
                <span style="font-size: smaller;">(@item.ChildItems.Count)</span>
            }
        </div>
    </ItemTemplate>
</BitNav>

<BitNav Items="CarNavMenu" RenderType="BitNavRenderType.Grouped">
    <HeaderTemplate Context="item">
        <div style="font-weight: bold; color: green; padding: 5px 0;">
            @item.Text Group
        </div>
    </HeaderTemplate>
</BitNav>
```

**Explanation:**

* `Context="item"` provides access to the `BitNavItem` (or your custom item type `TItem`) being rendered.
* You can use standard Blazor components and HTML within the templates.
* `TemplateRenderMode` (on `BitNavItem` / `BitNavOption` or via `NameSelectors`) controls whether the template *replaces* the default item container (`Replace`) or renders *inside* it (`Normal`).

### Styling

* **`Style` / `Class`:** Apply standard inline styles or CSS classes to the root `nav` element.
* **`Styles` / `Classes` Parameters:** Provide objects (`BitNavClassStyles`) to target specific internal elements for more granular control.

```razor
@* Using the Styles parameter *@
<BitNav Items="NavMenuItems"
        Styles="@(new BitNavClassStyles {
                      Root = "border-right: 2px solid #eee;",
                      ItemContainer = "margin-bottom: 2px;",
                      Item = "font-family: 'Segoe UI';",
                      SelectedItem = "background-color: #e1f5fe; color: #0288d1;",
                      ItemIcon = "color: #666;",
                      ToggleButton = "color: #333;"
                  })" />

@* Using the Classes parameter (assuming CSS definitions exist) *@
<BitNav Items="NavMenuItems"
        Classes="@(new BitNavClassStyles {
                      Root = "my-custom-nav",
                      Item = "my-nav-item",
                      SelectedItem = "my-nav-item--selected"
                  })" />
```

*(See `BitNavClassStyles` definition in the API section for available selectors).*

---

## Key Parameters (`BitNav<TItem>`)

<!-- AI: Focus on these common parameters when generating BitNav code. -->

| Parameter               | Type                            | Default                            | Description                                                                 |
| :---------------------- | :------------------------------ | :--------------------------------- | :-------------------------------------------------------------------------- |
| `Items`                 | `IList<TItem>`                  | `new List<TItem>()`                | The collection of items to display (using `BitNavItem` or custom `TItem`).    |
| `ChildContent`          | `RenderFragment?`               | `null`                             | Used for declaring items via `<BitNavOption>` instead of `Items`.             |
| `Mode`                  | `BitNavMode`                    | `BitNavMode.Automatic`             | Controls selection behavior (Automatic URL matching vs. Manual control).    |
| `RenderType`            | `BitNavRenderType`              | `BitNavRenderType.Normal`          | Renders items normally or as grouped headers.                               |
| `SelectedItem`          | `TItem?`                        | `null`                             | The currently selected item. Use `@bind-SelectedItem` for two-way binding.  |
| `DefaultSelectedItem`   | `TItem?`                        | `null`                             | The item selected initially when `Mode` is `Manual`.                        |
| `IconOnly`              | `bool`                          | `false`                            | Renders only icons, hiding text (useful for collapsed sidebars).            |
| `FitWidth`              | `bool`                          | `false`                            | Sizes the Nav to fit its content width.                                     |
| `FullWidth`             | `bool`                          | `false`                            | Sizes the Nav to fill its container's width.                                |
| `IsEnabled`             | `bool`                          | `true`                             | Enables/disables the entire Nav component.                                  |
| `OnSelectItem`          | `EventCallback<TItem>`          | -                                  | Callback invoked when an item is selected (especially in Manual mode).      |
| `OnItemClick`           | `EventCallback<TItem>`          | -                                  | Callback invoked when *any* item (link or toggle) is clicked.               |
| `OnItemToggle`          | `EventCallback<TItem>`          | -                                  | Callback invoked when an expandable item is expanded or collapsed.          |
| `HeaderTemplate`        | `RenderFragment<TItem>?`        | `null`                             | Custom template for group headers (`RenderType="Grouped"`).                 |
| `ItemTemplate`          | `RenderFragment<TItem>?`        | `null`                             | Custom template for individual items.                                       |
| `NameSelectors`         | `BitNavNameSelectors<TItem>?`   | `null`                             | Maps properties when using a custom `TItem` class instead of `BitNavItem`.    |
| `Styles`                | `BitNavClassStyles?`            | `null`                             | Custom inline styles for internal elements.                                 |
| `Classes`               | `BitNavClassStyles?`            | `null`                             | Custom CSS classes for internal elements.                                   |
| `Dir`                   | `BitDir?`                       | `null`                             | Sets the text direction (Ltr, Rtl, Auto).                                   |
| `IndentValue`           | `int`                           | `16`                               | Indentation (px) per level for child items.                               |
| `SingleExpand`          | `bool`                          | `false`                            | If true, only one item can be expanded at a time at the same level.         |

---

## `BitNavItem` Structure (for `Items` parameter)

This class defines the properties when using `List<BitNavItem>`.

| Property            | Type                       | Default                         | Description                                                                 |
| :------------------ | :------------------------- | :------------------------------ | :-------------------------------------------------------------------------- |
| `Text`              | `string`                   | `string.Empty`                  | Display text for the item.                                                  |
| `Url`               | `string?`                  | `null`                          | URL the item links to. Renders as an `<a>` tag if set.                       |
| `IconName`          | `string?`                  | `null`                          | Name of the BitIcon to display.                                             |
| `ChildItems`        | `List<BitNavItem>`         | `[]`                            | List of nested child items. Renders expand/collapse chevron if not empty.   |
| `IsEnabled`         | `bool`                     | `true`                          | Whether the item is clickable/interactive.                                  |
| `IsExpanded`        | `bool`                     | `false`                         | Whether the item's children are initially visible (if it has children).     |
| `Target`            | `string?`                  | `null`                          | HTML `target` attribute for the link (`_blank`, `_self`, etc.).              |
| `Key`               | `string?`                  | `null`                          | Unique identifier for the item. Used for selection tracking.                |
| `Title`             | `string?`                  | `null`                          | Tooltip text (HTML `title` attribute).                                      |
| `IsSeparator`       | `bool`                     | `false`                         | Renders the item as a visual separator instead of a link/button.            |
| `Style`             | `string?`                  | `null`                          | Custom inline CSS style for this specific item's container.                 |
| `Class`             | `string?`                  | `null`                          | Custom CSS class for this specific item's container.                        |
| `Description`       | `string?`                  | `null`                          | Additional descriptive text displayed below the main item text.             |
| `AriaLabel`         | `string?`                  | `null`                          | Aria label for accessibility.                                               |
| `ExpandAriaLabel`   | `string?`                  | `null`                          | Aria label for the expand/collapse toggle when collapsed.                   |
| `CollapseAriaLabel` | `string?`                  | `null`                          | Aria label for the expand/collapse toggle when expanded.                    |
| `AriaCurrent`       | `BitNavAriaCurrent`        | `BitNavAriaCurrent.Page`        | Sets the `aria-current` attribute value when selected.                      |
| `ForceAnchor`       | `bool`                     | `false`                         | Force rendering as `<a>` even without a `Url`.                             |
| `AdditionalUrls`    | `IEnumerable<string>?`     | `null`                          | Additional URLs to consider for matching in Automatic mode.                 |
| `Data`              | `object?`                  | `null`                          | Custom data payload associated with the item.                               |
| `Template`          | `RenderFragment<BitNavItem>?` | `null`                          | Specific template for *this individual item*, overriding the main `ItemTemplate`. |
| `TemplateRenderMode`| `BitNavItemTemplateRenderMode` | `BitNavItemTemplateRenderMode.Normal` | Render mode for the item-specific `Template`.                               |

---

## `BitNavOption` Structure (for Declarative Usage)

Attributes correspond closely to `BitNavItem` properties.

| Attribute           | Type                       | Description                                                                 |
| :------------------ | :------------------------- | :-------------------------------------------------------------------------- |
| `Text`              | `string`                   | Display text.                                                               |
| `Url`               | `string?`                  | Link URL.                                                                   |
| `IconName`          | `string?`                  | Icon name.                                                                  |
| `IsEnabled`         | `bool`                     | Enable/disable state.                                                       |
| `IsExpanded`        | `bool`                     | Initial expanded state.                                                     |
| `Target`            | `string?`                  | Link target.                                                                |
| `Key`               | `string?`                  | Unique key.                                                                 |
| `Title`             | `string?`                  | Tooltip text.                                                               |
| `IsSeparator`       | `bool`                     | Render as separator.                                                        |
| `Style`             | `string?`                  | Inline style.                                                               |
| `Class`             | `string?`                  | CSS class.                                                                  |
| `Description`       | `string?`                  | Description text.                                                           |
| `AriaLabel`         | `string?`                  | Aria label.                                                                 |
| `ExpandAriaLabel`   | `string?`                  | Expand toggle aria label.                                                   |
| `CollapseAriaLabel` | `string?`                  | Collapse toggle aria label.                                                 |
| `AriaCurrent`       | `BitNavAriaCurrent`        | `aria-current` value.                                                       |
| `ForceAnchor`       | `bool`                     | Force `<a>` tag rendering.                                                 |
| `AdditionalUrls`    | `IEnumerable<string>?`     | Additional URLs for matching.                                               |
| `Data`              | `object?`                  | Custom data.                                                                |
| `Template`          | `RenderFragment<BitNavItem>?` | Individual item template.                                                   |
| `TemplateRenderMode`| `BitNavItemTemplateRenderMode` | Render mode for `Template`.                                               |
| `ChildContent`      | `RenderFragment?`          | Place nested `<BitNavOption>` elements here.                                |

---

## Event Handling

* **`OnSelectItem(BitNavItem item)`**: Fires when an item becomes selected. Primarily useful in `Manual` mode to know which item the user chose. The `item` argument is the selected `BitNavItem` (or custom `TItem`).
* **`OnItemClick(BitNavItem item)`**: Fires whenever *any* part of an item is clicked (the item itself if it's a link, or the expand/collapse chevron). The `item` argument is the clicked `BitNavItem`.
* **`OnItemToggle(BitNavItem item)`**: Fires specifically when an item with children is expanded or collapsed via its chevron. The `item` argument is the toggled `BitNavItem`, and its `IsExpanded` property reflects the *new* state.

---

## Public Members

You can get a reference to the `BitNav` component using `@ref` and call these methods:

* **`CollapseAll()`**: Collapses all expandable items in the Nav.
* **`ToggleItem(TItem item)`**: Programmatically toggles the expansion state of a specific item.

```razor
<BitNav @ref="myNavRef" Items="NavMenuItems" />
<BitButton OnClick="() => myNavRef.CollapseAll()">Collapse All</BitButton>
<BitButton OnClick="() => myNavRef.ToggleItem(NavMenuItems[1])">Toggle Documents</BitButton>

@code {
    private BitNav<BitNavItem> myNavRef;
    // ... List<BitNavItem> NavMenuItems definition ...
}
```

---

## Relevant Enums

* `BitNavMode`: `Automatic`, `Manual`
* `BitNavRenderType`: `Normal`, `Grouped`
* `BitNavAriaCurrent`: `Page`, `Step`, `Location`, `Date`, `Time`, `True`
* `BitNavItemTemplateRenderMode`: `Normal`, `Replace`
* `BitDir`: `Ltr`, `Rtl`, `Auto`
* `BitColor`: Used for `Color` and `Accent` parameters (e.g., `Primary`, `Success`, `Error`).
* `BitVisibility`: Used for `Visibility` parameter (`Visible`, `Hidden`, `Collapsed`).

---

## AI Agent Guidance Summary

* Use `<BitNav>` for hierarchical navigation or tree views.
* **Data Input:** Choose one method:
  * Bind `List<BitNavItem>` to `Items`.
  * Bind `List<YourCustomClass>` to `Items` and provide `NameSelectors`.
  * Use nested `<BitNavOption>` elements within `<BitNav>`.
* **Selection:** Use `Mode="BitNavMode.Automatic"` for URL-based selection (default) or `Mode="BitNavMode.Manual"` with `@bind-SelectedItem` and/or `OnSelectItem` for external control.
* **Hierarchy:** Use `ChildItems` property (in `BitNavItem` or custom class) or nested `<BitNavOption>` tags.
* **Appearance:**
  * Use `RenderType="BitNavRenderType.Grouped"` for grouped lists.
  * Use `IconOnly="true"` for a compact icon view.
  * Use `Styles` or `Classes` for custom styling.
  * Use `HeaderTemplate` / `ItemTemplate` for complex item rendering.
* **Events:** Use `OnSelectItem`, `OnItemClick`, `OnItemToggle` to react to user interactions.
* **Control:** Use `@ref` and methods like `CollapseAll()` or `ToggleItem()` for programmatic control.
* Define item properties (text, url, icon, enabled state, etc.) via `BitNavItem` properties, custom class properties (with `NameSelectors`), or `<BitNavOption>` attributes.