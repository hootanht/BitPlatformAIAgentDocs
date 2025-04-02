# BitBreadcrumb Component Reference

## Overview

The `BitBreadcrumb` component is used as a navigational aid within an application or website. It clearly indicates the current page's location within a hierarchical structure. This helps users understand their position relative to the rest of the site or app hierarchy and provides convenient one-click access to navigate to higher levels within that hierarchy.

## Notes

*   The `BitBreadcrumb` is a versatile **Multi-API** component.
*   It can accept the list of breadcrumb items in three distinct ways:
    1.  Using a list of `BitBreadcrumbItem` class instances.
    2.  Using a list of a custom generic class (`TItem`), configured via the `NameSelectors` parameter.
    3.  Using `BitBreadcrumbOption` components directly nested within the `BitBreadcrumb` tags.

**(This document primarily focuses on examples using `BitBreadcrumbItem` as derived from the provided source HTML.)**

## Usage (Examples using `BitBreadcrumbItem`)

These examples demonstrate how to use the `BitBreadcrumb` component by providing a list of `BitBreadcrumbItem` objects to the `Items` parameter.

### 1. Basic Usage

This example shows the fundamental implementation of the `BitBreadcrumb` component. It also demonstrates:
*   A standard breadcrumb.
*   A breadcrumb where the entire component is disabled (`IsEnabled="false"`).
*   A breadcrumb where individual items are disabled (`IsEnabled = false` within the `BitBreadcrumbItem`).

**Code:**

```html
<BitBreadcrumb Items="BreadcrumbItems" />

<BitBreadcrumb Items="BreadcrumbItems" IsEnabled="false" />

<BitBreadcrumb Items="BreadcrumbItemsDisabled" />
```

```csharp
@code {
    private readonly List<BitBreadcrumbItem> BreadcrumbItems =
    [
        new() { Text = "Item 1", Href = "/components/breadcrumb" },
        new() { Text = "Item 2", Href = "/components/breadcrumb" },
        new() { Text = "Item 3", Href = "/components/breadcrumb" },
        new() { Text = "Item 4", Href = "/components/breadcrumb", IsSelected = true }
    ];

    private readonly List<BitBreadcrumbItem> BreadcrumbItemsDisabled =
    [
        new() { Text = "Item 1", Href = "/components/breadcrumb", IsEnabled = false },
        new() { Text = "Item 2", Href = "/components/breadcrumb", IsEnabled = false },
        new() { Text = "Item 3", Href = "/components/breadcrumb" },
        new() { Text = "Item 4", Href = "/components/breadcrumb", IsSelected = true }
    ];
}
```

### 2. MaxDisplayedItems & OverflowIndex

You can control how many breadcrumb items are visible using `MaxDisplayedItems`. If the total number of items exceeds this value, the excess items are collapsed into an overflow menu (represented by an ellipsis icon by default). The `OverflowIndex` parameter determines the position (index) where the overflow menu appears within the displayed items.

**Code:**

```html
<BitBreadcrumb Items="BreadcrumbItems" MaxDisplayedItems="1" />

<BitBreadcrumb Items="BreadcrumbItems" MaxDisplayedItems="2" />

<BitBreadcrumb Items="BreadcrumbItems" MaxDisplayedItems="3" />

<BitBreadcrumb Items="BreadcrumbItems" MaxDisplayedItems="3" OverflowIndex="0" />

<BitBreadcrumb Items="BreadcrumbItems" MaxDisplayedItems="3" OverflowIndex="1" />

<BitBreadcrumb Items="BreadcrumbItems" MaxDisplayedItems="3" OverflowIndex="2" />
```

```csharp
@code {
    private readonly List<BitBreadcrumbItem> BreadcrumbItems =
    [
        new() { Text = "Item 1", Href = "/components/breadcrumb" },
        new() { Text = "Item 2", Href = "/components/breadcrumb" },
        new() { Text = "Item 3", Href = "/components/breadcrumb" },
        new() { Text = "Item 4", Href = "/components/breadcrumb", IsSelected = true }
    ];
}
```

**Explanation:**

* `MaxDisplayedItems="1"`: Shows overflow (...) and the last item.
* `MaxDisplayedItems="2"`: Shows overflow (...), the second-to-last, and the last item.
* `MaxDisplayedItems="3"`: Shows overflow (...), the third-to-last, second-to-last, and last item.
* `OverflowIndex="0"`: Places the overflow menu at the beginning.
* `OverflowIndex="1"`: Places the overflow menu after the first visible item.
* `OverflowIndex="2"`: Places the overflow menu after the second visible item.

### 3. Icons

Customize the icons used within the `BitBreadcrumb`:

* `IconName` property on `BitBreadcrumbItem`: Sets an icon for an individual breadcrumb item.
* `DividerIconName`: Sets the icon used as a separator between items.
* `OverflowIconName`: Sets the icon for the overflow menu button.
* `ReversedIcon`: A boolean parameter (or property on `BitBreadcrumbItem`) that reverses the position of the icon and text within an item.

**Code:**

```html
<BitBreadcrumb Items="BreadcrumbItemsWitIcon"
               DividerIconName="@BitIconName.CaretRightSolid8"
               OverflowIconName="@BitIconName.ChevronDown"
               OverflowIndex="2"
               MaxDisplayedItems="3" />

<BitBreadcrumb Items="BreadcrumbItemsWitIcon"
               OverflowIconName="@BitIconName.CollapseMenu"
               MaxDisplayedItems="3"
               OverflowIndex="2"
               ReversedIcon />
```

```csharp
@code {
    private readonly List<BitBreadcrumbItem> BreadcrumbItemsWitIcon =
    [
        new() { Text = "Item 1", Href = "/components/breadcrumb", IconName = BitIconName.AdminELogoInverse32 },
        new() { Text = "Item 2", Href = "/components/breadcrumb", IconName = BitIconName.AppsContent },
        new() { Text = "Item 3", Href = "/components/breadcrumb", IconName = BitIconName.AzureIcon },
        new() { Text = "Item 4", Href = "/components/breadcrumb", IsSelected = true, IconName = BitIconName.ClassNotebookLogo16 }
    ];
}
```

### 4. Templates

Provide custom rendering logic for different parts of the breadcrumb using templates:

* `DividerIconTemplate`: Customizes the rendering of the divider between items.
* `ItemTemplate`: Customizes the rendering of each *visible* breadcrumb item. Receives the `BitBreadcrumbItem` as context.
* `OverflowTemplate`: Customizes the rendering of each item within the *overflow menu*. Receives the `BitBreadcrumbItem` as context.
* `Template` property on `BitBreadcrumbItem`: Provides a custom render fragment specifically for that *visible* item.
* `OverflowTemplate` property on `BitBreadcrumbItem`: Provides a custom render fragment specifically for that item when it appears *in the overflow menu*.

**Code:**

```html
<BitBreadcrumb Items="BreadcrumbItems">
    <DividerIconTemplate>
        <BitIcon IconName="@BitIconName.CaretRightSolid8" Color="BitColor.Warning" />
    </DividerIconTemplate>
</BitBreadcrumb>

<BitBreadcrumb Items="BreadcrumbItems"
                MaxDisplayedItems="3"
                OverflowIndex="2">
    <ItemTemplate Context="item">
        <div style="font-weight: bold; color: #d13438; font-style:italic;">
            @item.Text
        </div>
    </ItemTemplate>
    <OverflowTemplate Context="item">
        <div style="font-weight: bold; color: blueviolet; font-style:italic;">
            @item.Text
        </div>
    </OverflowTemplate>
</BitBreadcrumb>

<BitBreadcrumb Items="BreadcrumbItemTemplateItems"
                MaxDisplayedItems="3"
                OverflowIndex="2" />
```

```csharp
@code {
    private readonly List<BitBreadcrumbItem> BreadcrumbItems =
    [
        new() { Text = "Item 1", Href = "/components/breadcrumb" },
        new() { Text = "Item 2", Href = "/components/breadcrumb" },
        new() { Text = "Item 3", Href = "/components/breadcrumb" },
        new() { Text = "Item 4", Href = "/components/breadcrumb", IsSelected = true }
    ];

    private readonly List<BitBreadcrumbItem> BreadcrumbItemTemplateItems =
    [
        new()
        {
            Text = "Item 1", Href = "/components/breadcrumb",
            Template = (item => @<div style="color:green">@item.Text</div>),
            OverflowTemplate = (item => @<div style="color:green;text-decoration:underline;">@item.Text</div>)
        },
        new ()
        {
            Text = "Item 2", Href = "/components/breadcrumb",
            Template = (item => @<div style="color:yellow">@item.Text</div>),
            OverflowTemplate = (item => @<div style="color:yellow;text-decoration:underline;">@item.Text</div>)
        },
        new()
        {
            Text = "Item 3", Href = "/components/breadcrumb",
            Template = (item => @<div style="color:red">@item.Text</div>),
            OverflowTemplate = (item => @<div style="color:red;text-decoration:underline;">@item.Text</div>)
        },
        new()
        {
            Text = "Item 4", Href = "/components/breadcrumb", IsSelected = true,
            Template = (item => @<div style="color:blue">@item.Text</div>),
            OverflowTemplate = (item => @<div style="color:blue;text-decoration:underline;">@item.Text</div>)
        }
    ];
}
```

### 5. Events

The `OnItemClick` event callback is triggered when a breadcrumb item (either visible or in the overflow menu) is clicked. It receives the clicked `BitBreadcrumbItem` as an argument. This is useful for handling navigation or updating the selected state manually, especially if `Href` is not used on the items.

**Code:**

```html
<BitBreadcrumb Items="@BreadcrumbItemsWithControlled"
               MaxDisplayedItems="3"
               OverflowIndex="2"
               OnItemClick="(BitBreadcrumbItem item) => HandleOnItemClick(item)"
               Styles="@(new() { SelectedItem = "color: dodgerblue;", OverflowSelectedItem = "color: red;" })" />
```

```csharp
@code {
    private readonly List<BitBreadcrumbItem> BreadcrumbItemsWithControlled =
    [
        new() { Text = "Item 1" },
        new() { Text = "Item 2" },
        new() { Text = "Item 3" },
        new() { Text = "Item 4" },
        new() { Text = "Item 5" },
        new() { Text = "Item 6", IsSelected = true }
    ];

    private void HandleOnItemClick(BitBreadcrumbItem item)
    {
        // Find the currently selected item and deselect it
        BreadcrumbItemsWithControlled.FirstOrDefault(i => i.IsSelected).IsSelected = false;
        // Select the clicked item
        item.IsSelected = true;
        // StateHasChanged() might be needed depending on the component context
    }
}
```

*Note: The `Styles` parameter is used here to visually distinguish the selected item.*

### 6. Customizations (Dynamic Items)

This example demonstrates manipulating the `Items` collection dynamically (adding/removing items) and controlling `MaxDisplayedItems` and `OverflowIndex` via external controls.

**Code:**

```html
<BitBreadcrumb Items="@BreadcrumbItemsWithCustomized"
                MaxDisplayedItems="@MaxDisplayedItems"
                OverflowIndex="@OverflowIndex"
                OnItemClick="(BitBreadcrumbItem item) => HandleOnCustomizedItemClick(item)" />

<BitButton OnClick="AddBreadcrumbItem">Add Item</BitButton>
<BitButton OnClick="RemoveBreadcrumbItem">Remove Item</BitButton>

<BitNumberField @bind-Value="MaxDisplayedItems" Label="Max displayed items" ShowArrows="true" />
<BitNumberField @bind-Value="OverflowIndex" Label="Overflow index" ShowArrows="true" />
```

```csharp
@code {
    private int ItemsCount = 4;
    private uint OverflowIndex = 2;
    private uint MaxDisplayedItems = 3;

    private List<BitBreadcrumbItem> BreadcrumbItemsWithCustomized = // Use List<> not readonly for modification
    [
        new() { Text = "Item 1" },
        new() { Text = "Item 2" },
        new() { Text = "Item 3" },
        new() { Text = "Item 4", IsSelected = true }
    ];

    private void HandleOnCustomizedItemClick(BitBreadcrumbItem item)
    {
        BreadcrumbItemsWithCustomized.FirstOrDefault(i => i.IsSelected).IsSelected = false;
        item.IsSelected = true;
    }

    private void AddBreadcrumbItem() // Corrected function name from source HTML analysis
    {
        ItemsCount++;
        // Deselect current item before adding a new selected one
        var currentSelected = BreadcrumbItemsWithCustomized.FirstOrDefault(i => i.IsSelected);
        if (currentSelected != null) currentSelected.IsSelected = false;

        BreadcrumbItemsWithCustomized.Add(new BitBreadcrumbItem()
        {
            Text = $"Item {ItemsCount}",
            IsSelected = true // Make the new item selected
        });
    }

    private void RemoveBreadcrumbItem() // Corrected function name from source HTML analysis
    {
        if (BreadcrumbItemsWithCustomized.Count > 1)
        {
            var itemToRemove = BreadcrumbItemsWithCustomized[^1]; // Get the last item
            BreadcrumbItemsWithCustomized.RemoveAt(BreadcrumbItemsWithCustomized.Count - 1); // Remove the last item

            ItemsCount--; // Decrement count only after successful removal

            // If the removed item was selected, select the new last item
            if (itemToRemove.IsSelected && BreadcrumbItemsWithCustomized.Count > 0)
            {
                BreadcrumbItemsWithCustomized[^1].IsSelected = true;
            }
            // Ensure at least one item is selected if list is not empty
            else if (BreadcrumbItemsWithCustomized.Count > 0 && !BreadcrumbItemsWithCustomized.Any(i => i.IsSelected))
            {
                 BreadcrumbItemsWithCustomized[^1].IsSelected = true;
            }
        }
    }
}
```

*(Note: C# code adapted slightly for dynamic list manipulation and selection handling based on button actions).*

### 7. Class & Style

Apply custom CSS classes and inline styles:

* `Class` and `Style` parameters on `BitBreadcrumb`: Apply to the root element.
* `Class` and `Style` properties on `BitBreadcrumbItem`: Apply to individual item elements.
* `Classes` and `Styles` parameters on `BitBreadcrumb`: Allow targeting specific internal parts of the component (like `Item`, `SelectedItem`, `Divider`, etc.) using the `BitBreadcrumbClassStyles` object.

**Code:**

```html
<style>
    .custom-class {
        font-style: italic;
        text-shadow: dodgerblue 0 0 0.5rem;
        border-bottom: 1px solid dodgerblue;
    }

    .custom-item {
        color: #ffcece;
    }
    .custom-item:hover {
        color: #ff6868;
        background: transparent;
    }

    .custom-item-1 {
        color: #b6ff00;
    }
    .custom-item-1:hover {
        color: #2aff00;
        background: transparent;
    }

    .custom-item-2 {
        color: #ffd800;
    }
    .custom-item-2:hover {
        color: #ff6a00;
        background: transparent;
    }

    .custom-selected-item {
        color: blueviolet;
    }
    .custom-selected-item:hover {
        color: blueviolet;
        background: transparent;
        text-shadow: blueviolet 0 0 1rem;
    }
</style>

<!-- Component Level -->
<BitBreadcrumb Items="BreadcrumbItems" Class="custom-class" />
<BitBreadcrumb Items="BreadcrumbItems" Style="font-style: italic;text-shadow: aqua 0 0 0.5rem;border-bottom: 1px solid aqua;" />

<!-- Item Level -->
<BitBreadcrumb Items="BreadcrumbItemsWithClass" />
<BitBreadcrumb Items="BreadcrumbItemsWithStyle" />

<!-- Targeted Parts -->
<BitBreadcrumb Items="BreadcrumbItems"
               Classes="@(new() { Item = "custom-item", SelectedItem = "custom-selected-item" })" />
<BitBreadcrumb Items="BreadcrumbItems"
               Styles="@(new() { Item = "color: green;", SelectedItem = "color: lightseagreen; text-shadow: lightseagreen 0 0 1rem;" })" />

```

```csharp
@code {
    private readonly List<BitBreadcrumbItem> BreadcrumbItems =
    [
        new() { Text = "Item 1", Href = "/components/breadcrumb" },
        new() { Text = "Item 2", Href = "/components/breadcrumb" },
        new() { Text = "Item 3", Href = "/components/breadcrumb" },
        new() { Text = "Item 4", Href = "/components/breadcrumb", IsSelected = true }
    ];

    private readonly List<BitBreadcrumbItem> BreadcrumbItemsWithClass =
    [
        new() { Text = "Item 1", Href = "/components/breadcrumb", Class = "custom-item-1" },
        new() { Text = "Item 2", Href = "/components/breadcrumb", Class = "custom-item-2" },
        new() { Text = "Item 3", Href = "/components/breadcrumb", Class = "custom-item-1" },
        new() { Text = "Item 4", Href = "/components/breadcrumb", Class = "custom-item-2", IsSelected = true }
    ];

    private readonly List<BitBreadcrumbItem> BreadcrumbItemsWithStyle =
    [
        new() { Text = "Item 1", Href = "/components/breadcrumb", Style = "color: dodgerblue; text-shadow: dodgerblue 0 0 1rem;" },
        new() { Text = "Item 2", Href = "/components/breadcrumb", Style = "color: aqua; text-shadow: aqua 0 0 1rem;" },
        new() { Text = "Item 3", Href = "/components/breadcrumb", Style = "color: dodgerblue; text-shadow: dodgerblue 0 0 1rem;" },
        new() { Text = "Item 4", Href = "/components/breadcrumb", Style = "color: aqua; text-shadow: aqua 0 0 1rem;", IsSelected = true }
    ];
}
```

### 8. RTL (Right-to-Left)

The `BitBreadcrumb` component supports right-to-left layouts. Set the `Dir` parameter to `BitDir.Rtl`. The order of items remains logical, but the visual layout and divider direction adjust accordingly.

**Code:**

```html
<BitBreadcrumb Dir="BitDir.Rtl" Items="RtlBreadcrumbItems" MaxDisplayedItems="3" OverflowIndex="2" />
```

```csharp
@code {
    private readonly List<BitBreadcrumbItem> RtlBreadcrumbItems =
    [
        new() { Text = "پوشه اول" }, // "Folder 1"
        new() { Text = "پوشه دوم", IsSelected = true }, // "Folder 2"
        new() { Text = "پوشه سوم" }, // "Folder 3"
        new() { Text = "پوشه چهارم" }, // "Folder 4"
        new() { Text = "پوشه پنجم" }, // "Folder 5"
        new() { Text = "پوشه ششم" }  // "Folder 6"
    ];
}
```

---

## API Reference

### `BitBreadcrumb<TItem>` Parameters

| Name                  | Type                                         | Default Value | Description                                                                                                |
| --------------------- | -------------------------------------------- | ------------- | ---------------------------------------------------------------------------------------------------------- |
| `Items`               | `IList<TItem>`                               | `[]`          | Collection of breadcrumb items (`BitBreadcrumbItem` or custom `TItem`) to render.                          |
| `ChildContent`        | `RenderFragment?`                            | `null`        | The content of the `BitBreadcrumb`, used for rendering `BitBreadcrumbOption` components.                 |
| `Options`             | `RenderFragment?`                            | `null`        | Alias for `ChildContent`.                                                                                  |
| `MaxDisplayedItems`   | `uint`                                       | `0`           | The maximum number of breadcrumbs to display before collapsing into an overflow menu. `0` means show all.    |
| `OverflowIndex`       | `uint`                                       | `0`           | Optional index where overflow items will be collapsed.                                                     |
| `OverflowAriaLabel`   | `string?`                                    | `null`        | Aria label for the overflow button.                                                                        |
| `OverflowIconName`    | `string`                                     | `More`        | The name of the icon for the overflow button (from `BitIconName`).                                         |
| `DividerIconName`     | `string?`                                    | `null`        | The name of the icon used as a divider (from `BitIconName`). Defaults to a chevron.                       |
| `ReversedIcon`        | `bool`                                       | `false`       | Reverses the positions of the icon and text for all items globally. Can be overridden by item settings.   |
| `OnItemClick`         | `EventCallback<TItem>`                       |               | Callback triggered when a breadcrumb item is clicked. Receives the clicked item (`TItem`) as argument.   |
| `ItemTemplate`        | `RenderFragment<TItem>?`                     | `null`        | Custom template to render each visible item.                                                              |
| `OverflowTemplate`    | `RenderFragment<TItem>?`                     | `null`        | Custom template to render each item within the overflow menu.                                             |
| `DividerIconTemplate` | `RenderFragment?`                            | `null`        | Custom template to render the divider icon.                                                              |
| `OverflowIconTemplate`| `RenderFragment?`                            | `null`        | Custom template to render the overflow button's icon.                                                    |
| `Classes`             | `BitBreadcrumbClassStyles?`                  | `null`        | Custom CSS classes for different internal parts of the breadcrumb component.                             |
| `Styles`              | `BitBreadcrumbClassStyles?`                  | `null`        | Custom CSS styles for different internal parts of the breadcrumb component.                              |
| `NameSelectors`       | `BitBreadcrumbNameSelectors<TItem>?`         | `null`        | Configuration for mapping properties when using a custom `TItem` type instead of `BitBreadcrumbItem`.      |
| **Inherited Parameters** |                                            |               |                                                                                                            |
| `AriaLabel`           | `string?`                                    | `null`        | The aria-label for the root element.                                                                       |
| `Class`               | `string?`                                    | `null`        | Custom CSS class for the root element.                                                                     |
| `Dir`                 | `BitDir?`                                    | `null`        | Sets the component direction (Ltr, Rtl, Auto).                                                             |
| `IsEnabled`           | `bool`                                       | `true`        | Whether the entire component is enabled.                                                                   |
| `Style`               | `string?`                                    | `null`        | Custom CSS style for the root element.                                                                     |
| `Visibility`          | `BitVisibility`                              | `Visible`     | Controls component visibility (Visible, Hidden, Collapsed).                                                |
| `HtmlAttributes`      | `Dictionary<string, object>`                 | `new(...)`    | Additional HTML attributes to render on the root element.                                                  |
| `Id`                  | `string?`                                    | `null`        | Custom id for the root element. If null, `UniqueId` is used.                                               |

### `BitBreadcrumbItem` Properties

(Used when `Items` is `IList<BitBreadcrumbItem>`)

| Name                | Type                                | Default Value | Description                                                                                             |
| ------------------- | ----------------------------------- | ------------- | ------------------------------------------------------------------------------------------------------- |
| `Text`              | `string?`                           |               | Text displayed in the breadcrumb item.                                                                  |
| `Href`              | `string?`                           |               | URL to navigate to on click. Renders the item as a link (`<a>`).                                       |
| `Key`               | `string?`                           |               | A unique key for the item (useful for Blazor diffing).                                                  |
| `Class`             | `string?`                           |               | Custom CSS class for this specific item's element.                                                      |
| `Style`             | `string?`                           |               | Custom CSS style for this specific item's element.                                                      |
| `IconName`          | `string?`                           |               | Name of the icon (from `BitIconName`) to display next to the text.                                      |
| `ReversedIcon`      | `bool?`                             |               | Reverses icon and text position for this specific item. Overrides the component's `ReversedIcon`.       |
| `IsSelected`        | `bool`                              |               | If true, marks this item as the currently selected/active item.                                         |
| `IsEnabled`         | `bool`                              | `true`        | Whether this specific item is enabled or disabled.                                                      |
| `OnClick`           | `Action<BitBreadcrumbItem>?`        |               | Specific click event handler for this item. (Note: `OnItemClick` on the component is often preferred).    |
| `Template`          | `RenderFragment<BitBreadcrumbItem>?`|               | Custom rendering template for this specific item when visible.                                            |
| `OverflowTemplate`  | `RenderFragment<BitBreadcrumbItem>?`|               | Custom rendering template for this specific item when it appears in the overflow menu.                  |

### `BitBreadcrumbOption` Parameters

(Used as child components of `BitBreadcrumb`)

*Note: `BitBreadcrumbOption` mostly mirrors `BitBreadcrumbItem` properties but is used declaratively in markup.*

| Name                | Type                                | Default Value | Description                                                                                             |
| ------------------- | ----------------------------------- | ------------- | ------------------------------------------------------------------------------------------------------- |
| `Text`              | `string?`                           |               | Text displayed in the breadcrumb option.                                                                |
| `Href`              | `string?`                           |               | URL to navigate to on click. Renders the option as a link (`<a>`).                                      |
| `Key`               | `string?`                           |               | A unique key for the option.                                                                            |
| `Class`             | `string?`                           |               | Custom CSS class for this specific option's element.                                                    |
| `Style`             | `string?`                           |               | Custom CSS style for this specific option's element.                                                    |
| `IconName`          | `string?`                           |               | Name of the icon (from `BitIconName`) to display next to the text.                                      |
| `ReversedIcon`      | `bool?`                             |               | Reverses icon and text position for this specific option. Overrides the component's `ReversedIcon`.     |
| `IsSelected`        | `bool`                              |               | If true, marks this option as the currently selected/active item.                                       |
| `IsEnabled`         | `bool`                              | `true`        | Whether this specific option is enabled or disabled.                                                    |
| `OnClick`           | `EventCallback<BitBreadcrumbOption>`|               | Click event handler for this option.                                                                    |
| `Template`          | `RenderFragment<BitBreadcrumbItem>?`|               | Custom rendering template for this specific option when visible. (Context is internal `BitBreadcrumbItem`). |
| `OverflowTemplate`  | `RenderFragment<BitBreadcrumbItem>?`|               | Custom rendering template for this specific option when it appears in the overflow menu. (Context is internal `BitBreadcrumbItem`). |

### `BitBreadcrumbClassStyles` Properties

(Used for the `Classes` and `Styles` parameters of `BitBreadcrumb`)

| Name                 | Type      | Default Value | Description                                                               |
| -------------------- | --------- | ------------- | ------------------------------------------------------------------------- |
| `Root`               | `string?` | `null`        | CSS class/style for the root `div` element.                               |
| `Overlay`            | `string?` | `null`        | CSS class/style for the overlay element (used during overflow interaction). |
| `ItemContainer`      | `string?` | `null`        | CSS class/style for the `ul` element containing visible items.              |
| `OverflowButton`     | `string?` | `null`        | CSS class/style for the overflow `button` element.                          |
| `OverflowButtonIcon` | `string?` | `null`        | CSS class/style for the icon inside the overflow button.                  |
| `ItemWrapper`        | `string?` | `null`        | CSS class/style for the `li` element wrapping each visible item/divider.    |
| `Item`               | `string?` | `null`        | CSS class/style for each breadcrumb item (`a` or `button` or `span`).      |
| `ItemIcon`           | `string?` | `null`        | CSS class/style for the icon (`i`) within each visible item.              |
| `ItemText`           | `string?` | `null`        | CSS class/style for the text (`span`) within each visible item.           |
| `SelectedItem`       | `string?` | `null`        | CSS class/style applied specifically to the selected item.                 |
| `Divider`            | `string?` | `null`        | CSS class/style for the `li` element wrapping the divider icon.           |
| `DividerIcon`        | `string?` | `null`        | CSS class/style for the divider icon (`i`) itself.                        |
| `Callout`            | `string?` | `null`        | CSS class/style for the callout container (the overflow dropdown).        |
| `CalloutContainer`   | `string?` | `null`        | CSS class/style for the inner container of the callout.                   |
| `OverflowItemWrapper`| `string?` | `null`        | CSS class/style for the `li` wrapping each item in the overflow menu.     |
| `OverflowItem`       | `string?` | `null`        | CSS class/style for each item (`a` or `button` or `span`) in the overflow menu. |
| `OverflowItemIcon`   | `string?` | `null`        | CSS class/style for the icon within each overflow item.                   |
| `OverflowItemText`   | `string?` | `null`        | CSS class/style for the text within each overflow item.                   |
| `OverflowSelectedItem`| `string?`| `null`        | CSS class/style applied specifically to the selected item in the overflow menu. |

### `BitBreadcrumbNameSelectors<TItem>` Properties

(Used for the `NameSelectors` parameter when `TItem` is a custom class)

| Name             | Type                                                | Default Value                              | Description                                                              |
| ---------------- | --------------------------------------------------- | ------------------------------------------ | ------------------------------------------------------------------------ |
| `Key`            | `BitNameSelectorPair<TItem, string?>`               | `new(nameof(BitBreadcrumbItem.Key))`       | Name/Selector for the property representing the item's key.              |
| `Text`           | `BitNameSelectorPair<TItem, string?>`               | `new(nameof(BitBreadcrumbItem.Text))`      | Name/Selector for the property representing the item's text.             |
| `Href`           | `BitNameSelectorPair<TItem, string?>`               | `new(nameof(BitBreadcrumbItem.Href))`      | Name/Selector for the property representing the item's URL.              |
| `Class`          | `BitNameSelectorPair<TItem, string?>`               | `new(nameof(BitBreadcrumbItem.Class))`     | Name/Selector for the property representing the item's CSS class.        |
| `Style`          | `BitNameSelectorPair<TItem, string?>`               | `new(nameof(BitBreadcrumbItem.Style))`     | Name/Selector for the property representing the item's CSS style.        |
| `IconName`       | `BitNameSelectorPair<TItem, string?>`               | `new(nameof(BitBreadcrumbItem.IconName))`  | Name/Selector for the property representing the item's icon name.        |
| `ReversedIcon`   | `BitNameSelectorPair<TItem, bool?>`                 | `new(nameof(BitBreadcrumbItem.ReversedIcon))`| Name/Selector for the property determining if icon/text are reversed.    |
| `IsSelected`     | `BitNameSelectorPair<TItem, bool>`                  | `new(nameof(BitBreadcrumbItem.IsSelected))`| Name/Selector for the boolean property indicating if the item is selected.|
| `IsEnabled`      | `BitNameSelectorPair<TItem, bool>`                  | `new(nameof(BitBreadcrumbItem.IsEnabled))` | Name/Selector for the boolean property indicating if the item is enabled.  |
| `OnClick`        | `Action<TItem>?`                                    |                                            | A direct action to invoke when the item is clicked (less common).        |
| `Template`       | `BitNameSelectorPair<TItem, RenderFragment<TItem>?>`| `new(nameof(BitBreadcrumbItem.Template))`  | Name/Selector for the property providing a visible item template.        |
| `OverflowTemplate`| `BitNameSelectorPair<TItem, RenderFragment<TItem>?>`| `new(nameof(BitBreadcrumbItem.OverflowTemplate))`| Name/Selector for the property providing an overflow item template.      |

### `BitNameSelectorPair<TItem, TProp>` Properties

| Name     | Type                 | Description                          |
| -------- | -------------------- | ------------------------------------ |
| `Name`   | `string`             | The name of the property in `TItem`. |
| `Selector`| `Func<TItem, TProp?>?` | A function to extract the property value from an instance of `TItem`. |

### `BitVisibility` Enum

| Name        | Value | Description                                                                       |
| ----------- | ----- | --------------------------------------------------------------------------------- |
| `Visible`   | `0`   | The component is visible.                                                         |
| `Hidden`    | `1`   | The component is hidden, but preserves layout space (`visibility: hidden`).       |
| `Collapsed` | `2`   | The component is hidden and does not preserve layout space (`display: none`).      |

### `BitDir` Enum

| Name  | Value | Description                                                                       |
| ----- | ----- | --------------------------------------------------------------------------------- |
| `Ltr` | `0`   | Left-to-right direction.                                                          |
| `Rtl` | `1`   | Right-to-left direction.                                                          |
| `Auto`| `2`   | Direction is determined by the browser based on the content.                      |

---

## Feedback

* Provide feedback via the [bitplatform GitHub repository](https://github.com/bitfoundation/bitplatform).
* File a new [Issue](https://github.com/bitfoundation/bitplatform/issues/new/choose).
* Start a new [Discussion](https://github.com/bitfoundation/bitplatform/discussions/new/choose).
* [Review](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Bit.BlazorUI/Components/Navs/Breadcrumb/BitBreadcrumb.razor) / [Edit](https://github.com/bitfoundation/bitplatform/edit/develop/src/BlazorUI/Bit.BlazorUI/Components/Navs/Breadcrumb/BitBreadcrumb.razor) this component's source code on GitHub.

