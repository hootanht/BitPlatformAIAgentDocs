# BitCarousel Component Reference

The **BitCarousel** component (also referred to as a SlideShow) lets you display your items in separate slides. It is ideal for presenting images or content in a carousel format with advanced features such as infinite scrolling, auto play, customizable navigation controls, and RTL support.

---

## Overview

The **BitCarousel** component displays a set of items in a sliding format. It supports:
- Basic slide-show functionality
- Infinite scrolling for continuous loops
- Auto play with adjustable intervals
- Custom navigation buttons and dot indicators
- RTL (right-to-left) layout support for languages like Arabic
- Advanced customization through API properties and styling

---

## Usage

### Basic Carousel

The following example demonstrates a simple carousel with four slides. Each slide includes a number indicator and an image.

```html
<!-- Basic Carousel Example -->
<div class="bit-csl bit-csl-apri">
  <div class="bit-csl-cnt" style="display: block;">
    <div class="bit-crsi" style="width: 969.609375px; display: block; transform: translateX(0%);">
      <div class="number">1 / 4</div>
      <img class="image" src="_content/Bit.BlazorUI.Demo.Client.Core/images/carousel/img1.jpg" alt="Slide 1">
    </div>
    <div class="bit-crsi" style="width: 969.609375px; display: block; transform: translateX(100%);">
      <div class="number">2 / 4</div>
      <img class="image" src="_content/Bit.BlazorUI.Demo.Client.Core/images/carousel/img2.jpg" alt="Slide 2">
    </div>
    <div class="bit-crsi" style="width: 969.609375px; display: block; transform: translateX(200%);">
      <div class="number">3 / 4</div>
      <img class="image" src="_content/Bit.BlazorUI.Demo.Client.Core/images/carousel/img3.jpg" alt="Slide 3">
    </div>
    <div class="bit-crsi" style="width: 969.609375px; display: block; transform: translateX(300%);">
      <div class="number">4 / 4</div>
      <img class="image" src="_content/Bit.BlazorUI.Demo.Client.Core/images/carousel/img4.jpg" alt="Slide 4">
    </div>
    <!-- Navigation Buttons -->
    <div class="bit-csl-lbt">
      <i class="bit-icon bit-icon--ChevronRight"></i>
    </div>
    <div class="bit-csl-rbt" style="display: none;">
      <i class="bit-csl-rbi bit-icon bit-icon--ChevronRight"></i>
    </div>
  </div>
  <!-- Dots Indicator -->
  <div class="bit-csl-dcn">
    <div class="bit-csl-dot bit-csl-cud"></div>
    <div class="bit-csl-dot"></div>
    <div class="bit-csl-dot"></div>
    <div class="bit-csl-dot"></div>
  </div>
</div>
```

---

### Infinite Scrolling

Enable infinite scrolling so that the carousel continuously loops through slides.

```html
<!-- Infinite Scrolling Carousel Example -->
<div class="bit-csl bit-csl-apri">
  <div class="bit-csl-cnt">
    <div class="bit-crsi" style="width: 969.609375px; display: block; transform: translateX(0%);">
      <img class="image" src="_content/Bit.BlazorUI.Demo.Client.Core/images/carousel/img1.jpg" alt="Slide 1">
      <div class="text-title">Aurora</div>
      <div class="text-description">This is Aurora and it's fantastic</div>
    </div>
    <div class="bit-crsi" style="width: 969.609375px; display: block; transform: translateX(100%);">
      <img class="image" src="_content/Bit.BlazorUI.Demo.Client.Core/images/carousel/img2.jpg" alt="Slide 2">
      <div class="text-title">Beautiful Mountain</div>
      <div class="text-description">This is a Beautiful Mountain and it's gorgeous</div>
    </div>
    <div class="bit-crsi" style="width: 969.609375px; display: block; transform: translateX(200%);">
      <img class="image" src="_content/Bit.BlazorUI.Demo.Client.Core/images/carousel/img3.jpg" alt="Slide 3">
      <div class="text-title">Forest In The Valley</div>
      <div class="text-description">This is a Forest In The Valley and it's beautiful</div>
    </div>
    <div class="bit-crsi" style="width: 969.609375px; display: block; transform: translateX(300%);">
      <img class="image" src="_content/Bit.BlazorUI.Demo.Client.Core/images/carousel/img4.jpg" alt="Slide 4">
      <div class="text-title">Road Among The Mountains</div>
      <div class="text-description">This is a Road Among The Mountains and it's amazing</div>
    </div>
    <!-- Navigation Buttons -->
    <div class="bit-csl-lbt">
      <i class="bit-icon bit-icon--ChevronRight"></i>
    </div>
    <div class="bit-csl-rbt">
      <i class="bit-csl-rbi bit-icon bit-icon--ChevronRight"></i>
    </div>
  </div>
  <div class="bit-csl-dcn">
    <div class="bit-csl-dot bit-csl-cud"></div>
    <div class="bit-csl-dot"></div>
    <div class="bit-csl-dot"></div>
    <div class="bit-csl-dot"></div>
  </div>
</div>
```

---

### HideDots

Use the `HideDots` property to hide the dot indicators below the carousel.

```html
<!-- HideDots Carousel Example -->
<div class="bit-csl bit-csl-apri">
  <div class="bit-csl-cnt">
    <!-- Slides as in the basic example -->
    <div class="bit-crsi" style="width: 969.609375px; display: block; transform: translateX(0%);">
      <div class="number">1 / 4</div>
      <img class="image" src="_content/Bit.BlazorUI.Demo.Client.Core/images/carousel/img1.jpg" alt="Slide 1">
      <div class="text-title">Aurora</div>
      <div class="text-description">This is Aurora and it's fantastic</div>
    </div>
    <!-- Additional slides... -->
  </div>
  <!-- Dots are hidden in this configuration -->
</div>
```

---

### Public API Control

Programmatically control the carousel using public API methods. For example, you can navigate slides via buttons that call methods such as `GoNext`, `GoPrev`, and `GoTo`.

```html
<!-- Public API Control Example -->
<div class="bit-csl bit-csl-apri">
  <div class="bit-csl-cnt">
    <!-- Carousel slides (as shown in basic usage) -->
  </div>
  <div class="buttons-container">
    <button class="bit-btn bit-btn-fil bit-btn-pri bit-btn-md">&lt; Prev</button>
    <button class="bit-btn bit-btn-fil bit-btn-pri bit-btn-md">Next &gt;</button>
  </div>
  <div class="goto-container">
    <button class="bit-btn bit-btn-fil bit-btn-pri bit-btn-md goto-button">GoTo</button>
    <div class="bit-nfl bit-nfl-ltp">
      <input type="number" min="-2147483648" max="2147483647" step="1" value="0">
    </div>
  </div>
</div>
```

---

### AutoPlay

Enable AutoPlay to automatically transition between slides after a set interval.

```html
<!-- AutoPlay Carousel Example -->
<div class="bit-csl bit-csl-apri">
  <div class="bit-csl-cnt" style="transition: all 0.5s; transform: translateX(-100%);">
    <div class="bit-crsi" style="width: 969.609375px; display: block;">
      <div class="number">1 / 4</div>
      <img class="image" src="_content/Bit.BlazorUI.Demo.Client.Core/images/carousel/img1.jpg" alt="Slide 1">
      <div class="text-title">Aurora</div>
      <div class="text-description">This is Aurora and it's fantastic</div>
    </div>
    <!-- Additional slides... -->
  </div>
  <div class="bit-csl-dcn">
    <div class="bit-csl-dot"></div>
    <div class="bit-csl-dot"></div>
    <div class="bit-csl-dot"></div>
    <div class="bit-csl-dot bit-csl-cud"></div>
  </div>
</div>
```

---

### Advanced Configuration

Customize advanced settings such as the number of visible items, scroll count, and custom styles to tailor the carousel to your needs.

```html
<!-- Advanced Carousel Example -->
<div id="omu5ga" class="bit-csl" style="height: 100px;">
  <div class="bit-csl-cnt">
    <div class="bit-crsi item" style="width: 323.203125px; display: block; transform: translateX(0%);">
      <div>1</div>
    </div>
    <div class="bit-crsi item" style="width: 323.203125px; display: block; transform: translateX(100%);">
      <div>2</div>
    </div>
    <div class="bit-crsi item" style="width: 323.203125px; display: block; transform: translateX(200%);">
      <div>3</div>
    </div>
    <div class="bit-crsi item" style="width: 323.203125px; display: block; transform: translateX(300%);">
      <div>4</div>
    </div>
    <div class="bit-crsi item" style="width: 323.203125px; display: block; transform: translateX(400%);">
      <div>5</div>
    </div>
    <div class="bit-crsi item" style="width: 323.203125px; display: block; transform: translateX(500%);">
      <div>6</div>
    </div>
    <!-- Additional items... -->
  </div>
  <!-- Navigation controls as needed -->
</div>
```

---

### RTL Support

For right-to-left language support, add the `dir="rtl"` attribute and use the appropriate classes.

```html
<!-- RTL Carousel Example -->
<div id="i7pig0" class="bit-csl bit-rtl bit-csl-apri" dir="rtl" style="height: 100px;">
  <div class="bit-csl-cnt" style="direction: rtl;">
    <div class="bit-crsi item" style="width: 323.203125px; display: block; transform: translateX(0%);">
      <div>یک</div>
    </div>
    <div class="bit-crsi item" style="width: 323.203125px; display: block; transform: translateX(-100%);">
      <div>دو</div>
    </div>
    <div class="bit-crsi item" style="width: 323.203125px; display: block; transform: translateX(-200%);">
      <div>سه</div>
    </div>
    <div class="bit-crsi item" style="width: 323.203125px; display: block; transform: translateX(-300%);">
      <div>چهار</div>
    </div>
    <div class="bit-crsi item" style="width: 323.203125px; display: block; transform: translateX(-400%);">
      <div>پنج</div>
    </div>
    <div class="bit-crsi item" style="width: 323.203125px; display: block; transform: translateX(-500%);">
      <div>شیش</div>
    </div>
    <!-- Additional RTL items... -->
  </div>
  <div class="bit-csl-dcn" style="direction: rtl;">
    <div class="bit-csl-dot bit-csl-cud"></div>
    <div class="bit-csl-dot"></div>
    <div class="bit-csl-dot"></div>
  </div>
</div>
```

---

## API Reference

### BitCarousel Parameters

| **Name**              | **Type**                      | **Default Value** | **Description**                                                                                                  |
|-----------------------|-------------------------------|-------------------|------------------------------------------------------------------------------------------------------------------|
| `AnimationDuration`   | `double`                      | `0.5`             | Sets the duration (in seconds) of the slide animation.                                                          |
| `AutoPlay`            | `bool`                        | `false`           | Enables/disables automatic slide transitions.                                                                    |
| `AutoPlayInterval`    | `double`                      | `2000`            | The interval (in milliseconds) between automatic transitions.                                                   |
| `ChildContent`        | `RenderFragment?`             | `null`            | The content (slides) to render inside the carousel.                                                             |
| `Classes`             | `BitCarouselClassStyles?`     | `null`            | Custom CSS classes for various parts of the carousel.                                                            |
| `GoLeftIcon`          | `string?`                     | `null`            | Custom icon for the left navigation button.                                                                     |
| `GoRightIcon`         | `string?`                     | `null`            | Custom icon for the right navigation button.                                                                    |
| `HideDots`            | `bool`                        | `false`           | If true, hides the navigation dots indicator.                                                                   |
| `HideNextPrev`        | `bool`                        | `false`           | If true, hides the next/previous navigation buttons.                                                            |
| `InfiniteScrolling`   | `bool`                        | `false`           | If enabled, the carousel loops infinitely (first slide follows the last, and vice versa).                         |
| `OnChange`            | `EventCallback<int>`          | –                 | Event triggered on slide change. The integer parameter represents the new slide index.                             |
| `ScrollItemsCount`    | `int`                         | `1`               | Number of items to scroll on navigation.                                                                         |
| `Styles`              | `BitCarouselClassStyles?`     | `null`            | Custom CSS styles for the carousel.                                                                              |
| `VisibleItemsCount`   | `int`                         | `1`               | Number of items visible at once in the carousel.                                                                 |

### Inherited BitComponentBase Parameters

| **Name**         | **Type**                       | **Default Value**                  | **Description**                                                                                         |
|------------------|--------------------------------|------------------------------------|---------------------------------------------------------------------------------------------------------|
| `AriaLabel`      | `string?`                      | `null`                             | Provides an accessible label for the carousel.                                                         |
| `Class`          | `string?`                      | `null`                             | Additional CSS class names for the root element.                                                       |
| `Dir`            | `BitDir?`                      | `null`                             | Specifies text direction (LTR, RTL, or Auto).                                                           |
| `HtmlAttributes` | `Dictionary<string, object>`   | `new Dictionary<string, object>()` | Additional HTML attributes to include on the root element.                                             |
| `Id`             | `string?`                      | `null`                             | Custom identifier for the carousel. A unique ID is generated if none is provided.                        |
| `IsEnabled`      | `bool`                         | `true`                             | Determines if the carousel is interactive.                                                             |
| `Style`          | `string?`                      | `null`                             | Inline CSS styles for the carousel’s root element.                                                     |
| `Visibility`     | `BitVisibility`                | `BitVisibility.Visible`            | Controls whether the carousel is visible, hidden, or collapsed.                                        |

### Public API Methods

| **Name**   | **Type** | **Default Value** | **Description**                                         |
|------------|----------|-------------------|---------------------------------------------------------|
| `GoNext`   | `Task`   | –                 | Programmatically navigates to the next slide.           |
| `GoPrev`   | `Task`   | –                 | Programmatically navigates to the previous slide.       |
| `GoTo`     | `Task`   | –                 | Navigates to a specific slide by index.                 |
| `Pause`    | `Task`   | –                 | Pauses the AutoPlay feature if enabled.                 |
| `Resume`   | `Task`   | –                 | Resumes AutoPlay if it was paused.                      |

---

## Enumerations

### BitVisibility Enum

| **Name**    | **Value** | **Description**                                                                           |
|-------------|-----------|-------------------------------------------------------------------------------------------|
| `Visible`   | `0`       | The carousel is visible.                                                                  |
| `Hidden`    | `1`       | The carousel is hidden using `visibility: hidden` (space is still reserved).              |
| `Collapsed` | `2`       | The carousel is collapsed using `display: none` (no space is allocated).                   |

### BitDir Enum

| **Name** | **Value** | **Description**                                                           |
|----------|-----------|---------------------------------------------------------------------------|
| `Ltr`    | `0`       | Left-to-right text direction (e.g., English).                             |
| `Rtl`    | `1`       | Right-to-left text direction (e.g., Arabic, Hebrew).                      |
| `Auto`   | `2`       | Automatically determine direction based on content.                     |

---

## Class Styles

The `BitCarouselClassStyles` object lets you override the default styling of various parts of the carousel. Typical properties include:

- **Root:** CSS classes/styles for the carousel’s root container.
- **Container:** Styles for the inner container that holds the slides.
- **Buttons:** Styles for the navigation buttons.
- **GoLeftButton / GoRightButton:** Custom styles for the left and right navigation buttons.
- **GoLeftButtonIcon / GoRightButtonIcon:** Styles for the icons on the navigation buttons.
- **DotsContainer:** Styles for the container holding the dot indicators.
- **Dots:** Styles for individual dot indicators.
- **CurrentDot:** Styles for the currently active dot.

---