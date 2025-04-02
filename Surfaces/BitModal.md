# BitModal Component

**Purpose:** This document provides a detailed reference for the `BitModal` Blazor UI component. It is intended to be used by an AI agent (like GitHub Copilot, Cursor, etc.) to understand the component's functionality, usage patterns, and API, enabling the agent to provide accurate code suggestions and assistance related to `BitModal`.

**Source:** This information is derived from the Bit Blazor UI documentation for the `BitModal` component.

---

## Overview

*   **Component:** `BitModal`
*   **Purpose:** Creates temporary pop-up windows (modals) that demand user interaction and take focus from the main page. Ideal for displaying lengthy content (like privacy policies) or forms requiring multiple actions (like settings). Differentiated from `BitDialog` which is generally for simpler, shorter interactions.
*   **Library:** Bit Blazor UI (`Bit.BlazorUI`)

---

## Usage Examples

Here are common ways to use the `BitModal` component. The state (open/closed) is typically managed by a boolean variable bound to the `IsOpen` parameter.

### 1. Basic Modal

This example shows the simplest way to use `BitModal`. A button toggles a boolean (`isOpenBasic`), which controls the modal's visibility via `@bind-IsOpen`.

```cshtml
<BitButton OnClick="() => isOpenBasic = true">Open Modal</BitButton>

<BitModal @bind-IsOpen="isOpenBasic">
    <div style="padding:1rem; max-width:40rem">
        Lorem ipsum dolor sit amet, consectetur adipiscing elit. Maecenas lorem nulla, malesuada ut sagittis sit
        amet, vulputate in leo. Maecenas vulputate congue sapien eu tincidunt. Etiam eu sem turpis. Fusce tempor
        sagittis nunc, ut interdum ipsum vestibulum non. Proin dolor elit, aliquam eget tincidunt non, vestibulum ut
        turpis. In hac habitasse platea dictumst. In a odio eget enim porttitor maximus. Aliquam nulla nibh,
        ullamcorper aliquam placerat eu, viverra et dui. Phasellus ex lectus, maximus in mollis ac, luctus vel eros.
        Vivamus ultrices, turpis sed malesuada gravida, eros ipsum venenatis elit, et volutpat eros dui et ante.
        Quisque ultricies mi nec leo ultricies mollis. Vivamus egestas volutpat lacinia. Quisque pharetra eleifend
        efficitur.
    </div>
</BitModal>
```

```csharp
@code {
    private bool isOpenBasic;
}
```

### 2. Customizing Content (Header/Body)

Modals often require structured content, like a header with a title and close button, and a distinct body area. This is achieved using standard HTML elements and CSS within the `BitModal`'s `ChildContent`.

```cshtml
<style>
    .modal-header { /* Style for the header container */
        gap: 0.5rem;
        display: flex;
        font-size: 24px;
        font-weight: 600;
        align-items: center;
        padding: 12px 12px 14px 24px;
        border-top: 4px solid #0054C6; /* Example: adds a top border */
    }

    .modal-header-text { /* Style for the title text */
        flex-grow: 1; /* Allows text to take available space */
    }

    .modal-body { /* Style for the main content area */
        max-width: 960px;
        line-height: 20px;
        overflow-y: hidden; /* Or 'auto'/'scroll' if needed */
        padding: 0 24px 24px;
    }
</style>

<BitButton OnClick="() => isOpenCustomContent = true">Open Modal</BitButton>

<BitModal @bind-IsOpen="isOpenCustomContent">
    <div class="modal-header">
        <span class="modal-header-text">Lorem Ipsum</span>
        @* Close button inside the header *@
        <BitButton Variant="BitVariant.Text" OnClick="() => isOpenCustomContent = false" IconName="@BitIconName.ChromeClose" Title="Close" />
    </div>
    <div class="modal-body">
        <p>
            Lorem ipsum dolor sit amet... [content] ...efficitur.
        </p>
        <p>
            Mauris at nunc eget lectus lobortis... [more content] ...sed velit mi.
        </p>
        <p>
            Sed condimentum ultricies turpis... [more content] ...venenatis elementum.
        </p>
    </div>
</BitModal>
```

```csharp
@code {
    private bool isOpenCustomContent;
}
```

### 3. Advanced Options (`Blocking`, `AutoToggleScroll`, `Modeless`)

* **`Blocking`**: Prevents the modal from being closed by clicking the overlay (outside the modal content). Requires explicit close action (e.g., a button).
* **`AutoToggleScroll`**: Automatically hides the scrollbar of the main page (or a specified element via `ScrollerSelector`) when the modal is open, preventing background scrolling.
* **`Modeless`**: Removes the overlay entirely. The modal doesn't block interaction with the underlying page content.

```cshtml
@* (Includes CSS from previous example) *@

<BitButton OnClick="() => isOpenBlocking = true">Open Modal (Blocking)</BitButton>
<BitButton OnClick="() => isOpenAutoToggleScroll = true">Open Modal (AutoToggleScroll)</BitButton>
<BitButton OnClick="() => isOpenModeless = true">Open Modal (Modeless)</BitButton>

@* Blocking Modal *@
<BitModal @bind-IsOpen="isOpenBlocking" Blocking>
    <div class="modal-header">
        <span class="modal-header-text">Blocking</span>
        <BitButton Variant="BitVariant.Text" OnClick="() => isOpenBlocking = false" IconName="@BitIconName.ChromeClose" Title="Close" />
    </div>
    <div class="modal-body">
        <p>In Blocking mode, the modal won't close by clicking outside (on the overlay).</p>
        <br />
        <p>Lorem ipsum dolor sit amet...</p>
    </div>
</BitModal>

@* AutoToggleScroll Modal *@
<BitModal @bind-IsOpen="isOpenAutoToggleScroll" AutoToggleScroll>
    <div class="modal-header">
        <span class="modal-header-text">AutoToggleScroll</span>
        <BitButton Variant="BitVariant.Text" OnClick="() => isOpenAutoToggleScroll = false" IconName="@BitIconName.ChromeClose" Title="Close" />
    </div>
    <div class="modal-body">
        <p>In AutoToggleScroll mode, the scrollbar of the scroll element (body by default...) will be removed...</p>
        <br />
        <p>Lorem ipsum dolor sit amet...</p>
    </div>
</BitModal>

@* Modeless Modal *@
<BitModal @bind-IsOpen="isOpenModeless" Modeless>
    <div class="modal-header">
        <span class="modal-header-text">Modeless</span>
        <BitButton Variant="BitVariant.Text" OnClick="() => isOpenModeless = false" IconName="@BitIconName.ChromeClose" Title="Close" />
    </div>
    <div class="modal-body">
        <p>In Modeless mode, the overlay element won't render.</p>
        <br />
        <p>Lorem ipsum dolor sit amet...</p>
    </div>
</BitModal>
```

```csharp
@code {
    private bool isOpenBlocking;
    private bool isOpenAutoToggleScroll;
    private bool isOpenModeless;
}
```

### 4. Absolute Positioning (`AbsolutePosition`, `ScrollerSelector`)

* **`AbsolutePosition`**: Positions the modal using `position: absolute` relative to its nearest positioned ancestor, instead of the default `position: fixed` relative to the viewport. Useful for containing a modal within a specific section of the page. Often used with `Modeless`.
* **`ScrollerSelector`**: When `AutoToggleScroll` and `AbsolutePosition` are used, this specifies the CSS selector of the container whose scrollbar should be hidden (instead of the main `body`).

```cshtml
<style>
    .relative-container { /* Parent container for absolute positioning */
        width: 100%;
        height: 400px;
        overflow: auto; /* Example scrollable parent */
        margin-top: 1rem;
        position: relative; /* Required for AbsolutePosition */
        background-color: #eee;
        border: 2px lightgreen solid;
    }
    /* Include .modal-header, .modal-header-text, .modal-body styles */
</style>

<BitButton OnClick="() => isOpenAbsolutePosition = true">Open Modal (AbsolutePosition)</BitButton>
<BitButton OnClick="() => isOpenScrollerSelector = true">Open Modal (ScrollerSelector)</BitButton>

<div class="relative-container">
    @* Modal positioned absolutely within .relative-container, no overlay *@
    <BitModal @bind-IsOpen="isOpenAbsolutePosition" AbsolutePosition Modeless>
        <div class="modal-header">
            <span class="modal-header-text">AbsolutePosition & Modeless</span>
            <BitButton Variant="BitVariant.Text" OnClick="() => isOpenAbsolutePosition = false" IconName="@BitIconName.ChromeClose" Title="Close" />
        </div>
        <div class="modal-body"><p>Lorem ipsum dolor sit amet...</p></div>
    </BitModal>

    @* Modal positioned absolutely, hides scrollbar of .relative-container *@
    <BitModal @bind-IsOpen="isOpenScrollerSelector" AutoToggleScroll AbsolutePosition ScrollerSelector=".relative-container">
        <div class="modal-header">
            <span class="modal-header-text">ScrollerSelector</span>
            <BitButton Variant="BitVariant.Text" OnClick="() => isOpenScrollerSelector = false" IconName="@BitIconName.ChromeClose" Title="Close" />
        </div>
        <div class="modal-body"><p>Lorem ipsum dolor sit amet...</p></div>
    </BitModal>

    <div> [Long content inside relative-container to make it scrollable] </div>
</div>
```

```csharp
@code {
    private bool isOpenAbsolutePosition;
    private bool isOpenScrollerSelector;
}
```

### 5. Positioning (`Position`)

Controls the alignment of the modal within the viewport (or its absolute container if `AbsolutePosition` is true) using the `BitPosition` enum.

```cshtml
@* (Includes CSS from previous examples) *@

<BitButton OnClick="() => OpenModalInPosition(BitPosition.TopLeft)">Top Left</BitButton>
<BitButton OnClick="() => OpenModalInPosition(BitPosition.TopRight)">Top Right</BitButton>
@* ... (Buttons for other positions: TopCenter, CenterLeft, Center, CenterRight, BottomLeft, BottomCenter, BottomRight) ... *@
<BitButton OnClick="() => OpenModalInPosition(BitPosition.BottomLeft)">Bottom Left</BitButton>
<BitButton OnClick="() => OpenModalInPosition(BitPosition.BottomRight)">Bottom Right</BitButton>

<BitModal @bind-IsOpen="isOpenPosition" Position="position">
    <div class="modal-header">
        <span class="modal-header-text">Modal positioning</span>
        <BitButton Variant="BitVariant.Text" OnClick="() => isOpenPosition = false" IconName="@BitIconName.ChromeClose" Title="Close" />
    </div>
    <div class="modal-body">
        BitModal with custom positioning. Lorem ipsum dolor sit amet...
    </div>
</BitModal>
```

```csharp
@code {
    private bool isOpenPosition;
    private BitPosition position = BitPosition.Center; // Default or set by button click

    private void OpenModalInPosition(BitPosition positionValue)
    {
        isOpenPosition = true;
        position = positionValue;
    }
}
```

* **Note:** `BitPosition` includes values like `Center`, `TopLeft`, `TopCenter`, `TopRight`, `CenterLeft`, `CenterRight`, `BottomLeft`, `BottomCenter`, `BottomRight`.

### 6. Draggable (`Draggable`, `DragElementSelector`)

* **`Draggable`**: Allows the user to click and drag the modal to reposition it.
* **`DragElementSelector`**: Specifies a CSS selector within the modal's content that acts as the drag handle. If omitted, the entire modal content area is draggable.

```cshtml
@* (Includes CSS from previous examples) *@
<style>
    .modal-header-drag { /* Example class for the drag handle */
        cursor: move;
    }
</style>

<BitButton OnClick="() => isOpenDraggable = true">Open Draggable Modal</BitButton>
<BitModal @bind-IsOpen="isOpenDraggable" Draggable>
    <div class="modal-header"> @* Draggable by header or body *@
        <span class="modal-header-text">Draggable Modal</span>
        <BitButton Variant="BitVariant.Text" OnClick="() => isOpenDraggable = false" IconName="@BitIconName.ChromeClose" Title="Close" />
    </div>
    <div class="modal-body"><p>Lorem ipsum dolor sit amet...</p></div>
</BitModal>

<BitButton OnClick="() => isOpenDraggableSelector = true">Open Modal (Custom Drag Handle)</BitButton>
<BitModal @bind-IsOpen="isOpenDraggableSelector" Draggable DragElementSelector=".modal-header-drag">
    <div class="modal-header modal-header-drag"> @* Only this header is draggable *@
        <span class="modal-header-text">Draggable Modal (Custom Handle)</span>
        <BitButton Variant="BitVariant.Text" OnClick="() => isOpenDraggableSelector = false" IconName="@BitIconName.ChromeClose" Title="Close" />
    </div>
    <div class="modal-body"><p>Lorem ipsum dolor sit amet...</p></div>
</BitModal>
```

```csharp
@code {
    private bool isOpenDraggable;
    private bool isOpenDraggableSelector;
}
```

### 7. Full Size (`FullSize`)

Makes the modal occupy the entire viewport. Can be toggled dynamically.

```cshtml
@* (Includes CSS from previous examples) *@

<BitButton OnClick="() => isOpenFullSize = true">Open Full Size Modal</BitButton>

<BitModal @bind-IsOpen="isOpenFullSize" FullSize="isFullSize"> @* Bind FullSize to a variable *@
    <div class="modal-header">
        <span class="modal-header-text">Full size modal</span>
        @* Button to toggle full size state *@
        <BitButton Variant="BitVariant.Text"
                   OnClick="() => isFullSize = !isFullSize"
                   IconName="@(isFullSize ? BitIconName.BackToWindow : BitIconName.ChromeFullScreen)"
                   Title="@(isFullSize ? "Exit FullScreen" : "FullScreen")" />
        <BitButton Variant="BitVariant.Text"
                   OnClick="() => isOpenFullSize = false"
                   IconName="@BitIconName.ChromeClose"
                   Title="Close" />
    </div>
    <div class="modal-body"><p>Lorem ipsum dolor sit amet...</p></div>
</BitModal>
```

```csharp
@code {
    private bool isOpenFullSize;
    private bool isFullSize = true; // Initial state when opening
}
```

### 8. Events (`OnDismiss`, `OnOverlayClick`)

* **`OnDismiss`**: Callback triggered when the modal is about to be dismissed (e.g., by clicking the overlay if not `Blocking`, or pressing ESC). Can be used for cleanup or confirmation logic.
* **`OnOverlayClick`**: Callback triggered specifically when the overlay area (outside the modal content) is clicked.

```cshtml
@* (Includes CSS from previous examples) *@

<BitButton OnClick="() => isEventsOpen = true">Open Events Modal</BitButton>

<div>Dismissed? [@isDismissed]</div>
<div>Overlay clicked? [@isOverlayClicked]</div>

<BitModal @bind-IsOpen="isEventsOpen"
          Draggable
          OnDismiss="HandleOnDismiss"
          OnOverlayClick="HandleOnOverlayClick">
    <div class="modal-header">
        <span class="modal-header-text">Events modal</span>
        <BitButton Title="Close"
                   Variant="BitVariant.Text"
                   OnClick="() => isEventsOpen = false"
                   IconName="@BitIconName.ChromeClose" />
    </div>
    <div class="modal-body"><p>Lorem ipsum dolor sit amet...</p></div>
</BitModal>
```

```csharp
@code {
    private bool isEventsOpen;
    private bool isDismissed;
    private bool isOverlayClicked;

    // Example: Indicate dismissal for 3 seconds
    private async Task HandleOnDismiss()
    {
        isDismissed = true;
        InvokeAsync(StateHasChanged); // Update UI
        await Task.Delay(3000);
        isDismissed = false;
        InvokeAsync(StateHasChanged); // Update UI
    }

    // Example: Indicate overlay click for 2 seconds
    private void HandleOnOverlayClick()
    {
        isOverlayClicked = true;
        InvokeAsync(StateHasChanged);
        _ = Task.Delay(2000).ContinueWith(t =>
        {
            isOverlayClicked = false;
            InvokeAsync(StateHasChanged);
        });
    }
}
```

### 9. Styling (`Style`, `Class`, `Styles`, `Classes`)

Provides granular control over the modal's appearance.

* **`Style`**: Applies inline styles directly to the modal's root wrapper element.
* **`Class`**: Adds CSS classes to the modal's root wrapper element.
* **`Styles`**: An object (`BitModalClassStyles`) allowing inline styles for specific parts: `Root`, `Overlay`, `Content`.
* **`Classes`**: An object (`BitModalClassStyles`) allowing CSS classes for specific parts: `Root`, `Overlay`, `Content`.

```cshtml
<style>
    /* ... (modal-header, modal-body styles) ... */

    /* For 'Class' parameter */
    .custom-class {
        border: 0.5rem solid tomato;
        background-color: darkgoldenrod; /* Applies to the root wrapper */
    }

    /* For 'Classes' parameter */
    .custom-root { /* Applied via Classes.Root */
        border: 0.25rem solid #0054C6;
    }
    .custom-overlay { /* Applied via Classes.Overlay */
        background-color: #ffbd5a66;
    }
    .custom-content { /* Applied via Classes.Content */
        margin: 1rem;
        box-shadow: 0 0 10rem purple;
        border-end-end-radius: 1rem;
        border-end-start-radius: 1rem;
    }
</style>

<BitButton OnClick="() => isOpenStyle = true">Open styled modal</BitButton>
<BitButton OnClick="() => isOpenClass = true">Open classed modal</BitButton>
<BitButton OnClick="() => isOpenStyles = true">Open modal styles</BitButton>
<BitButton OnClick="() => isOpenClasses = true">Open modal classes</BitButton>

@* Using Style *@
<BitModal @bind-IsOpen="isOpenStyle" Style="box-shadow: inset 0px 0px 1.5rem 1.5rem palevioletred;">
    @* ... modal header and body ... *@
</BitModal>

@* Using Class *@
<BitModal @bind-IsOpen="isOpenClass" Class="custom-class">
    @* ... modal header and body ... *@
</BitModal>

@* Using Styles *@
<BitModal @bind-IsOpen="isOpenStyles" Styles="@(new() { Overlay = "background-color: #4776f433;", Content = "box-shadow: 0 0 1rem tomato;" })">
    @* ... modal header and body ... *@
</BitModal>

@* Using Classes *@
<BitModal @bind-IsOpen="isOpenClasses" Classes="@(new() { Root = "custom-root", Overlay = "custom-overlay", Content = "custom-content" })">
    @* ... modal header and body ... *@
</BitModal>
```

```csharp
@code {
    private bool isOpenStyle;
    private bool isOpenClass;
    private bool isOpenStyles;
    private bool isOpenClasses;
}
```

### 10. Right-to-Left (`Dir`)

Sets the text direction for the modal content and affects layout details like close button positioning if relevant styles are direction-aware.

```cshtml
@* (Includes CSS from previous examples) *@

<BitButton Dir="BitDir.Rtl" OnClick="() => isOpenRtl = true">باز کردن مُدال</BitButton>

<BitModal Dir="BitDir.Rtl" @bind-IsOpen="isOpenRtl">
    <div class="modal-header">
        <span class="modal-header-text">لورم ایپسوم</span>
        <BitButton Variant="BitVariant.Text" OnClick="() => isOpenRtl = false" IconName="@BitIconName.ChromeClose" Title="Close" />
    </div>
    <div class="modal-body">
        <p>لورم ایپسوم متن ساختگی...</p>
        <p>لورم ایپسوم متن ساختگی...</p>
        <p>لورم ایپسوم متن ساختگی...</p>
    </div>
</BitModal>
```

```csharp
@code {
    private bool isOpenRtl;
}
```

---

## API Reference

### `BitModal` Parameters

| Name                  | Type                          | Default Value | Description                                                                                                                                      |
| :-------------------- | :---------------------------- | :------------ | :----------------------------------------------------------------------------------------------------------------------------------------------- |
| `IsOpen`              | `bool`                        | `false`       | Controls whether the Modal is displayed. Use `@bind-IsOpen` for two-way binding.                                                                 |
| `ChildContent`        | `RenderFragment?`             | `null`        | The content to be rendered inside the modal.                                                                                                     |
| `AbsolutePosition`    | `bool`                        | `false`       | If true, positions the modal absolutely relative to its nearest positioned ancestor. Otherwise, uses fixed positioning relative to the viewport. |
| `AutoToggleScroll`    | `bool`                        | `false`       | If true, automatically hides the scrollbar of the element specified by `ScrollerSelector` (default: `body`) when the modal opens.                 |
| `Blocking`            | `bool`                        | `false`       | If true, prevents closing the modal by clicking the overlay. Requires an explicit close action (e.g., button).                                   |
| `Classes`             | `BitModalClassStyles?`        | `null`        | Custom CSS classes for specific parts (`Root`, `Overlay`, `Content`) of the modal. See `BitModalClassStyles` section below.                        |
| `DragElementSelector` | `string?`                     | `null`        | CSS selector for the element within the modal that acts as the drag handle. If null, the entire modal content area is the handle (if `Draggable`). |
| `Draggable`           | `bool`                        | `false`       | Allows the modal to be dragged by the user.                                                                                                      |
| `FullHeight`          | `bool`                        | `false`       | Makes the Modal height 100% of its parent container (useful with `AbsolutePosition`).                                                            |
| `FullSize`            | `bool`                        | `false`       | Makes the Modal width **and** height 100% (usually of the viewport, unless `AbsolutePosition` is true).                                          |
| `FullWidth`           | `bool`                        | `false`       | Makes the Modal width 100% (usually of the viewport, unless `AbsolutePosition` is true).                                                         |
| `IsAlert`             | `bool?`                       | `null`        | Explicitly sets the ARIA role (`alertdialog` if true, `dialog` if false). Overrides default role based on `Blocking`/`Modeless`.                 |
| `Modeless`            | `bool`                        | `false`       | If true, removes the overlay and doesn't block interaction with the page behind it. `Blocking` is ignored if this is true.                       |
| `OnDismiss`           | `EventCallback<MouseEventArgs>` |               | Callback invoked when the modal is about to be dismissed (e.g., overlay click if not `Blocking`, ESC key).                                         |
| `OnOverlayClick`      | `EventCallback<MouseEventArgs>` |               | Callback invoked specifically when the overlay area is clicked.                                                                                  |
| `Position`            | `BitPosition?`                | `null`        | Sets the alignment of the modal (`Center`, `TopLeft`, `TopRight`, etc.). See `BitPosition` enum below.                                           |
| `ScrollerSelector`    | `string`                      | `"body"`      | CSS selector for the element whose scrollbar is hidden when `AutoToggleScroll` is true.                                                          |
| `Styles`              | `BitModalClassStyles?`        | `null`        | Custom inline CSS styles for specific parts (`Root`, `Overlay`, `Content`) of the modal. See `BitModalClassStyles` section below.                  |
| `SubtitleAriaId`      | `string?`                     | `null`        | Sets the `aria-describedby` attribute, pointing to the ID of the element containing the modal's subtitle/description.                              |
| `TitleAriaId`         | `string?`                     | `null`        | Sets the `aria-labelledby` attribute, pointing to the ID of the element containing the modal's title.                                            |

### Inherited Parameters (`BitComponentBase`)

These parameters are inherited from the base component class and are available on `BitModal`.

| Name             | Type                          | Default Value              | Description                                                                                    |
| :--------------- | :---------------------------- | :------------------------- | :--------------------------------------------------------------------------------------------- |
| `AriaLabel`      | `string?`                     | `null`                     | The `aria-label` attribute for accessibility, used if `TitleAriaId` is not provided.            |
| `Class`          | `string?`                     | `null`                     | Custom CSS class(es) applied to the root wrapper element of the modal.                         |
| `Dir`            | `BitDir?`                     | `null`                     | Sets the text direction (`Ltr`, `Rtl`, `Auto`). See `BitDir` enum below.                       |
| `HtmlAttributes` | `Dictionary<string, object>`  | `new Dictionary<>()`       | Allows capturing and rendering additional HTML attributes on the root element.                 |
| `Id`             | `string?`                     | `null`                     | Custom `id` attribute for the root element. If `null`, a unique ID (`UniqueId`) is generated. |
| `IsEnabled`      | `bool`                        | `true`                     | Typically used for styling disabled state; modals are generally interactive when open.         |
| `Style`          | `string?`                     | `null`                     | Custom inline CSS style(s) applied to the root wrapper element of the modal.                   |
| `Visibility`     | `BitVisibility`               | `BitVisibility.Visible`    | Controls the component's visibility (`Visible`, `Hidden`, `Collapsed`). Modals usually use `IsOpen`. |

### Public Members (`BitComponentBase`)

These are public properties available on the component instance.

| Name          | Type               | Default Value    | Description                                                                           |
| :------------ | :----------------- | :--------------- | :------------------------------------------------------------------------------------ |
| `UniqueId`    | `string`           | `Guid.NewGuid()` | Readonly unique identifier generated for the component instance. Used if `Id` is null. |
| `RootElement` | `ElementReference` |                  | A reference to the root HTML element of the component (available after rendering).      |

### Supporting Classes and Enums

#### `BitModalClassStyles` Class

Used for the `Classes` and `Styles` parameters to target specific parts of the modal.

| Property | Type      | Description                                                   |
| :------- | :-------- | :------------------------------------------------------------ |
| `Root`   | `string?` | CSS class(es) or style(s) for the main root wrapper element.  |
| `Overlay`| `string?` | CSS class(es) or style(s) for the background overlay element. |
| `Content`| `string?` | CSS class(es) or style(s) for the modal's content container.  |

#### `BitPosition` Enum

Used for the `Position` parameter.

| Name           | Value | Description                     |
| :------------- | :---- | :------------------------------ |
| `Center`       | `0`   | Center of the container/viewport. |
| `TopLeft`      | `1`   | Top-left corner.                |
| `TopCenter`    | `2`   | Top-center alignment.           |
| `TopRight`     | `3`   | Top-right corner.               |
| `CenterLeft`   | `4`   | Center-left alignment.          |
| `CenterRight`  | `5`   | Center-right alignment.         |
| `BottomLeft`   | `6`   | Bottom-left corner.             |
| `BottomCenter` | `7`   | Bottom-center alignment.        |
| `BottomRight`  | `8`   | Bottom-right corner.            |

#### `BitVisibility` Enum

Used for the inherited `Visibility` parameter.

| Name        | Value | Description                                                        |
| :---------- | :---- | :----------------------------------------------------------------- |
| `Visible`   | `0`   | Component is visible (default).                                    |
| `Hidden`    | `1`   | Component is hidden (`visibility: hidden;`), still occupies space. |
| `Collapsed` | `2`   | Component is hidden (`display: none;`), does not occupy space.     |

#### `BitDir` Enum

Used for the inherited `Dir` parameter.

| Name   | Value | Description                                     |
| :----- | :---- | :---------------------------------------------- |
| `Ltr`  | `0`   | Left-to-right text direction.                   |
| `Rtl`  | `1`   | Right-to-left text direction.                   |
| `Auto` | `2`   | Browser determines direction based on content. |

---

**End of Reference**

**Explanation of the Markdown File:**

1.  **Standard Header:** Includes the component name (`BitModal`) and clearly states the document's purpose for an AI agent.
2.  **Overview:** Provides a concise summary of what `BitModal` is and its intended use case, based on the description in the HTML.
3.  **Usage Examples:**
    *   Each key feature demonstrated in the HTML (`Basic`, `Customizing`, `Blocking`, `AbsolutePosition`, `Position`, `Draggable`, `FullSize`, `Events`, `Styling`, `RTL`) is presented as a separate subsection with a descriptive heading (`###`).
    *   A brief explanation introduces the concept shown in the example.
    *   Relevant C# (`@code`) and CSHTML (`.cshtml`) code snippets are included in fenced code blocks with language identifiers (```csharp`, ```cshtml`).
    *   Custom CSS needed for specific examples (like header/body styling or the drag handle) is included within `<style>` tags inside the `cshtml` block or in a separate ```css` block if preferred.
    *   Key parameters being demonstrated (`@bind-IsOpen`, `Blocking`, `Draggable`, `Position`, `Styles`, `Classes`, `Dir`, etc.) are visible in the code.
    *   Notes are added where necessary (e.g., explaining `BitPosition` values).
4.  **API Reference:**
    *   Clearly separated sections for `BitModal` specific parameters, inherited `BitComponentBase` parameters, and public members.
    *   Uses Markdown tables for easy parsing, detailing `Name`, `Type`, `Default Value`, and `Description` for each parameter/member.
    *   Data types (`bool`, `string?`, `RenderFragment?`, `EventCallback<>`, custom classes/enums like `BitModalClassStyles?`, `BitPosition?`) are listed accurately.
    *   Default values are provided as specified in the HTML.
    *   Descriptions concisely explain the purpose of each item.
5.  **Supporting Classes and Enums:**
    *   Dedicated subsections explain complex types used in parameters, like `BitModalClassStyles`, and list the possible values for enums (`BitPosition`, `BitVisibility`, `BitDir`) using tables.
6.  **Formatting:** Uses standard Markdown for structure (headings, lists, code blocks, tables) and emphasis (backticks for code elements), making it highly readable for both humans and machines.

This format provides the AI agent with structured information, code examples illustrating various features, and a detailed API breakdown, enabling it to effectively assist developers using the `BitModal` component.
