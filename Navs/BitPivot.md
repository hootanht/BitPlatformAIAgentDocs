# BitPivot Component Documentation

The **BitPivot** control (and its visual variant, Tab) is designed for navigating between frequently accessed and distinct content categories. It uses text headers (optionally enhanced with icons or counts) to clearly articulate different content sections. When a user taps or clicks on a pivot header, the corresponding content panel is displayed. This component is ideal for applications that need to organize content into multiple views or sections.

---

## Overview

The BitPivot control and related tabs are used for:
- **Navigating Content Views:** Quickly switching between two or more content sections.
- **Visual Distinction:** Using text, icons, or a combination of both to describe sections.
- **Flexible Presentation:** Offering several visual variants and size options for optimal design integration.
- **Responsive Layouts:** Supporting both left-to-right and right-to-left (RTL) languages.

Tabs represent a visual variant of Pivot where a mix of icons and text (or just icons) can be used to articulate the header labels.

---

## Usage

### 1. Basic Pivot

A basic example with three pivot items. Tapping the header navigates to the associated content view.

```razor
<div role="toolbar" class="bit-pvt bit-pvt-md bit-pvt-lnk bit-pvt-non bit-pvt-top">
  <div class="bit-pvt-hct" role="tablist">
    <button role="tab" type="button" name="File" data-content="File" class="bit-pvti bit-pvti-sel" tabindex="0" aria-selected="true">
      <span><span>File</span></span>
    </button>
    <button role="tab" type="button" name="Shared with me" data-content="Shared with me" class="bit-pvti" tabindex="-1" aria-selected="false">
      <span><span>Shared with me</span></span>
    </button>
    <button role="tab" type="button" name="Recent" data-content="Recent" class="bit-pvti" tabindex="-1" aria-selected="false">
      <span><span>Recent</span></span>
    </button>
  </div>
  <div role="tabpanel" class="bit-pvt-cct" aria-labelledby="w309ko">
    <h3>Pivot #1</h3>
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Cras eu ligula quis orci accumsan pharetra.</p>
  </div>
</div>
```

### 2. Icon and Count

This example demonstrates how to include icons and counts within the pivot header. It helps to visually emphasize the content category.

```razor
<div role="toolbar" class="bit-pvt bit-pvt-md bit-pvt-lnk bit-pvt-non bit-pvt-top">
  <div class="bit-pvt-hct" role="tablist">
    <button role="tab" type="button" name="Files" data-content="Files" class="bit-pvti bit-pvti-sel" tabindex="0" aria-selected="true">
      <span>
        <span><i class="bit-icon bit-icon--Info"></i></span>
        <span>Files</span>
      </span>
    </button>
    <button role="tab" type="button" name="Shared with me" data-content="Shared with me" class="bit-pvti" tabindex="-1" aria-selected="false">
      <span>
        <span>Shared with me</span>
        <span>(32)</span>
      </span>
    </button>
    <button role="tab" type="button" name="Recent" data-content="Recent" class="bit-pvti" tabindex="-1" aria-selected="false">
      <span>
        <span><i class="bit-icon bit-icon--Info"></i></span>
        <span>Recent</span>
        <span>(12)</span>
      </span>
    </button>
  </div>
  <div role="tabpanel" class="bit-pvt-cct" aria-labelledby="fu4vs5">
    <h1>Pivot #1: Files</h1>
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Cras eu ligula quis orci accumsan pharetra.</p>
  </div>
</div>
```

### 3. Size Variants

Pivot headers can be rendered in various sizes to suit different UI designs:

```razor
<!-- Large Pivot -->
<div role="toolbar" class="bit-pvt bit-pvt-lg bit-pvt-lnk bit-pvt-non bit-pvt-top">
  <div class="bit-pvt-hct" role="tablist">
    <button role="tab" type="button" name="Large File" data-content="Large File" class="bit-pvti bit-pvti-sel" tabindex="0" aria-selected="true">
      <span><span>Large File</span></span>
    </button>
    <!-- Additional items... -->
  </div>
  <div role="tabpanel" class="bit-pvt-cct">
    <h1>Pivot #1: Large File</h1>
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
  </div>
</div>
```

### 4. Header Type

Customize the header rendering style. For example, you can render the header as a link:

```razor
<div role="toolbar" class="bit-pvt bit-pvt-md bit-pvt-tab bit-pvt-non bit-pvt-top">
  <div class="bit-pvt-hct" role="tablist">
    <button role="tab" type="button" name="File tab" data-content="File tab" class="bit-pvti bit-pvti-sel" tabindex="0" aria-selected="true">
      <span><span>File tab</span></span>
    </button>
    <!-- Additional headers -->
  </div>
  <div role="tabpanel" class="bit-pvt-cct">
    <h1>Pivot #1: File tab</h1>
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
  </div>
</div>
```

### 5. Data Binding

Pivot supports event callbacks and binding for handling header clicks and selection changes.

**Example with Events:**

```razor
<BitPivot DefaultSelectedKey="file" OnChange="HandlePivotChange" OnItemClick="HandlePivotClick">
  <BitPivotItem Key="file" HeaderText="File">
    <p>Content for File</p>
  </BitPivotItem>
  <BitPivotItem Key="shared" HeaderText="Shared with me">
    <p>Content for Shared with me</p>
  </BitPivotItem>
  <BitPivotItem Key="recent" HeaderText="Recent">
    <p>Content for Recent</p>
  </BitPivotItem>
</BitPivot>

@code {
    private void HandlePivotChange(BitPivotItem item)
    {
        // Handle pivot item change.
    }
    
    private void HandlePivotClick(BitPivotItem item)
    {
        // Handle pivot item click.
    }
}
```

### 6. Detached Pivot

A detached mode allows the pivot header and its content to be rendered separately. This can be useful if you want more control over layout or animations.

```razor
<div style="border:1px solid gray; padding:10px;">
  <p>Hello, I am detached content for the pivot.</p>
</div>
<hr />
<div role="toolbar" class="bit-pvt bit-pvt-md bit-pvt-lnk bit-pvt-non bit-pvt-top">
  <div class="bit-pvt-hct" role="tablist">
    <button role="tab" type="button" name="Foo" data-content="Foo" class="bit-pvti bit-pvti-sel" tabindex="0" aria-selected="true">
      <span><span>Foo</span></span>
    </button>
    <button role="tab" type="button" name="Bar" data-content="Bar" class="bit-pvti" tabindex="-1" aria-selected="false">
      <span><span>Bar</span></span>
    </button>
    <button role="tab" type="button" name="Bas" data-content="Bas" class="bit-pvti" tabindex="-1" aria-selected="false">
      <span><span>Bas</span></span>
    </button>
    <button role="tab" type="button" name="Biz" data-content="Biz" class="bit-pvti" tabindex="-1" aria-selected="false">
      <span><span>Biz</span></span>
    </button>
  </div>
</div>
```

### 7. Right-to-Left (RTL) Support

Pivot can be rendered in RTL mode for languages such as Arabic:

```razor
<div dir="rtl">
  <div role="toolbar" class="bit-pvt bit-rtl bit-pvt-md bit-pvt-lnk bit-pvt-scr bit-pvt-top" dir="rtl">
    <div class="bit-pvt-hct" role="tablist">
      <button role="tab" type="button" name="اسناد" data-content="اسناد" class="bit-pvti bit-pvti-sel" tabindex="0" aria-selected="true">
        <span><span><i class="bit-icon bit-icon--Info"></i></span><span>اسناد</span></span>
      </button>
      <button role="tab" type="button" name="آخرین ها" data-content="آخرین ها" class="bit-pvti" tabindex="-1" aria-selected="false">
        <span><span>آخرین ها</span><span>(8)</span></span>
      </button>
      <button role="tab" type="button" name="شخصی" data-content="شخصی" class="bit-pvti" tabindex="-1" aria-selected="false">
        <span><span><i class="bit-icon bit-icon--Info"></i></span><span>شخصی</span><span>(6)</span></span>
      </button>
    </div>
    <div role="tabpanel" class="bit-pvt-cct">
      <p>لورم ایپسوم متن ساختگی با تولید سادگی نامفهوم از صنعت چاپ است.</p>
    </div>
  </div>
</div>
```

---

## API Reference

### BitPivot Parameters

| Name               | Type                              | Default Value                        | Description                                                                                   |
|--------------------|-----------------------------------|--------------------------------------|-----------------------------------------------------------------------------------------------|
| **Alignment**      | `BitAlignment?`                   | `null`                               | Determines the alignment of the header section.                                             |
| **ChildContent**   | `RenderFragment?`                 | `null`                               | The content of the pivot.                                                                     |
| **Classes**        | `BitPivotClassStyles?`            | `null`                               | Custom CSS classes for different parts of the pivot.                                          |
| **DefaultSelectedKey** | `string?`                   | `null`                               | The default selected key for the pivot.                                                       |
| **HeaderOnly**     | `bool`                            | `false`                              | If true, only the header is rendered (skips the tab panel content).                           |
| **HeaderType**     | `BitPivotHeaderType`              | `BitPivotHeaderType.Link`            | The type used to render the header items (Link or Tab).                                       |
| **OnItemClick**    | `EventCallback<BitPivotItem>`     | —                                    | Callback when a pivot item header is clicked.                                                 |
| **OnChange**       | `EventCallback<BitPivotItem>`     | —                                    | Callback when the selected pivot item changes.                                                |
| **OverflowBehavior** | `BitOverflowBehavior`           | `BitOverflowBehavior.None`           | Defines what happens when there is not enough room for all pivot headers.                      |
| **Position**       | `BitPivotPosition`                | `BitPivotPosition.Top`               | The position of the pivot header relative to its content (Top, Bottom, Left, Right).            |
| **SelectedKey**    | `string?`                        | `null`                               | The key of the currently selected pivot item.                                                 |
| **Size**           | `BitSize?`                        | `null`                               | The size of the pivot header items (Small, Medium, Large).                                    |
| **Styles**         | `BitPivotClassStyles?`            | `null`                               | Custom CSS styles for different parts of the pivot.                                           |

### Inherited BitComponentBase Parameters

| Name             | Type                         | Default Value                      | Description                                                                 |
|------------------|------------------------------|------------------------------------|-----------------------------------------------------------------------------|
| **AriaLabel**    | `string?`                    | `null`                             | ARIA label for accessibility.                                             |
| **Class**        | `string?`                    | `null`                             | Custom CSS class for the root element.                                    |
| **Dir**          | `BitDir?`                    | `null`                             | Text direction (LTR, RTL, or Auto).                                         |
| **HtmlAttributes** | `Dictionary<string, object>` | `new Dictionary<string, object>()` | Additional attributes for the root element.                               |
| **Id**           | `string?`                    | `null`                             | Custom id for the root element; if null, a unique id is generated.          |
| **IsEnabled**    | `bool`                     | `true`                             | Determines whether the component is enabled.                              |
| **Style**        | `string?`                    | `null`                             | Inline CSS styles for the root element.                                   |
| **Visibility**   | `BitVisibility`              | `BitVisibility.Visible`            | Sets the visibility of the component.                                     |

### Public Members

- **UniqueId:** A read-only unique identifier generated during component construction.
- **RootElement:** An `ElementReference` to the component's root DOM element.

### BitPivotClassStyles Properties

| Name             | Type      | Default Value | Description                                                                   |
|------------------|-----------|---------------|-------------------------------------------------------------------------------|
| **Root**         | `string?` | `null`        | Custom CSS classes for the root element of the pivot.                         |
| **Header**       | `string?` | `null`        | Custom CSS classes for the pivot header container.                            |
| **Body**         | `string?` | `null`        | Custom CSS classes for the content panel of the pivot.                        |
| **HeaderItem**   | `string?` | `null`        | Custom CSS classes for each pivot header item.                                |
| **SelectedItem** | `string?` | `null`        | Custom CSS classes for the currently selected header item.                    |
| **HeaderItemContent** | `string?` | `null`    | Custom CSS classes for the content within a header item.                      |

---

## Enumerations

### BitAlignment Enum

| Name      | Value | Description                                |
|-----------|-------|--------------------------------------------|
| **Start**       | 0     | Align headers at the start.             |
| **End**         | 1     | Align headers at the end.               |
| **Center**      | 2     | Center the headers.                     |
| **SpaceBetween**| 3     | Distribute headers with space between.  |
| **SpaceAround** | 4     | Distribute headers with space around.   |
| **SpaceEvenly** | 5     | Distribute headers evenly.              |
| **Baseline**    | 6     | Align headers along the baseline.       |
| **Stretch**     | 7     | Stretch headers to fill the container.  |

### BitPivotHeaderType Enum

| Name | Value | Description                               |
|------|-------|-------------------------------------------|
| **Tab**  | 0     | Renders pivot header items as tabs.   |
| **Link** | 1     | Renders pivot header items as links.  |

### BitSize Enum

| Name    | Value | Description        |
|---------|-------|--------------------|
| **Small**   | 0     | The small size.   |
| **Medium**  | 1     | The medium size.  |
| **Large**   | 2     | The large size.   |

### BitOverflowBehavior Enum

| Name   | Value | Description                                                             |
|--------|-------|-------------------------------------------------------------------------|
| **None** | 0   | Pivot headers will overflow the container.                            |
| **Menu** | 1   | Displays an overflow menu for headers that do not fit.                  |
| **Scroll** | 2 | Displays a scroll bar to navigate through the headers.                  |

### BitPivotPosition Enum

| Name  | Value | Description                                       |
|-------|-------|---------------------------------------------------|
| **Top**    | 0     | Display the header above the content.         |
| **Bottom** | 1     | Display the header below the content.         |
| **Left**   | 2     | Display the header to the left of the content.  |
| **Right**  | 3     | Display the header to the right of the content. |

### BitVisibility Enum

| Name       | Value | Description                                                       |
|------------|-------|-------------------------------------------------------------------|
| **Visible**    | 0     | The component is visible.                                      |
| **Hidden**     | 1     | The component is hidden (space is reserved; CSS `visibility: hidden`). |
| **Collapsed**  | 2     | The component is not rendered (CSS `display: none`).           |

### BitDir Enum

| Name  | Value | Description                                                                 |
|-------|-------|-----------------------------------------------------------------------------|
| **Ltr**  | 0     | Left-to-right text direction (e.g., English).                             |
| **Rtl**  | 1     | Right-to-left text direction (e.g., Arabic).                              |
| **Auto** | 2     | Automatically determines direction based on content.                      |

---