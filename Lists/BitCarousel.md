# BitCarousel Component Reference (Blazor UI / SlideShow)

## 1. Overview

**`BitCarousel`** (also referred to as SlideShow) is a Blazor component used to display a collection of items (like images, text, or complex components) in individual, navigable slides. It allows users to cycle through content sequentially, often used for image galleries, feature showcases, or onboarding flows.

**Key Purpose:** To present multiple pieces of content in a compact, interactive, slide-based format.

## 2. Key Features

*   **Item Definition:** Uses nested `BitCarouselItem` components to define the content of each slide.
*   **Navigation:** Provides built-in previous/next buttons and dot indicators for navigation.
*   **Infinite Scrolling:** Supports looping from the last slide back to the first and vice-versa (`InfiniteScrolling`).
*   **AutoPlay:** Can automatically cycle through slides at a configurable interval (`AutoPlay`, `AutoPlayInterval`).
*   **Multiple Visible Items:** Can display more than one item per slide view (`VisibleItemsCount`) and control how many items scroll at once (`ScrollItemsCount`).
*   **Programmatic Control:** Exposes a public API (`GoNext`, `GoPrev`, `GoTo`, `Pause`, `Resume`) for controlling navigation from C# code using `@ref`.
*   **Customization:** Allows hiding navigation elements (`HideDots`, `HideNextPrev`), customizing navigation icons (`GoLeftIcon`, `GoRightIcon`), setting animation duration (`AnimationDuration`), and applying custom styles/classes (`Class`, `Style`, `Classes`, `Styles`).
*   **RTL Support:** Built-in support for Right-to-Left layouts using the `Dir` parameter.
*   **Event Handling:** Provides an `OnChange` event that fires when the active slide changes.

## 3. Core Usage (Basic Example)

The fundamental structure involves a `BitCarousel` parent component containing one or more `BitCarouselItem` children, each representing a slide.

**Components:**
*   `BitCarousel`: The main container and controller.
*   `BitCarouselItem`: Represents a single slide within the carousel.

**Example (`.razor`):**

```cshtml
<style>
    /* Basic styling for the slide content */
    .basic-carousel-item .numbertext { /* Renamed from .number for clarity */
        position: absolute;
        top: 0.75rem;
        left: 0.75rem; /* Added for positioning */
        padding: 0.5rem;
        font-size: 0.75rem;
        color: #D7D7D7;
        background-color: rgba(0,0,0,0.5); /* Added for visibility */
        border-radius: 3px;
    }

    .basic-carousel-item .image {
        display: block; /* Prevent extra space below image */
        width: 100%;
        height: 300px; /* Example fixed height */
        object-fit: cover; /* Ensure image covers the area */
    }
</style>

<BitCarousel AriaLabel="Image Carousel Example">
    <BitCarouselItem Class="basic-carousel-item">
        <div class="numbertext">1 / 4</div>
        <img class="image" src="/images/carousel/img1.jpg" alt="Aurora Image">
    </BitCarouselItem>
    <BitCarouselItem Class="basic-carousel-item">
        <div class="numbertext">2 / 4</div>
        <img class="image" src="/images/carousel/img2.jpg" alt="Mountain Image">
    </BitCarouselItem>
    <BitCarouselItem Class="basic-carousel-item">
        <div class="numbertext">3 / 4</div>
        <img class="image" src="/images/carousel/img3.jpg" alt="Forest Image">
    </BitCarouselItem>
    <BitCarouselItem Class="basic-carousel-item">
        <div class="numbertext">4 / 4</div>
        <img class="image" src="/images/carousel/img4.jpg" alt="Road Image">
    </BitCarouselItem>
</BitCarousel>
```

**Explanation:**

1. **`<BitCarousel>`:** The main component that manages the slides. `AriaLabel` is added for accessibility.
2. **`<BitCarouselItem>`:** Each child defines one slide. The content inside (divs, images, etc.) is standard HTML/Blazor markup.
3. **Styling:** CSS is used to style the content within each slide (positioning text, setting image dimensions). It's applied via the `Class` parameter on `BitCarouselItem` or directly to elements inside.
4. **Navigation:** By default, `BitCarousel` displays previous/next buttons and dot indicators.

---

## 4. Key Features & Configuration

### 4.1 Infinite Scrolling

Allows seamless looping from the last slide to the first, and vice-versa.

**Parameter:** `InfiniteScrolling` (boolean, default: `false`)

```cshtml
<BitCarousel InfiniteScrolling>
    @* ... BitCarouselItem slides ... *@
    <BitCarouselItem>
        <img class="image" src="/images/carousel/img1.jpg" />
        <div class="text-title">Aurora</div>
        <div class="text-description">This is Aurora and it's fantastic</div>
    </BitCarouselItem>
    @* Other items... *@
</BitCarousel>
```

### 4.2 Hiding Navigation Elements

You can hide the default navigation controls.

**Parameters:**

* `HideDots` (boolean, default: `false`): Hides the dot indicators below the carousel.
* `HideNextPrev` (boolean, default: `false`): Hides the previous and next arrow buttons.

```cshtml
@* Example hiding dots *@
<BitCarousel HideDots>
    @* ... BitCarouselItem slides ... *@
</BitCarousel>

@* Example hiding arrows (often used with programmatic control or autoplay) *@
<BitCarousel HideNextPrev>
    @* ... BitCarouselItem slides ... *@
</BitCarousel>
```

### 4.3 AutoPlay

Automatically transitions between slides after a specified interval.

**Parameters:**

* `AutoPlay` (boolean, default: `false`): Enables automatic playback.
* `AutoPlayInterval` (double, default: `2000`): The time (in milliseconds) between automatic transitions.

```cshtml
<BitCarousel AutoPlay AutoPlayInterval="3000" InfiniteScrolling> @* Autoplay every 3 seconds, loops infinitely *@
     @* ... BitCarouselItem slides ... *@
    <BitCarouselItem>
        <img class="image" src="/images/carousel/img1.jpg" />
        <div class="text-title">Aurora</div>
        <div class="text-description">This is Aurora and it's fantastic</div>
    </BitCarouselItem>
     @* Other items... *@
</BitCarousel>
```

### 4.4 Multiple Visible Items

Display several items within the carousel viewport simultaneously and control how many scroll at a time.

**Parameters:**

* `VisibleItemsCount` (int, default: `1`): Number of items visible at once.
* `ScrollItemsCount` (int, default: `1`): Number of items to scroll when navigating.

```cshtml
<style>
    .multi-item { text-align: center; height: 100px; line-height: 100px; background-color: lightblue; border: 1px solid blue; }
</style>

<BitCarousel VisibleItemsCount="3" ScrollItemsCount="3" Style="height: 120px;" HideDots>
    <BitCarouselItem Class="multi-item"><div>1</div></BitCarouselItem>
    <BitCarouselItem Class="multi-item"><div>2</div></BitCarouselItem>
    <BitCarouselItem Class="multi-item"><div>3</div></BitCarouselItem>
    <BitCarouselItem Class="multi-item"><div>4</div></BitCarouselItem>
    <BitCarouselItem Class="multi-item"><div>5</div></BitCarouselItem>
    <BitCarouselItem Class="multi-item"><div>6</div></BitCarouselItem>
    <BitCarouselItem Class="multi-item"><div>7</div></BitCarouselItem>
    <BitCarouselItem Class="multi-item"><div>8</div></BitCarouselItem>
    <BitCarouselItem Class="multi-item"><div>9</div></BitCarouselItem>
</BitCarousel>
```

**Explanation:** This example shows 3 items at a time. Clicking next/prev will scroll by 3 items. The `Style` is adjusted to accommodate the items. Dots are hidden as they represent pages, not individual items here.

### 4.5 Programmatic Control (Public API)

Control the carousel's navigation using C# code.

**Steps:**

1. Add `@ref="myCarousel"` to the `<BitCarousel>` component.
2. Declare a variable in `@code`: `private BitCarousel myCarousel;`
3. Call methods on the `myCarousel` instance: `GoNext()`, `GoPrev()`, `GoTo(index)`, `Pause()`, `Resume()`.

```cshtml
<BitCarousel @ref="carousel" HideNextPrev> @* Hide default buttons *@
    @* ... BitCarouselItem slides ... *@
    <BitCarouselItem>
        <img class="image" src="/images/carousel/img1.jpg" />
        <div class="text-title">Aurora</div>
    </BitCarouselItem>
    @* Other items... *@
</BitCarousel>

<div class="buttons-container" style="margin-top: 1rem; display: flex; justify-content: space-between;">
    <div>
        <BitButton OnClick="HandlePrev">&lt; Prev</BitButton>
        <BitButton OnClick="HandleNext" Style="margin-left: 0.5rem;">Next &gt;</BitButton>
    </div>
    <div style="display: flex; align-items: center;">
        <BitNumberField @bind-Value="goToIndex" Min="0" Max="3" Style="width: 80px;" /> @* Assuming 4 slides (0-3) *@
        <BitButton OnClick="HandleGoTo" Style="margin-left: 0.5rem;">Go To</BitButton>
    </div>
</div>

@code {
    private BitCarousel carousel;
    private int goToIndex = 0; // Default to first slide

    private async Task HandleNext()
    {
        if (carousel is not null) await carousel.GoNext();
    }

    private async Task HandlePrev()
    {
        if (carousel is not null) await carousel.GoPrev();
    }

    private async Task HandleGoTo()
    {
        if (carousel is not null) await carousel.GoTo(goToIndex);
    }

    // You can also use Pause() and Resume() for AutoPlay control
    // private async Task PauseCarousel() => await carousel?.Pause();
    // private async Task ResumeCarousel() => await carousel?.Resume();
}
```

### 4.6 Right-to-Left (RTL) Support

Enable RTL layout and navigation.

**Parameter:** `Dir="BitDir.Rtl"`

```cshtml
<style>
    .rtl-item { text-align: center; height: 100px; line-height: 100px; background-color: lightcoral; border: 1px solid red; }
</style>

<BitCarousel Dir="BitDir.Rtl" VisibleItemsCount="3" ScrollItemsCount="1" InfiniteScrolling Style="height: 120px;">
    <BitCarouselItem Class="rtl-item"><div>یک</div></BitCarouselItem>
    <BitCarouselItem Class="rtl-item"><div>دو</div></BitCarouselItem>
    <BitCarouselItem Class="rtl-item"><div>سه</div></BitCarouselItem>
    <BitCarouselItem Class="rtl-item"><div>چهار</div></BitCarouselItem>
    <BitCarouselItem Class="rtl-item"><div>پنج</div></BitCarouselItem>
    @* ... more items ... *@
</BitCarousel>
```

**Explanation:** Sets the direction to RTL. Navigation buttons and slide transitions will respect this direction.

---

## 5. Styling

* **Basic:** Use standard `Class` and `Style` parameters on `BitCarousel` and `BitCarouselItem`.
* **Advanced:** Use the `Classes` and `Styles` parameters of type `BitCarouselClassStyles` to target specific internal elements (root, container, buttons, dots).

```csharp
// Example of setting Classes in @code block
private BitCarouselClassStyles customClasses = new()
{
    Root = "my-custom-carousel-root",
    Container = "my-carousel-container",
    DotsContainer = "my-dots-container",
    CurrectDot = "my-active-dot" // Typo 'CurrectDot' is present in source HTML API table
};
```

```cshtml
<BitCarousel Classes="customClasses">
    @* ... Items ... *@
</BitCarousel>

<style>
    .my-custom-carousel-root { border: 2px solid green; }
    .my-carousel-container { background-color: #eee; }
    .my-dots-container { bottom: 20px; } /* Adjust dot position */
    .my-active-dot { background-color: green !important; } /* Style active dot */
</style>
```

---

## 6. API Reference

### `BitCarousel` Parameters

| Name                | Type                   | Default Value | Description                                                                                                                               |
| :------------------ | :--------------------- | :------------ | :---------------------------------------------------------------------------------------------------------------------------------------- |
| `ChildContent`      | `RenderFragment?`      | `null`        | The content of the carousel, typically consists of `BitCarouselItem` components.                                                          |
| `VisibleItemsCount` | `int`                  | `1`           | Number of items visible in the carousel viewport at one time.                                                                             |
| `ScrollItemsCount`  | `int`                  | `1`           | Number of items to scroll when navigating using next/prev buttons.                                                                        |
| `InfiniteScrolling` | `bool`                 | `false`       | Enables looping navigation (first slide follows last, last slide precedes first).                                                         |
| `AutoPlay`          | `bool`                 | `false`       | Enables automatic transitioning between slides.                                                                                           |
| `AutoPlayInterval`  | `double`               | `2000`        | Interval (in milliseconds) for automatic slide transitions when `AutoPlay` is enabled.                                                    |
| `AnimationDuration` | `double`               | `0.5`         | Duration (in seconds) of the slide transition animation.                                                                                  |
| `HideDots`          | `bool`                 | `false`       | Hides the dot indicators used for navigation.                                                                                             |
| `HideNextPrev`      | `bool`                 | `false`       | Hides the default next and previous navigation buttons.                                                                                   |
| `GoLeftIcon`        | `string?`              | `null`        | Custom icon name (e.g., from Fluent UI System Icons) for the "go left" button (appears on the right in LTR, left in RTL).                 |
| `GoRightIcon`       | `string?`              | `null`        | Custom icon name for the "go right" button (appears on the left in LTR, right in RTL).                                                    |
| `OnChange`          | `EventCallback<int>`   |               | Event triggered when the current slide index changes. The `int` argument is the new zero-based index.                                     |
| `Classes`           | `BitCarouselClassStyles?` | `null`        | Custom CSS classes for specific parts of the component (see `BitCarouselClassStyles`).                                                    |
| `Styles`            | `BitCarouselClassStyles?` | `null`        | Custom CSS inline styles for specific parts of the component (see `BitCarouselClassStyles`). *Note: API table shows type as ClassStyles* |
| **Inherited**       |                        |               | *Includes `AriaLabel`, `Class`, `Dir`, `HtmlAttributes`, `Id`, `IsEnabled`, `Style`, `Visibility` from `BitComponentBase`.*               |

### `BitCarousel` Public Methods

| Name     | Return Type | Description                                    |
| :------- | :---------- | :--------------------------------------------- |
| `GoNext()` | `Task`      | Navigates to the next slide/page.              |
| `GoPrev()` | `Task`      | Navigates to the previous slide/page.          |
| `GoTo(int index)` | `Task`      | Navigates directly to the slide at the specified zero-based `index`. |
| `Pause()`  | `Task`      | Pauses automatic playback if `AutoPlay` is enabled. |
| `Resume()` | `Task`      | Resumes automatic playback if `AutoPlay` is enabled and was paused. |

### `BitCarouselItem` Parameters

`BitCarouselItem` primarily serves as a container for the content of a single slide. It accepts standard `BitComponentBase` parameters:

| Name            | Type                         | Default Value | Description                                                 |
| :-------------- | :--------------------------- | :------------ | :---------------------------------------------------------- |
| `ChildContent`  | `RenderFragment?`            | `null`        | The HTML or Blazor components that make up the slide's content. |
| **Inherited**   |                              |               | *Includes `Class`, `Style`, `Id`, `Visibility`, etc. from `BitComponentBase`.* |

### `BitCarouselClassStyles` Properties

Used to apply custom classes/styles to internal elements via the `Classes` or `Styles` parameters of `BitCarousel`.

| Name                | Type      | Default Value | Description                                                                 |
| :------------------ | :-------- | :------------ | :-------------------------------------------------------------------------- |
| `Root`              | `string?` | `null`        | Styles/classes for the main root element.                                   |
| `Container`         | `string?` | `null`        | Styles/classes for the container holding the slides.                        |
| `Buttons`           | `string?` | `null`        | Styles/classes applied to *both* next/prev buttons (likely their container).|
| `GoLeftButton`      | `string?` | `null`        | Styles/classes for the "go left" navigation button.                         |
| `GoLeftButtonIcon`  | `string?` | `null`        | Styles/classes for the icon *inside* the "go left" button.                  |
| `GoRightButton`     | `string?` | `null`        | Styles/classes for the "go right" navigation button.                        |
| `GoRightButtonIcon` | `string?` | `null`        | Styles/classes for the icon *inside* the "go right" button.                 |
| `DotsContainer`     | `string?` | `null`        | Styles/classes for the container holding the dot indicators.                |
| `Dots`              | `string?` | `null`        | Styles/classes applied to each individual dot indicator.                    |
| `CurrectDot`        | `string?` | `null`        | Styles/classes applied specifically to the *active/current* dot indicator. (Note typo in source) |

### Inherited `BitComponentBase` Parameters

*(Same as provided in the BitBasicList reference)*

| Name             | Type                         | Default Value           | Description                                                               |
| :--------------- | :--------------------------- | :---------------------- | :------------------------------------------------------------------------ |
| `AriaLabel`      | `string?`                    | `null`                  | Aria-label for accessibility.                                             |
| `Class`          | `string?`                    | `null`                  | Custom CSS class for the root element.                                    |
| `Dir`            | `BitDir?`                    | `null`                  | Component direction (Ltr, Rtl, Auto).                                     |
| `HtmlAttributes` | `Dictionary<string, object>` | `new Dictionary<...>()` | Additional HTML attributes to render.                                     |
| `Id`             | `string?`                    | `null`                  | Custom id for the root element.                                           |
| `IsEnabled`      | `bool`                       | `true`                  | Whether the component is enabled.                                         |
| `Style`          | `string?`                    | `null`                  | Custom inline CSS style for the root element.                             |
| `Visibility`     | `BitVisibility`              | `BitVisibility.Visible` | Component visibility (Visible, Hidden, Collapsed).                        |

### Inherited `BitComponentBase` Public Members

*(Same as provided in the BitBasicList reference)*

| Name          | Type                | Default Value    | Description                                      |
| :------------ | :------------------ | :--------------- | :----------------------------------------------- |
| `UniqueId`    | `Guid`              | `Guid.NewGuid()` | **Readonly**. Unique identifier for the instance. |
| `RootElement` | `ElementReference`  | *(N/A)*          | Reference to the component's root HTML element.  |

### Enums

**`BitVisibility`** *(Same as BitBasicList)*
**`BitDir`** *(Same as BitBasicList)*

---

## 7. Best Practices & Considerations

* **Accessibility:** Always provide a descriptive `AriaLabel` for the carousel, especially if it contains primarily visual content. Ensure content within `BitCarouselItem` (like images) also has appropriate `alt` text.
* **Content:** Keep slide content concise and focused. Complex components within slides might impact performance, especially with many slides.
* **AutoPlay Interaction:** Consider pausing `AutoPlay` (`Pause()` method) when the user interacts with the carousel controls (e.g., hover, focus, manual navigation) and resuming (`Resume()` method) afterward for a better user experience.
* **Performance:** While not as demanding as virtualized lists, very large numbers of complex slides could still impact initial load time.
* **Styling:** Use the `Classes` parameter for complex styling to keep the markup clean. Ensure custom styles don't break the layout or navigation functionality.
* **Multi-Item View:** When `VisibleItemsCount > 1`, the concept of a "current page" applies. Dots usually represent pages, not individual items. Consider hiding dots (`HideDots`) if it's confusing.

---

## 8. Further Information (Source Links)

* **Component Source Code:** [BitCarousel.razor on GitHub](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Bit.BlazorUI/Components/Lists/Carousel/BitCarousel.razor)
* **Demo Page Source Code:** [BitCarouselDemo.razor on GitHub](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Lists/Carousel/BitCarouselDemo.razor)
* **Project Issues:** [File an Issue on GitHub](https://github.com/bitfoundation/bitplatform/issues/new/choose)
* **Project Discussions:** [Start a Discussion on GitHub](https://github.com/bitfoundation/bitplatform/discussions/new/choose)

