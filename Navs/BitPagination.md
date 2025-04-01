# BitPagination Component Documentation

The **BitPagination** component provides users with an easy way to navigate through content. It is ideal for lists, tables, or any content-rich interface where content is spread across multiple pages. The component supports various visual variants, sizes, colors, and binding scenarios, ensuring it fits a wide range of design requirements.

---

## Overview

The Pagination component helps users swiftly browse across multiple pages by rendering navigation buttons. It supports:
- **Basic navigation:** Render previous/next buttons and page numbers.
- **Variants:** Choose between Fill (default), Outline, or Text styles.
- **Default Selection:** Preselect a page on load.
- **Boundary & Middle Counts:** Limit the number of pages shown at the beginning/end or in the middle of the range.
- **Custom Navigation Buttons:** Optionally show first/last buttons.
- **Custom Icons:** Replace default icons with custom ones.
- **Color and Size Variants:** Match your design system.
- **Data Binding:** Support for one-way and two-way binding.
- **RTL Support:** Render in right-to-left mode for languages such as Arabic.

---

## Usage

### 1. Basic Example

A simple Pagination component with five pages:

```razor
<div class="bit-pgn bit-pgn-pri bit-pgn-md">
    <button aria-label="Previous page" disabled class="bit-pgn-btn bit-pgn-fil">
        <i class="bit-icon bit-icon--ChevronRight bit-pgn-trs"></i>
    </button>
    <button aria-current="page" aria-label="Current page 1" class="bit-pgn-btn bit-pgn-sel bit-pgn-fil">1</button>
    <button aria-label="Page 2" class="bit-pgn-btn bit-pgn-fil">2</button>
    <button aria-label="Page 3" class="bit-pgn-btn bit-pgn-fil">3</button>
    <button aria-label="Page 4" class="bit-pgn-btn bit-pgn-fil">4</button>
    <button aria-label="Page 5" class="bit-pgn-btn bit-pgn-fil">5</button>
    <button aria-label="Next page" class="bit-pgn-btn bit-pgn-fil">
        <i class="bit-icon bit-icon--ChevronRight bit-pgn-tre"></i>
    </button>
</div>
```

### 2. Visual Variants

The component supports three variants:

- **Fill (Default):**  
  Uses the `bit-pgn-fil` class.
  
- **Outline:**  
  Uses the `bit-pgn-otl` class.  
  Example:

  ```razor
  <div class="bit-pgn bit-pgn-pri bit-pgn-md">
      <button aria-label="Previous page" disabled class="bit-pgn-btn bit-pgn-otl">
          <i class="bit-icon bit-icon--ChevronRight bit-pgn-trs"></i>
      </button>
      <button aria-current="page" aria-label="Current page 1" class="bit-pgn-btn bit-pgn-sel bit-pgn-otl">1</button>
      <!-- Additional page buttons -->
  </div>
  ```

- **Text:**  
  Uses the `bit-pgn-txt` class.  
  Example:

  ```razor
  <div class="bit-pgn bit-pgn-pri bit-pgn-md">
      <button aria-label="Previous page" disabled class="bit-pgn-btn bit-pgn-txt">
          <i class="bit-icon bit-icon--ChevronRight bit-pgn-trs"></i>
      </button>
      <button aria-current="page" aria-label="Current page 1" class="bit-pgn-btn bit-pgn-sel bit-pgn-txt">1</button>
      <!-- Additional page buttons -->
  </div>
  ```

### 3. Default Selected Page

Set a default selected page using the `DefaultSelectedPage` parameter:
  
```razor
<BitPagination DefaultSelectedPage="3" Count="5" />
```

### 4. Boundary & Middle Count

- **BoundaryCount:** Limits the number of pages shown at the start and end of the range.
  
  ```razor
  <BitPagination BoundaryCount="2" Count="11" DefaultSelectedPage="6" />
  ```
  
- **MiddleCount:** Defines the number of pages displayed in the middle of the control.
  
  ```razor
  <BitPagination MiddleCount="3" Count="11" DefaultSelectedPage="6" />
  ```

### 5. Navigation Buttons

Display additional navigation buttons (first and last) with parameters:

```razor
<BitPagination Count="24" ShowFirstButton="true" ShowLastButton="true" />
```

### 6. Custom Icons

Customize navigation button icons via parameters:

```razor
<BitPagination 
    FirstIcon="FirstPageIcon" 
    PreviousIcon="PrevPageIcon" 
    NextIcon="NextPageIcon" 
    LastIcon="LastPageIcon" 
    Count="5" />
```

### 7. Color Variants

Change the color theme using the `Color` parameter:

```razor
<BitPagination Color="BitColor.Primary" Count="5" />
```

### 8. Size Variants

Adjust the size of the pagination buttons with the `Size` parameter (accepts values from the `BitSize` enum):

```razor
<BitPagination Size="BitSize.Large" Count="5" />
```

### 9. Data Binding

Pagination supports both one-way and two-way binding:

**One-way Binding:**

```razor
<BitPagination SelectedPage="1" Count="5" />
```

**Two-way Binding:**

```razor
<BitPagination @bind-SelectedPage="currentPage" Count="5" />
<div>Changed page: <b>@currentPage</b></div>
```

### 10. Right-to-Left (RTL) Mode

Render the Pagination component in RTL mode by setting the direction attribute:

```razor
<div dir="rtl">
    <BitPagination Count="5" />
</div>
```

---

## API Reference

### BitPagination Parameters

| Name                  | Type                              | Default Value | Description                                                                              |
|-----------------------|-----------------------------------|---------------|------------------------------------------------------------------------------------------|
| **BoundaryCount**     | `int`                             | `2`           | Number of page items shown at the beginning and end of the pagination range.             |
| **Classes**           | `BitPaginationClassStyles?`       | `null`        | Custom CSS classes for different parts of the pagination.                                |
| **Color**             | `BitColor?`                       | `null`        | General color theme of the pagination.                                                   |
| **Count**             | `int`                             | `1`           | Total number of pages.                                                                   |
| **DefaultSelectedPage** | `int`                          | `0`           | The default selected page number.                                                        |
| **FirstIcon**         | `string?`                         | `null`        | Icon name for the first page button.                                                     |
| **LastIcon**          | `string?`                         | `null`        | Icon name for the last page button.                                                      |
| **MiddleCount**       | `int`                             | `3`           | Number of page items displayed in the middle.                                            |
| **NextIcon**          | `string?`                         | `null`        | Icon name for the next page button.                                                      |
| **OnChange**          | `EventCallback<int>`              | `null`        | Callback invoked when the selected page changes.                                         |
| **PreviousIcon**      | `string?`                         | `null`        | Icon name for the previous page button.                                                  |
| **SelectedPage**      | `int`                             | `0`           | Currently selected page number.                                                          |
| **ShowFirstButton**   | `bool`                            | `false`       | Whether to display the first page button.                                                |
| **ShowLastButton**    | `bool`                            | `false`       | Whether to display the last page button.                                                 |
| **ShowNextButton**    | `bool`                            | `true`        | Whether to display the next page button.                                                 |
| **ShowPreviousButton**| `bool`                            | `true`        | Whether to display the previous page button.                                             |
| **Size**              | `BitSize?`                        | `null`        | Size of the pagination buttons (Small, Medium, Large).                                   |
| **Styles**            | `BitPaginationClassStyles?`       | `null`        | Custom CSS styles for different parts of the pagination.                                 |
| **Variant**           | `BitVariant?`                     | `null`        | Visual variant of the pagination (Fill, Standard, Text).                                 |

### Inherited BitComponentBase Parameters

| Name             | Type                         | Default Value                      | Description                                                                  |
|------------------|------------------------------|------------------------------------|------------------------------------------------------------------------------|
| **AriaLabel**    | `string?`                    | `null`                             | ARIA label for the control (for screen readers).                           |
| **Class**        | `string?`                    | `null`                             | Custom CSS class for the root element.                                     |
| **Dir**          | `BitDir?`                    | `null`                             | Specifies text direction (LTR, RTL, or Auto).                              |
| **HtmlAttributes** | `Dictionary<string, object>` | `new Dictionary<string, object>()` | Additional attributes for the root element.                                |
| **Id**           | `string?`                    | `null`                             | Custom id for the root element; if null, a unique id is generated.           |
| **IsEnabled**    | `bool`                     | `true`                             | Indicates whether the component is enabled.                                |
| **Style**        | `string?`                    | `null`                             | Inline CSS styles for the root element.                                    |
| **Visibility**   | `BitVisibility`              | `BitVisibility.Visible`            | Determines if the component is visible, hidden, or collapsed.                |

### Public Members

- **UniqueId:** A read-only unique identifier generated at component construction.
- **RootElement:** A reference to the root DOM element of the component.

### BitPaginationClassStyles Properties

| Name                | Type      | Default Value | Description                                                             |
|---------------------|-----------|---------------|-------------------------------------------------------------------------|
| **Root**            | `string?` | `null`        | Custom CSS class for the root element of the BitPagination.             |
| **Button**          | `string?` | `null`        | Custom CSS class for pagination buttons.                                |
| **Ellipsis**        | `string?` | `null`        | Custom CSS class for the ellipsis indicator.                            |
| **SelectedButton**  | `string?` | `null`        | Custom CSS class for the selected page button.                          |
| **FirstButton**     | `string?` | `null`        | Custom CSS class for the first page button.                             |
| **FirstButtonIcon** | `string?` | `null`        | Custom CSS class for the icon in the first page button.                 |
| **PreviousButton**  | `string?` | `null`        | Custom CSS class for the previous page button.                          |
| **PreviousButtonIcon** | `string?` | `null`    | Custom CSS class for the icon in the previous page button.              |
| **NextButton**      | `string?` | `null`        | Custom CSS class for the next page button.                              |
| **NextButtonIcon**  | `string?` | `null`        | Custom CSS class for the icon in the next page button.                  |
| **LastButton**      | `string?` | `null`        | Custom CSS class for the last page button.                              |
| **LastButtonIcon**  | `string?` | `null`        | Custom CSS class for the icon in the last page button.                  |

---

## Enumerations

### BitColor Enum

| Name           | Value | Description                     |
|----------------|-------|---------------------------------|
| **Primary**    | 0     | Primary (info) color.           |
| **Secondary**  | 1     | Secondary color.                |
| **Tertiary**   | 2     | Tertiary color.                 |
| **Info**       | 3     | Info general color.             |
| **Success**    | 4     | Success color.                  |
| **Warning**    | 5     | Warning color.                  |
| **SevereWarning** | 6  | Severe warning color.           |
| **Error**      | 7     | Error color.                    |

### BitSize Enum

| Name    | Value | Description        |
|---------|-------|--------------------|
| **Small**   | 0     | The small size.   |
| **Medium**  | 1     | The medium size.  |
| **Large**   | 2     | The large size.   |

### BitVariant Enum

| Name      | Value | Description                      |
|-----------|-------|----------------------------------|
| **Fill**      | 0     | Fill styled variant.           |
| **Standard**  | 1     | Outline styled variant.        |
| **Text**      | 2     | Text styled variant.           |

### BitVisibility Enum

| Name       | Value | Description                                                       |
|------------|-------|-------------------------------------------------------------------|
| **Visible**    | 0     | The component is visible.                                      |
| **Hidden**     | 1     | The component is hidden but occupies space (visibility: hidden). |
| **Collapsed**  | 2     | The component is not rendered (display: none).                  |

### BitDir Enum

| Name  | Value | Description                                                                 |
|-------|-------|-----------------------------------------------------------------------------|
| **Ltr**  | 0     | Left-to-right direction (e.g., English).                                   |
| **Rtl**  | 1     | Right-to-left direction (e.g., Arabic).                                    |
| **Auto** | 2     | Automatically determines text direction based on content.                  |

---