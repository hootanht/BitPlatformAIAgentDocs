# BitTimeline Component Reference (Blazor UI)

## 1. Overview

**`BitTimeline`** is a Blazor component used to display a sequence of events or items chronologically. It arranges items linearly, either vertically (default) or horizontally, using dots and connecting lines to represent the flow. Each item can display primary and secondary text, an icon, and custom content.

**Key Purpose:** To visualize processes, histories, or sequences of events in an ordered, easy-to-follow manner.

## 2. Multi-API Data Input

`BitTimeline` offers flexibility in how you provide data items:

1.  **`Items` with `BitTimelineItem`:** (Simplest) Pass a collection (`IEnumerable<BitTimelineItem>`) to the `Items` parameter. `BitTimelineItem` has predefined properties like `PrimaryText`, `SecondaryText`, `IconName`, `Color`, `Reversed`, `IsEnabled`, etc.
2.  **`Items` with Custom Generic Type (`TItem`)**: Pass a collection of your *own* custom objects (`IEnumerable<TItem>`) to the `Items` parameter. You **must** also provide the `NameSelectors` parameter to tell the `BitTimeline` how to map properties from your custom object (`TItem`) to the timeline item's display attributes (like text, icon, color, etc.).
3.  **`ChildContent` / `Options` with `BitTimelineOption`:** Define timeline items declaratively as child components (`<BitTimelineOption>`) within the `<BitTimeline>` tags. This is useful for manually defining a fixed set of timeline items directly in the markup.

These approaches allow you to choose the most convenient method based on your data source and structure.

## 3. Key Features

*   **Multiple Data Sources:** Accepts data via `Items` (using `BitTimelineItem` or custom generics with `NameSelectors`) or `ChildContent` (using `BitTimelineOption`).
*   **Orientation:** Supports both `Vertical` (default) and `Horizontal` layouts.
*   **Customization:**
    *   **Appearance:** Control overall appearance using `Variant` (Fill, Outline, Text), `Color`, and `Size`.
    *   **Item Content:** Customize content using `PrimaryText`/`SecondaryText`, `IconName`, or fully custom `RenderFragment` templates (`PrimaryContent`, `SecondaryContent`, `DotTemplate`, `ItemTemplate`).
    *   **Styling:** Apply custom CSS via `Class`/`Style` on the component/items, or use `Classes`/`Styles` parameters for fine-grained control over internal elements.
*   **Reversed Layout:** Display items on alternating sides (`Reversed` property on `BitTimeline` or individual items).
*   **Interactivity:** Supports `OnClick` events for individual items and disabling items (`IsEnabled`).
*   **RTL Support:** Adapts layout and direction for right-to-left languages (`Dir` parameter).

## 4. Usage Examples

*(Note: The examples below primarily use the `BitTimelineItem` approach for simplicity, as shown in the provided HTML source. See API sections for details on custom generics and `BitTimelineOption`.)*

### 4.1 Basic Timeline (`BitTimelineItem`)

Provide a list of `BitTimelineItem` objects to the `Items` parameter.

**Example (`.razor`):**

```cshtml
<BitTimeline Items="basicItems" />

@code {
    private List<BitTimelineItem> basicItems =
    [
        new() { PrimaryText = "Event 1 Started" },
        new() { PrimaryText = "Event 2 In Progress", SecondaryText = "Details about event 2..." },
        new() { PrimaryText = "Event 3 Completed" }
    ];
}
```

**Explanation:**

1. A `List<BitTimelineItem>` is created in the `@code` block.
2. Each `BitTimelineItem` defines at least `PrimaryText`. `SecondaryText` is optional.
3. The list is passed to the `Items` parameter of `<BitTimeline>`.
4. The timeline renders vertically by default.

### 4.2 Horizontal Orientation

Set the `Horizontal` parameter to `true`.

**Example (`.razor`):**

```cshtml
<BitTimeline Horizontal Items="basicItems" />

@code {
    // basicItems list remains the same as above
    private List<BitTimelineItem> basicItems =
    [
        new() { PrimaryText = "Step 1" },
        new() { PrimaryText = "Step 2", SecondaryText = "Approval" },
        new() { PrimaryText = "Step 3" }
    ];
}
```

### 4.3 Disabling Items

Items can be disabled individually via the `IsEnabled` property on `BitTimelineItem`, or the entire timeline can be disabled using the `IsEnabled` parameter on `BitTimeline`.

**Example (`.razor`):**

```cshtml
@* Disable the whole timeline *@
<BitTimeline Horizontal Items="basicItems" IsEnabled="false" />
<hr />
@* Disable a specific item *@
<BitTimeline Horizontal Items="disabledItems" />

@code {
    private List<BitTimelineItem> basicItems =
    [
        new() { PrimaryText = "Item 1" },
        new() { PrimaryText = "Item 2" },
        new() { PrimaryText = "Item 3" }
    ];

    private List<BitTimelineItem> disabledItems =
    [
        new() { PrimaryText = "Item A - Enabled" },
        new() { PrimaryText = "Item B - Disabled", SecondaryText = "Cannot click", IsEnabled = false },
        new() { PrimaryText = "Item C - Enabled" }
    ];
}
```

### 4.4 Variants

Control the visual style using the `Variant` parameter.

**Parameter:** `Variant` (Enum: `BitVariant.Fill` (default), `BitVariant.Outline`, `BitVariant.Text`)

**Example (`.razor`):**

```cshtml
<BitTimeline Horizontal Variant="BitVariant.Fill" Items="basicItems" />
<BitTimeline Horizontal Variant="BitVariant.Outline" Items="basicItems" />
<BitTimeline Horizontal Variant="BitVariant.Text" Items="basicItems" />

@code {
    // basicItems list remains the same as above
    private List<BitTimelineItem> basicItems = [ /* ... */ ];
}
```

### 4.5 Icons

Assign an icon to each item using the `IconName` property (`BitIconName` enum).

**Example (`.razor`):**

```cshtml
<BitTimeline Horizontal Items="iconItems" />

@code {
    private List<BitTimelineItem> iconItems =
    [
        new() { PrimaryText = "Create", IconName = BitIconName.Add },
        new() { PrimaryText = "Edit", IconName = BitIconName.Edit, IsEnabled = false },
        new() { PrimaryText = "Delete", IconName = BitIconName.Delete }
    ];
}
```

### 4.6 Item Reversal

Display items on alternating sides (vertical) or flip their content position (horizontal). Set `Reversed="true"` on the `BitTimeline` to reverse all items, or on individual `BitTimelineItem` objects.

**Example (`.razor`):**

```cshtml
@* Reverse all items in the timeline *@
<BitTimeline Items="basicItems" Reversed />
<hr/>
@* Reverse only the second item *@
<BitTimeline Items="reversedItems" />
<hr />
@* Horizontal reversed timeline *@
<BitTimeline Horizontal Items="basicItems" Reversed />
<hr />
@* Horizontal with one reversed item *@
<BitTimeline Horizontal Items="reversedItems" />

@code {
    private List<BitTimelineItem> basicItems =
    [
        new() { PrimaryText = "Item 1" },
        new() { PrimaryText = "Item 2" },
        new() { PrimaryText = "Item 3" }
    ];

    private List<BitTimelineItem> reversedItems =
    [
        new() { PrimaryText = "Normal Item 1" },
        new() { PrimaryText = "Reversed Item 2", Reversed = true }, // Individual item reversed
        new() { PrimaryText = "Normal Item 3" }
    ];
}
```

### 4.7 Custom Templates

Override default rendering using `RenderFragment` properties on `BitTimelineItem`:

* `PrimaryContent`: Replaces the `PrimaryText`.
* `SecondaryContent`: Replaces the `SecondaryText`.
* `DotTemplate`: Replaces the default dot/icon.
* `ItemTemplate`: Replaces the *entire* rendering for the item (use with caution, may break layout).

**Example (`.razor`):**

```cshtml
<style>
    .custom-dot-template {
        z-index: 1; /* Ensure it's above the line */
        border-radius: 50%;
        background-color: tomato;
        width: 30px; /* Match loading indicator size */
        height: 30px;
        display: flex;
        align-items: center;
        justify-content: center;
    }
</style>

<BitTimeline Items="templateItems" />

@code {
    private List<BitTimelineItem> templateItems =
    [
        new() // Item 1
        {
            PrimaryContent = (item => @<BitPersona PrimaryText="Annie Lindqvist" Size="@BitPersonaSize.Size32" ImageUrl="...female.png" />),
            DotTemplate = (item => @<div class="custom-dot-template"><BitRingLoading CustomSize="30" Color="BitColor.Tertiary" /></div>),
            SecondaryContent = (item => @<div style="display: flex; align-items: center; gap: 0.5rem;"><BitIcon IconName="Accept" Style="color: limegreen;" /> <BitLabel>Software Engineer</BitLabel></div>)
        },
        new() // Item 2 (Reversed)
        {
            PrimaryContent = (item => @<BitPersona PrimaryText="Saleh Khafan" Size="@BitPersonaSize.Size32" />),
            DotTemplate = (item => @<div class="custom-dot-template"><BitSpinnerLoading CustomSize="30" Color="BitColor.Tertiary" /></div>),
            SecondaryContent = (item => @<div style="display: flex; align-items: center; gap: 0.5rem;"><BitIcon IconName="Accept" Style="color: limegreen;" /> <BitLabel>Co-Founder & CTO</BitLabel></div>),
            Reversed = true
        },
        new() // Item 3
        {
            PrimaryContent = (item => @<BitPersona PrimaryText="Ted Randall" Size="@BitPersonaSize.Size32" ImageUrl="...male.png" />),
            DotTemplate = (item => @<div class="custom-dot-template"><BitRollerLoading CustomSize="30" Color="BitColor.Tertiary" /></div>),
            SecondaryContent = (item => @<div style="display: flex; align-items: center; gap: 0.5rem;"><BitIcon IconName="Accept" Style="color: limegreen;" /> <BitLabel>Project Manager</BitLabel></div>)
        }
    ];
}

```

### 4.8 Color & Theming

Apply semantic colors (`BitColor` enum) to the entire timeline or individual items. Works with different `Variant`s.

**Example (`.razor`):**

```cshtml
<BitTimeline Horizontal Color="BitColor.Success" Items="iconItems" />
<BitTimeline Horizontal Color="BitColor.Warning" Variant="BitVariant.Outline" Items="iconItems" />
<BitTimeline Horizontal Color="BitColor.Error" Variant="BitVariant.Text" Items="iconItems" />

@* You can also set Color on individual BitTimelineItem objects *@

@code {
    private List<BitTimelineItem> iconItems =
    [
        new() { PrimaryText = "Create", IconName = BitIconName.Add },
        new() { PrimaryText = "Edit", IconName = BitIconName.Edit },
        new() { PrimaryText = "Delete", IconName = BitIconName.Delete }
    ];
}
```

### 4.9 Size

Adjust the overall size of the timeline elements.

**Parameter:** `Size` (Enum: `BitSize.Small`, `BitSize.Medium` (default), `BitSize.Large`)

**Example (`.razor`):**

```cshtml
<BitTimeline Horizontal Size="BitSize.Small" Items="iconItems" />
<BitTimeline Horizontal Size="BitSize.Medium" Variant="BitVariant.Outline" Items="iconItems" />
<BitTimeline Horizontal Size="BitSize.Large" Variant="BitVariant.Text" Items="iconItems" />

@code {
    // iconItems list remains the same as above
    private List<BitTimelineItem> iconItems = [ /* ... */ ];
}
```

### 4.10 Styling

Apply custom styles using `Style` and `Class` on `BitTimeline` and `BitTimelineItem`. Use `Styles` and `Classes` (of type `BitTimelineClassStyles`) on `BitTimeline` for targeting internal parts like the dot, icon, divider, etc.

**Example (`.razor`):**

```cshtml
<style>
    .custom-timeline-class { margin: 2rem; background-color: #eee; padding: 1rem; }
    .custom-timeline-item-class { font-style: italic; }
    .custom-dot { border: 2px dashed blueviolet; box-shadow: blueviolet 0 0 0.5rem; }
    .custom-icon { color: blueviolet !important; /* May need !important */ }
    .custom-divider::before { background: linear-gradient(to bottom, red, orange); }
    .custom-item-text-color { color: darkcyan; }
</style>

@* Style on component *@
<BitTimeline Style="border: 2px solid green; padding: 1rem;" Items="basicItems" />

@* Class on component *@
<BitTimeline Horizontal Class="custom-timeline-class" Items="basicItems" />

@* Style/Class on items *@
<BitTimeline Items="styleClassItems" />

@* Using Styles parameter *@
<BitTimeline Items="iconItems"
             Styles="@(new() { Icon = "color: red; font-size: 1.2em;", Dot = "background-color: yellow;" })" />

@* Using Classes parameter *@
<BitTimeline Items="iconItems" Variant="BitVariant.Outline"
             Classes="@(new() { Dot = "custom-dot", Icon = "custom-icon", Divider = "custom-divider", Item = "custom-item-text-color" })" />

@code {
    private List<BitTimelineItem> basicItems = [ /* ... */ ];
    private List<BitTimelineItem> iconItems = [ /* ... */ ];

    private List<BitTimelineItem> styleClassItems =
    [
        new() { PrimaryText = "Styled Item", Style = "background-color: lightyellow;", IconName = BitIconName.Brush },
        new() { PrimaryText = "Classed Item", Class = "custom-timeline-item-class", IconName = BitIconName.FormatPainter }
    ];
}
```

---

## 5. API Reference

### `BitTimeline<TItem>` Parameters

| Name            | Type                                   | Default Value        | Description                                                                                                      |
| :-------------- | :------------------------------------- | :------------------- | :--------------------------------------------------------------------------------------------------------------- |
| `Items`         | `IEnumerable<TItem>`                   | `new List<TItem>()`  | List of items to render. `TItem` can be `BitTimelineItem` or a custom type (requires `NameSelectors`).          |
| `NameSelectors` | `BitTimelineNameSelectors<TItem>?`     | `null`               | **Required when `TItem` is not `BitTimelineItem`**. Maps properties of `TItem` to timeline display attributes. |
| `ChildContent`  | `RenderFragment?`                      | `null`               | Defines items using `<BitTimelineOption>` child components. Use this **or** `Items`.                             |
| `Options`       | `RenderFragment?`                      | `null`               | Alias for `ChildContent`.                                                                                        |
| `Horizontal`    | `bool`                                 | `false`              | Renders the timeline horizontally instead of vertically.                                                         |
| `Reversed`      | `bool`                                 | `false`              | Reverses the direction/layout of all items in the timeline. Individual items can also be reversed.               |
| `OnItemClick`   | `EventCallback<TItem>`                 |                      | Callback invoked when an enabled timeline item is clicked. The clicked item (`TItem`) is passed as argument.     |
| `Color`         | `BitColor?`                            | `null`               | Overall color theme (Primary, Success, Warning, Error, etc.). Can be overridden by item-level color.              |
| `Size`          | `BitSize?`                             | `null` (`Medium`)    | Overall size (Small, Medium, Large) affecting text, dots, and spacing.                                           |
| `Variant`       | `BitVariant?`                          | `null` (`Fill`)      | Visual style (Fill, Outline, Text).                                                                              |
| `Classes`       | `BitTimelineClassStyles?`              | `null`               | Custom CSS classes for internal parts (root, item, dot, divider, text, icon).                                    |
| `Styles`        | `BitTimelineClassStyles?`              | `null`               | Custom inline styles for internal parts.                                                                         |
| **Inherited**   |                                        |                      | *Includes `AriaLabel`, `Class`, `Dir`, `HtmlAttributes`, `Id`, `IsEnabled`, `Style`, `Visibility` from `BitComponentBase`.* |

### `BitTimelineItem` Properties (Used with `Items` parameter)

| Name               | Type                                | Default Value | Description                                                     |
| :----------------- | :---------------------------------- | :------------ | :-------------------------------------------------------------- |
| `PrimaryText`      | `string?`                           | `null`        | Main text content for the item.                                 |
| `SecondaryText`    | `string?`                           | `null`        | Additional descriptive text below/beside the primary text.      |
| `PrimaryContent`   | `RenderFragment<BitTimelineItem>?`  | `null`        | Custom `RenderFragment` to replace `PrimaryText`.               |
| `SecondaryContent` | `RenderFragment<BitTimelineItem>?`  | `null`        | Custom `RenderFragment` to replace `SecondaryText`.             |
| `DotTemplate`      | `RenderFragment<BitTimelineItem>?`  | `null`        | Custom `RenderFragment` for the item's dot/icon area.           |
| `ItemTemplate`     | `RenderFragment<BitTimelineItem>?`  | `null`        | Custom `RenderFragment` to replace the entire item's rendering. |
| `IconName`         | `string?`                           | `null`        | Name of the Fluent UI icon to display in the dot position.      |
| `Color`            | `BitColor?`                         | `null`        | Specific color for this item, overriding the timeline's color.  |
| `Size`             | `BitSize?`                          | `null`        | Specific size for this item, overriding the timeline's size.    |
| `Reversed`         | `bool`                              | `false`       | Reverses the direction/layout specifically for this item.       |
| `HideDot`          | `bool`                              | `false`       | Hides the dot (and its connector line segment) for this item. |
| `IsEnabled`        | `bool`                              | `true`        | Enables/disables interaction (`OnClick`) for this item.         |
| `OnClick`          | `EventCallback`                     |               | Callback invoked when this specific item is clicked.            |
| `Key`              | `string?`                           | `null`        | Unique key for the item, useful for dynamic scenarios.          |
| `Style`            | `string?`                           | `null`        | Custom inline style attribute for the item's root element.      |
| `Class`            | `string?`                           | `null`        | Custom CSS class for the item's root element.                   |

### `BitTimelineOption` Parameters (Used with `ChildContent`/`Options`)

*(These parameters mirror `BitTimelineItem` properties but are used declaratively)*

| Name               | Type                                  | Default Value | Description                                                       |
| :----------------- | :------------------------------------ | :------------ | :---------------------------------------------------------------- |
| `PrimaryText`      | `string?`                             | `null`        | Main text content.                                              |
| `SecondaryText`    | `string?`                             | `null`        | Additional descriptive text.                                      |
| `PrimaryContent`   | `RenderFragment<BitTimelineOption>?`  | `null`        | Custom `RenderFragment` for primary content.                      |
| `SecondaryContent` | `RenderFragment<BitTimelineOption>?`  | `null`        | Custom `RenderFragment` for secondary content.                    |
| `DotTemplate`      | `RenderFragment<BitTimelineOption>?`  | `null`        | Custom `RenderFragment` for the dot area.                         |
| `ItemTemplate`     | `RenderFragment<BitTimelineOption>?`  | `null`        | Custom `RenderFragment` for the entire item.                      |
| `IconName`         | `string?`                             | `null`        | Icon to display in the dot position.                              |
| `Color`            | `BitColor?`                           | `null`        | Specific color for this option.                                   |
| `Size`             | `BitSize?`                            | `null`        | Specific size for this option.                                    |
| `Reversed`         | `bool`                                | `false`       | Reverses the direction/layout for this option.                    |
| `HideDot`          | `bool`                                | `false`       | Hides the dot for this option.                                    |
| `IsEnabled`        | `bool`                                | `true`        | Enables/disables interaction (`OnClick`) for this option.         |
| `OnClick`          | `EventCallback`                       |               | Callback invoked when this option is clicked.                     |
| `Key`              | `string?`                             | `null`        | Unique key for the option.                                        |
| `Style`            | `string?`                             | `null`        | Custom inline style attribute for the option's root element.      |
| `Class`            | `string?`                             | `null`        | Custom CSS class for the option's root element.                   |
| **Inherited**      |                                       |               | *Includes `Visibility` etc. from `BitComponentBase`.*             |

### `BitTimelineNameSelectors<TItem>` Properties

(Used when `Items` contains custom objects of type `TItem`)

| Name               | Type                                         | Default Name (Based on `BitTimelineItem`) | Description                                                          |
| :----------------- | :------------------------------------------- | :---------------------------------------- | :------------------------------------------------------------------- |
| `PrimaryText`      | `BitNameSelectorPair<TItem, string?>`        | `PrimaryText`                             | Selector for the main text property in `TItem`.                    |
| `SecondaryText`    | `BitNameSelectorPair<TItem, string?>`        | `SecondaryText`                           | Selector for the secondary text property in `TItem`.                 |
| `PrimaryContent`   | `BitNameSelectorPair<TItem, RenderFragment?>`| `PrimaryContent`                          | Selector for the primary content `RenderFragment` property in `TItem`.|
| `SecondaryContent` | `BitNameSelectorPair<TItem, RenderFragment?>`| `SecondaryContent`                        | Selector for the secondary content `RenderFragment` property in `TItem`.|
| `DotTemplate`      | `BitNameSelectorPair<TItem, RenderFragment?>`| `DotTemplate`                             | Selector for the dot `RenderFragment` property in `TItem`.          |
| `ItemTemplate`     | `BitNameSelectorPair<TItem, RenderFragment?>`| `Template` *(Note: `Template` in API table)* | Selector for the entire item `RenderFragment` property in `TItem`.|
| `IconName`         | `BitNameSelectorPair<TItem, string?>`        | `IconName`                                | Selector for the icon name property in `TItem`.                      |
| `Color`            | `BitNameSelectorPair<TItem, BitColor?>`      | `Color`                                   | Selector for the `BitColor` property in `TItem`.                   |
| `Size`             | `BitNameSelectorPair<TItem, BitSize?>`       | `Size`                                    | Selector for the `BitSize` property in `TItem`.                    |
| `Reversed`         | `BitNameSelectorPair<TItem, bool>`           | `Reversed` *(Type mismatch in API table?)* | Selector for the `bool` reversed property in `TItem`.              |
| `HideDot`          | `BitNameSelectorPair<TItem, bool>`           | `HideDot`                                 | Selector for the `bool` hide dot property in `TItem`.              |
| `IsEnabled`        | `BitNameSelectorPair<TItem, bool>`           | `IsEnabled`                               | Selector for the `bool` enabled property in `TItem`.                 |
| `OnClick`          | `BitNameSelectorPair<TItem, Action<TItem>?>` | `OnClick`                                 | Selector for the `Action<TItem>` click handler property in `TItem`. |
| `Key`              | `BitNameSelectorPair<TItem, string?>`        | `Key`                                     | Selector for the unique key property in `TItem`.                     |
| `Style`            | `BitNameSelectorPair<TItem, string?>`        | `Style`                                   | Selector for the inline style property in `TItem`.                   |
| `Class`            | `BitNameSelectorPair<TItem, string?>`        | `Class`                                   | Selector for the CSS class property in `TItem`.                      |

*(`BitNameSelectorPair<TItem, TProp>` has `Name` (string) and `Selector` (Func<TItem, TProp>) properties)*

### `BitTimelineClassStyles` Properties

(Used with `Classes` and `Styles` parameters on `BitTimeline`)

| Name               | Type      | Description                                          |
| :----------------- | :-------- | :--------------------------------------------------- |
| `Root`             | `string?` | Styles/classes for the main root element.            |
| `Item`             | `string?` | Styles/classes applied to each timeline item wrapper.|
| `PrimaryContent`   | `string?` | Styles/classes for the primary content container.    |
| `PrimaryText`      | `string?` | Styles/classes applied to the primary text element.  |
| `SecondaryContent` | `string?` | Styles/classes for the secondary content container.  |
| `SecondaryText`    | `string?` | Styles/classes applied to the secondary text element.|
| `Divider`          | `string?` | Styles/classes for the line connecting the dots.     |
| `Dot`              | `string?` | Styles/classes for the dot element itself.           |
| `Icon`             | `string?` | Styles/classes applied to the icon within the dot.   |

### Inherited `BitComponentBase` Parameters & Members

*(Refer to previous component documentation (e.g., BitSwiper) for details on `AriaLabel`, `Class`, `Dir`, `IsEnabled`, `Style`, `Visibility`, `UniqueId`, `RootElement`, etc.)*

### Enums

* **`BitVariant`**: `Fill` (0), `Outline` (1), `Text` (2)
* **`BitColor`**: `Primary` (0), `Secondary` (1), `Tertiary` (2), `Info` (3), `Success` (4), `Warning` (5), `SevereWarning` (6), `Error` (7)
* **`BitSize`**: `Small` (0), `Medium` (1), `Large` (2)
* **`BitVisibility`**: `Visible` (0), `Hidden` (1), `Collapsed` (2)
* **`BitDir`**: `Ltr` (0), `Rtl` (1), `Auto` (2)

---

## 6. Best Practices & Considerations

* **Choose the Right API:** Use `BitTimelineItem` for simple data structures, `BitTimelineOption` for declarative markup, and custom generics + `NameSelectors` for binding to existing complex models.
* **Content Length:** Keep `PrimaryText` and `SecondaryText` reasonably concise, especially in horizontal mode, to avoid layout issues. Use `PrimaryContent`/`SecondaryContent` for more complex layouts within an item.
* **Templates:** When using custom templates (`DotTemplate`, `PrimaryContent`, etc.), ensure they fit within the expected layout and don't interfere with the timeline structure (lines, alignment).
* **Reversed Layout:** Use the `Reversed` property thoughtfully to enhance readability, especially in vertical mode where alternating sides can prevent text overlap.
* **Accessibility:** Provide an `AriaLabel` for the overall timeline. Ensure content within items is accessible. If items are clickable, ensure they have sufficient visual indication and work with keyboard navigation.
* **Performance:** For extremely long timelines, consider if this component is the best fit or if pagination/virtualization (not built-in here) might be needed.

---

## 7. Further Information (Source Links)

* **Component Source Code:** [BitTimeline.razor on GitHub](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Bit.BlazorUI/Components/Lists/Timeline/BitTimeline.razor)
* **Demo Page Source Code:** [BitTimelineDemo.razor on GitHub](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Lists/Timeline/BitTimelineDemo.razor)
* **Project Issues:** [File an Issue on GitHub](https://github.com/bitfoundation/bitplatform/issues/new/choose)
* **Project Discussions:** [Start a Discussion on GitHub](https://github.com/bitfoundation/bitplatform/discussions/new/choose)
