<!--
AI Agent Reference File: BitPivot Component

Purpose: This file provides detailed information about the Blazor `BitPivot` component.
Use this reference when generating, analyzing, or modifying code involving BitPivot.
Focus on its purpose (tabbed navigation), structure (BitPivot wrapping BitPivotItem), key parameters (SelectedKey, Position, HeaderType, Alignment, OverflowBehavior, HeaderOnly), event handling (OnItemClick, OnChange), and customization options (templates, styles, classes).
-->

# BitPivot Component Reference (Blazor)

## Overview

The `BitPivot` component implements the "tabs" pattern, used for navigating between distinct views or sections of content within the same context. It displays a set of headers (pivots or tabs), and selecting a header reveals its associated content pane.

It's ideal for organizing related but separate information, commonly seen in settings pages, user profiles, dashboards, or any interface requiring distinct content categories accessible from a single location.

**Related Terms:** Tab, TabPage, Tab Control

## Core Concepts

*   **Structure:** The main component is `<BitPivot>`, which acts as a container. Each navigable section is defined by a nested `<BitPivotItem>` component.
*   **Headers & Content:** Each `<BitPivotItem>` defines both its header (the clickable tab/link) and its body content (what's displayed when the item is selected).
*   **Selection:** Navigation occurs by clicking on the headers. The `BitPivot` component manages which `BitPivotItem`'s content is currently visible. Selection can be controlled programmatically using keys.
*   **Declarative Definition:** The primary way to define pivots is by nesting `<BitPivotItem>` components directly within the `<BitPivot>` tag in your Razor markup.

---

## Usage

### Basic Usage

Define `<BitPivotItem>` elements inside a `<BitPivot>`. Each item requires at least a `HeaderText` and contains the content for its pane.

```razor
<BitPivot>
    <BitPivotItem HeaderText="File">
        <h3>Pivot #1</h3>
        <p>Content for the File tab.</p>
    </BitPivotItem>
    <BitPivotItem HeaderText="Shared with me">
        <h3>Pivot #2</h3>
        <p>Content for the Shared tab.</p>
    </BitPivotItem>
    <BitPivotItem HeaderText="Recent">
        <h3>Pivot #3</h3>
        <p>Content for the Recent tab.</p>
    </BitPivotItem>
</BitPivot>
```

**Explanation:**

* The `<BitPivot>` component manages the overall tab structure and content switching.
* Each `<BitPivotItem>` represents one tab/pivot.
* `HeaderText` defines the text shown in the tab header.
* The content placed inside `<BitPivotItem>` (or within its `<Body>` template) is displayed when that item is active.

### Adding Icons and Item Counts

Enhance headers with icons (`IconName`) and counts (`ItemCount`).

```razor
<BitPivot>
    <BitPivotItem HeaderText="Files" IconName="@BitIconName.FabricFolder">
        <h1>Content for Files</h1>
    </BitPivotItem>
    <BitPivotItem HeaderText="Shared with me" ItemCount="32">
        <h1>Content for Shared</h1>
    </BitPivotItem>
    <BitPivotItem HeaderText="Recent" IconName="@BitIconName.Recent" ItemCount="12">
        <h1>Content for Recent</h1>
    </BitPivotItem>
</BitPivot>
```

**Explanation:**

* `IconName`: Specifies a `BitIconName` to display in the header.
* `ItemCount`: Displays a number (typically in parentheses) next to the header text.

### Header Type (`HeaderType`)

Change the visual style of the headers.

```razor
<BitPivot HeaderType="BitPivotHeaderType.Tab">
    <BitPivotItem HeaderText="File tab"> ... </BitPivotItem>
    <BitPivotItem HeaderText="Shared with me tab"> ... </BitPivotItem>
    <BitPivotItem HeaderText="Recent tab"> ... </BitPivotItem>
</BitPivot>

@* Default is BitPivotHeaderType.Link *@
<BitPivot HeaderType="BitPivotHeaderType.Link">
    <BitPivotItem HeaderText="File link"> ... </BitPivotItem>
    <BitPivotItem HeaderText="Shared with me link"> ... </BitPivotItem>
    <BitPivotItem HeaderText="Recent link"> ... </BitPivotItem>
</BitPivot>
```

**Explanation:**

* `HeaderType="BitPivotHeaderType.Tab"`: Renders headers with a distinct tab-like appearance (often with borders/background).
* `HeaderType="BitPivotHeaderType.Link"`: (Default) Renders headers as underlined text links.

### Sizing (`Size`)

Control the size (padding, font size) of the pivot headers.

```razor
<BitPivot Size="BitSize.Small"> ... </BitPivot>
<BitPivot Size="BitSize.Medium"> ... </BitPivot> @* Default *@
<BitPivot Size="BitSize.Large"> ... </BitPivot>
```

**Explanation:**

* `Size="BitSize..."`: Affects the visual size of the tab headers (Small, Medium, Large).

### Header Position (`Position`)

Place the headers relative to the content area.

```razor
<BitPivot Position="BitPivotPosition.Top"> ... </BitPivot>    @* Default *@
<BitPivot Position="BitPivotPosition.Bottom"> ... </BitPivot>
<BitPivot Position="BitPivotPosition.Left"> ... </BitPivot>
<BitPivot Position="BitPivotPosition.Right"> ... </BitPivot>
```

**Explanation:**

* `Position="BitPivotPosition..."`: Controls whether headers appear above, below, to the left, or to the right of the content panes.

### Header Alignment (`Alignment`)

Align the headers within their container (especially noticeable when headers don't fill the width/height).

```razor
<BitPivot Alignment="BitAlignment.Start"> ... </BitPivot>  @* Default (Left for LTR, Right for RTL) *@
<BitPivot Alignment="BitAlignment.Center"> ... </BitPivot>
<BitPivot Alignment="BitAlignment.End"> ... </BitPivot>    @* (Right for LTR, Left for RTL) *@
```

**Explanation:**

* `Alignment="BitAlignment..."`: Aligns the group of headers horizontally (for Top/Bottom position) or vertically (for Left/Right position).

### Binding and Selection (`SelectedKey`, `DefaultSelectedKey`, `OnItemClick`, `OnChange`)

Manage which pivot item is selected. Requires setting a unique `Key` attribute on each `BitPivotItem`.

```razor
<BitPivot @bind-SelectedKey="currentKey">
    <BitPivotItem Key="Key1" HeaderText="Item One"> ... </BitPivotItem>
    <BitPivotItem Key="Key2" HeaderText="Item Two"> ... </BitPivotItem>
    <BitPivotItem Key="Key3" HeaderText="Item Three"> ... </BitPivotItem>
</BitPivot>

<BitButton OnClick="() => currentKey = "Key2"">Select Item Two</BitButton>

<hr />

<BitPivot DefaultSelectedKey="Foo" OnChange="HandlePivotChange">
     <BitPivotItem Key="Foo" HeaderText="Foo"> ... </BitPivotItem>
     <BitPivotItem Key="Bar" HeaderText="Bar"> ... </BitPivotItem>
</BitPivot>
<div>Last Changed To: @lastChangedKey</div>

@code {
    private string currentKey = "Key1"; // Initial selection for binding example
    private string lastChangedKey = "Foo"; // Store result from OnChange

    private void HandlePivotChange(BitPivotItem item)
    {
        lastChangedKey = item?.Key;
        Console.WriteLine($"Pivot changed to: {item?.Key}");
    }
}
```

**Explanation:**

* `Key`: **Required** on each `BitPivotItem` when using binding or `DefaultSelectedKey`. Must be unique.
* `DefaultSelectedKey`: Sets the initially selected item by its `Key`.
* `@bind-SelectedKey`: Provides two-way binding. Clicking a tab updates the bound variable, and changing the variable updates the selected tab.
* `OnItemClick`: An `EventCallback<BitPivotItem>` triggered whenever *any* pivot header is clicked.
* `OnChange`: An `EventCallback<BitPivotItem>` triggered only when the *selected* pivot item actually changes.

### Detached Mode (`HeaderOnly`)

Render *only* the pivot headers, without the content panes. Useful when the content associated with each tab is displayed elsewhere in the UI, controlled by the selected key.

```razor
<div style="border:1px solid gray; padding:10px; min-height: 50px;">
    @* Manually render content based on the selected key *@
    @if (detachedKey == "Foo") { <div>Content for Foo</div> }
    else if (detachedKey == "Bar") { <div>Content for Bar</div> }
    else { <div>Select a tab</div> }
</div>

<hr />

<BitPivot HeaderOnly="true"
          DefaultSelectedKey="Foo"
          OnItemClick="(item => detachedKey = item?.Key)">
    <BitPivotItem HeaderText="Foo" Key="Foo" />
    <BitPivotItem HeaderText="Bar" Key="Bar" />
</BitPivot>

@code {
    private string detachedKey = "Foo";
}
```

**Explanation:**

* `HeaderOnly="true"`: Instructs the `BitPivot` component to *not* render the content area (`.bit-pvt-cct`).
* You typically use `OnItemClick` or `@bind-SelectedKey` to get the selected item's key and then conditionally render the appropriate content elsewhere on the page.

### Overflow Behavior (`OverflowBehavior`)

How to handle headers when they don't fit in the available space.

```razor
<div style="max-width: 250px; border: 1px dashed blue;">
    @* Default: None - headers might wrap or overflow *@
    <BitPivot> <BitPivotItem HeaderText="Very Long Header One" /> ... </BitPivot>

    @* Menu: Items that don't fit go into a dropdown menu *@
    <BitPivot OverflowBehavior="BitOverflowBehavior.Menu"> <BitPivotItem HeaderText="V L H One" /> ...</BitPivot>

    @* Scroll: A horizontal scrollbar appears for the headers *@
    <BitPivot OverflowBehavior="BitOverflowBehavior.Scroll"> <BitPivotItem HeaderText="V L H One" /> ... </BitPivot>
</div>
```

**Explanation:**

* `OverflowBehavior="BitOverflowBehavior..."`: Controls the behavior (`None`, `Menu`, `Scroll`) when headers exceed the container width (or height for Left/Right positions).

### Right-to-Left (`Dir`)

Renders the component layout and header order for RTL languages.

```razor
<div dir="rtl"> @* Container div recommended for proper layout *@
    <BitPivot Dir="BitDir.Rtl">
        <BitPivotItem HeaderText="فایل"> ... </BitPivotItem>
        <BitPivotItem HeaderText="اشتراک‌گذاری‌ها"> ... </BitPivotItem>
    </BitPivot>
</div>
```

---

## Customization

### Custom Templates (`<Header>`, `<Body>`)

Override the default rendering of individual pivot item headers and/or bodies.

```razor
<BitPivot>
    <BitPivotItem>
        <Header>
            <span style="color:red; font-weight:bold;">
                <BitIcon IconName="@BitIconName.Warning" /> Custom Header 1
            </span>
        </Header>
        <Body> @* Or just place content directly in BitPivotItem *@
            <h1>Custom Content Pane 1</h1>
        </Body>
    </BitPivotItem>
    <BitPivotItem HeaderText="Default Header 2"> @* Can mix with default headers *@
         <h1>Default Content Pane 2</h1>
         <p>Using ChildContent implicitly becomes the Body.</p>
    </BitPivotItem>
</BitPivot>
```

**Explanation:**

* Place custom markup inside `<Header>` within a `<BitPivotItem>` to completely control the header's appearance. `HeaderText`, `IconName`, `ItemCount` attributes on the `BitPivotItem` are ignored when a `<Header>` template is used.
* Place custom markup inside `<Body>` or directly within `<BitPivotItem>` (as `ChildContent`) to define the content pane for that item.

### Styling (`Style`, `Class`, `Styles`, `Classes`)

Apply custom CSS.

* **`Style` / `Class`:** Apply to the root `div` element of the `BitPivot` component.
* **`Styles` / `Classes` Parameters:** Provide `BitPivotClassStyles` objects to target internal elements like `Root`, `Header`, `Body`, `HeaderItem`, `SelectedItem`, `HeaderItemContent`, `HeaderIcon`, `HeaderText`, `HeaderItemCount`.

```razor
@* Direct Style/Class on root *@
<BitPivot Style="margin-bottom: 2rem;" Class="my-custom-pivot">
    ...
</BitPivot>

@* Granular styling via Styles *@
<BitPivot Styles="@(new BitPivotClassStyles {
                      Header = "background-color: #eee; border-bottom: 2px solid blue;",
                      HeaderItem = "padding: 0.5rem 1rem;",
                      SelectedItem = "background-color: white; border-bottom: 2px solid transparent; margin-bottom: -2px;",
                      Body = "padding: 1rem; border: 1px solid #eee; border-top: none;"
                  })">
    ...
</BitPivot>

@* Granular styling via Classes (assuming CSS definitions exist) *@
<BitPivot Classes="@(new BitPivotClassStyles {
                      Root = "custom-pivot-root",
                      HeaderItem = "custom-pivot-header-item",
                      SelectedItem = "custom-pivot-selected-item",
                      Body = "custom-pivot-body"
                  })">
    ...
</BitPivot>
```

---

## Key Parameters (`BitPivot`)

<!-- AI: Focus on these common parameters when generating BitPivot code. -->

| Parameter          | Type                       | Default                    | Description                                                           |
| :----------------- | :------------------------- | :------------------------- | :-------------------------------------------------------------------- |
| `ChildContent`     | `RenderFragment?`          | `null`                     | Defines the `<BitPivotItem>` components.                              |
| `SelectedKey`      | `string?`                  | `null`                     | Key of the selected item. Use `@bind-SelectedKey` for two-way binding. |
| `DefaultSelectedKey`| `string?`                  | `null`                     | Key of the item selected initially.                                   |
| `HeaderType`       | `BitPivotHeaderType`       | `BitPivotHeaderType.Link`  | Visual style of the headers (Link or Tab).                            |
| `Position`         | `BitPivotPosition`         | `BitPivotPosition.Top`     | Position of the header relative to the content (Top, Bottom, Left, Right). |
| `Alignment`        | `BitAlignment?`            | `null` (`Start`)           | Alignment of the headers within their container.                      |
| `OverflowBehavior` | `BitOverflowBehavior`      | `BitOverflowBehavior.None` | How to handle headers that don't fit (None, Menu, Scroll).            |
| `HeaderOnly`       | `bool`                     | `false`                    | If true, only renders the headers, not the content pane container.    |
| `Size`             | `BitSize?`                 | `null` (`Medium`)          | Size of the header items (Small, Medium, Large).                      |
| `OnItemClick`      | `EventCallback<BitPivotItem>`| -                          | Callback when any header item is clicked.                             |
| `OnChange`         | `EventCallback<BitPivotItem>`| -                          | Callback when the selected item changes.                              |
| `IsEnabled`        | `bool`                     | `true`                     | Enables/disables the entire Pivot control.                            |
| `Styles`           | `BitPivotClassStyles?`     | `null`                     | Custom inline styles for internal elements.                           |
| `Classes`          | `BitPivotClassStyles?`     | `null`                     | Custom CSS classes for internal elements.                             |
| `Dir`              | `BitDir?`                  | `null`                     | Sets the text direction (Ltr, Rtl, Auto).                             |

---

## `BitPivotItem` Parameters

<!-- AI: Use these attributes when defining BitPivotItem elements. -->

| Parameter    | Type                | Default          | Description                                                                 |
| :----------- | :------------------ | :--------------- | :-------------------------------------------------------------------------- |
| `ChildContent`| `RenderFragment?`   | `null`           | Content of the item's pane (rendered when selected). Alias of `<Body>`.     |
| `HeaderText` | `string?`           | `null`           | Text displayed in the header. Ignored if `<Header>` template is used.       |
| `Key`        | `string?`           | `null`           | **Required for binding/default selection.** Unique identifier for the item. |
| `IconName`   | `string?`           | `null`           | Icon to display in the header. Ignored if `<Header>` template is used.      |
| `ItemCount`  | `int`               | `0`              | Count displayed in the header. Ignored if `<Header>` template is used.      |
| `Header`     | `RenderFragment?`   | `null`           | Custom template for the item's header. Overrides `HeaderText`, etc.       |
| `Body`       | `RenderFragment?`   | `null`           | Explicit template for the item's content pane. Alias of `ChildContent`.     |
| `IsEnabled`  | `bool`              | `true`           | Whether this specific item can be selected.                               |
| `Visible`    | `bool`              | `true`           | Whether this item is rendered in the header list.                         |
| `Style`      | `string?`           | `null`           | Custom inline style for this item's *header* element.                     |
| `Class`      | `string?`           | `null`           | Custom CSS class for this item's *header* element.                        |
| `BodyStyle`  | `string?`           | `null`           | Custom inline style for this item's *body content* container.             |
| `BodyClass`  | `string?`           | `null`           | Custom CSS class for this item's *body content* container.                |

---

## Event Handling

* **`OnItemClick(BitPivotItem item)`**: Fires when *any* pivot header is clicked, providing the corresponding `BitPivotItem`. Useful even in `HeaderOnly` mode.
* **`OnChange(BitPivotItem item)`**: Fires *only* when the *selected* pivot item changes (i.e., a different tab is selected). Provides the newly selected `BitPivotItem`.

---

## API Parameter Tables (Detailed)

*(Includes inherited parameters and class style properties)*

*(Refer to the tables in the provided HTML source, summarized in the sections above.)*

---

## Relevant Enums

* **`BitPivotHeaderType`**: `Link` (default), `Tab`
* **`BitPivotPosition`**: `Top` (default), `Bottom`, `Left`, `Right`
* **`BitAlignment`**: `Start` (default), `End`, `Center`, `SpaceBetween`, `SpaceAround`, `SpaceEvenly`, `Baseline`, `Stretch`
* **`BitOverflowBehavior`**: `None` (default), `Menu`, `Scroll`
* **`BitSize`**: `Small`, `Medium` (default), `Large`
* **`BitDir`**: `Ltr`, `Rtl`, `Auto`
* **`BitVisibility`**: `Visible` (default), `Hidden`, `Collapsed`

---

## AI Agent Guidance Summary

* Use `<BitPivot>` to create tabbed interfaces for navigating between content sections.
* Define tabs using nested `<BitPivotItem>` components.
* Each `<BitPivotItem>` needs a way to identify its header (`HeaderText` attribute or `<Header>` template) and contains the content for its pane (directly inside, or in `<Body>` template).
* **Selection:**
  * Use `Key` on `<BitPivotItem>` if you need binding or default selection.
  * Use `DefaultSelectedKey` for initial selection.
  * Use `@bind-SelectedKey` for two-way programmatic control.
  * Use `OnChange` event to react to selection changes.
  * Use `OnItemClick` to react to any header click.
* **Appearance:**
  * `HeaderType`: `Link` (default) or `Tab`.
  * `Position`: `Top` (default), `Bottom`, `Left`, `Right`.
  * `Alignment`: `Start` (default), `Center`, `End`, etc.
  * `Size`: `Small`, `Medium` (default), `Large`.
* **Customization:**
  * Use `IconName` and `ItemCount` on `<BitPivotItem>` for simple header additions.
  * Use `<Header>` and `<Body>` templates within `<BitPivotItem>` for full control over rendering.
  * Use `Style`/`Class` on `<BitPivot>` or `Styles`/`Classes` (`BitPivotClassStyles`) for CSS customization.
* **Detached Mode:** Use `HeaderOnly="true"` to render only the navigation headers and handle content display externally based on the selected key.
* **Overflow:** Use `OverflowBehavior` (`None`, `Menu`, `Scroll`) to manage many tabs.
* **RTL:** Use `Dir="BitDir.Rtl"`.

