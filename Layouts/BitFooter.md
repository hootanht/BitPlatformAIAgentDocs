# BitFooter Component Reference (Blazor UI)

## Overview

The `BitFooter` component is a layout element used to display a distinct section, typically a colored bar with text or other components, consistently at the bottom of a website or application page. It serves as a container for footer-related content such as copyright information, navigation links, social media icons, etc. The component can be easily styled using standard CSS.

**Use Cases:**

*   Displaying copyright notices.
*   Providing links to privacy policies, terms of service, or site maps.
*   Showing contact information or social media links.
*   Indicating application status or version information.

## Usage

### Basic Usage

The simplest way to use `BitFooter` is to place content directly within its opening and closing tags. This content will be rendered inside the footer element.

```csharp
<BitFooter>
    Copyright © @DateTime.Now.Year Your Company Name. All rights reserved.
</BitFooter>
```

**Explanation:**

* The text "Copyright © ..." will appear inside the rendered footer bar.
* By default, the footer spans the width of its container and has default styling.

### Custom Content and Styling

You can embed complex HTML structures, other Blazor components (like `BitLink`), and apply custom CSS styles to achieve sophisticated footer designs.

**Example:** A footer with centered text, a heart icon, and social media links.

**CSHTML:**

```csharp
<style>
    .my-custom-footer .footer-content { /* Target content within a specific footer */
        flex-grow: 1;
        font-size: 12px;
        text-align: center;
        padding: 0 1rem; /* Add some padding */
        display: flex;
        align-items: center;
        justify-content: center;
        flex-wrap: wrap; /* Allow wrapping on smaller screens */
        gap: 1rem; /* Space between items */
    }

    .my-custom-footer .footer-social-lnk-grp {
        display: flex;
        align-items: center;
        flex-flow: row nowrap;
        justify-content: center;
        gap: 0.5rem; /* Space between icons */
    }

    .my-custom-footer .social-lnk {
        width: 24px; /* Slightly smaller icons */
        height: 24px;
        display: inline-block; /* Ensure links behave correctly */
        vertical-align: middle;
    }

    .my-custom-footer .social-lnk svg {
        width: 100%;
        height: 100%;
        display: block; /* Remove extra space below svg */
    }

    .my-custom-footer .social-lnk svg path {
        fill: var(--bit-color-primary-main); /* Use theme color or specific color */
        transition: fill 0.2s ease-in-out;
    }
    .my-custom-footer .social-lnk:hover svg path {
        fill: var(--bit-color-primary-dark); /* Darker on hover */
    }

    .my-custom-footer .heart {
         color: red;
         margin: 0 0.25rem;
         font-size: 1.2em; /* Make heart slightly bigger */
         vertical-align: middle;
    }
</style>

<BitFooter Class="my-custom-footer">
    <div class="footer-content">
        <span>Made with <span class="heart">♥</span> by bit platform</span>
        <div class="footer-social-lnk-grp">
            <BitLink Href="https://www.linkedin.com/company/bitplatformhq" Target="_blank" AriaLabel="LinkedIn">
                <div class="social-lnk">
                    <!-- LinkedIn SVG -->
                    <svg viewBox="0 0 32 32"><path d="M23.155 23.13H20.2737V18.622C20.2737 17.5464 20.2556 16.164 18.7768 16.164C17.2778 16.164 17.0488 17.3354 17.0488 18.5443V23.13H14.1702V13.8586H16.9322V15.1265H16.9725C17.3562 14.3978 18.2965 13.6289 19.6984 13.6289C22.6158 13.6289 23.1543 15.5484 23.1543 18.0453V23.13H23.155ZM10.9218 12.5928C10.7022 12.593 10.4847 12.5499 10.2818 12.466C10.0789 12.382 9.89452 12.2589 9.73924 12.1036C9.58397 11.9483 9.46083 11.764 9.37688 11.561C9.29293 11.3581 9.24982 11.1407 9.25 10.9211C9.25 10.5906 9.34797 10.2676 9.53153 9.99282C9.71509 9.71804 9.97599 9.50386 10.2813 9.37734C10.5865 9.25082 10.9225 9.21764 11.2466 9.28201C11.5707 9.34637 11.8684 9.50539 12.1022 9.73896C12.336 9.97252 12.4952 10.2701 12.5599 10.5942C12.6245 10.9183 12.5916 11.2542 12.4653 11.5596C12.3391 11.865 12.1251 12.1261 11.8505 12.3098C11.5759 12.4936 11.2529 12.5919 10.9225 12.5921L10.9218 12.5928ZM12.3631 23.13H9.47901V13.8586H12.3631V23.13Z" /></svg>
                </div>
            </BitLink>
            <BitLink Href="https://github.com/bitfoundation/bitplatform" Target="_blank" AriaLabel="GitHub">
                <div class="social-lnk">
                     <!-- GitHub SVG -->
                    <svg viewBox="0 0 32 32"><path d="M18.5373 10.0257C17.3046 9.73929 16.0226 9.73929 14.7899 10.0257C14.078 9.58908 13.5344 9.3884 13.1391 9.30369C12.9704 9.26561 12.7978 9.24767 12.6248 9.25024C12.5461 9.25237 12.4678 9.26183 12.3909 9.27848L12.3808 9.28049L12.3767 9.28251H12.3737L12.5119 9.76757L12.3737 9.28352C12.3029 9.30354 12.2373 9.33883 12.1815 9.38692C12.1258 9.435 12.0812 9.49471 12.051 9.56185C11.7535 10.2281 11.6968 10.9771 11.8907 11.6806C11.3886 12.289 11.115 13.0538 11.1172 13.8427C11.1172 15.4088 11.5791 16.4616 12.3667 17.1382C12.9183 17.6122 13.5879 17.8643 14.2595 18.0085C14.1486 18.3161 14.1203 18.6418 14.1425 18.9746V19.5776C13.7321 19.6633 13.4477 19.6361 13.245 19.5696C12.9919 19.4859 12.7973 19.3175 12.6107 19.0754C12.5132 18.945 12.4223 18.8097 12.3384 18.67L12.2809 18.5763C12.2084 18.4556 12.133 18.3365 12.0551 18.2193C11.8635 17.9359 11.5791 17.5809 11.1192 17.4599L10.6311 17.3318L10.375 18.308L10.8631 18.4361C10.9438 18.4562 11.0486 18.5319 11.2211 18.785C11.2846 18.8788 11.3441 18.9766 11.4127 19.0895L11.4813 19.2005C11.576 19.3538 11.685 19.5232 11.811 19.6886C12.0661 20.0213 12.4141 20.3571 12.9304 20.5276C13.2833 20.6446 13.6847 20.6728 14.1425 20.6022V22.4849C14.1425 22.6187 14.1956 22.7469 14.2902 22.8415C14.3848 22.936 14.513 22.9892 14.6467 22.9892H18.6805C18.8142 22.9892 18.9425 22.936 19.037 22.8415C19.1316 22.7469 19.1847 22.6187 19.1847 22.4849V18.8919C19.1847 18.5742 19.1706 18.2828 19.0808 18.0115C19.7494 17.8703 20.414 17.6182 20.9626 17.1443C21.7491 16.4626 22.21 15.3997 22.21 13.8245V13.8235C22.2075 13.0411 21.9338 12.2838 21.4355 11.6806C21.6291 10.9774 21.5725 10.2288 21.2752 9.56286C21.2452 9.49564 21.2009 9.4358 21.1453 9.38754C21.0897 9.33929 21.0242 9.30378 20.9535 9.28352L20.8153 9.76757C20.9535 9.28352 20.9525 9.28352 20.9515 9.28352L20.9495 9.28251L20.9454 9.28049L20.9363 9.27848C20.9114 9.272 20.8862 9.26695 20.8607 9.26335C20.8079 9.25564 20.7547 9.25127 20.7014 9.25024C20.5284 9.24769 20.3558 9.26563 20.1871 9.30369C19.7928 9.3884 19.2492 9.58908 18.5373 10.0257Z" /></svg>
                </div>
            </BitLink>
            <BitLink Href="@("https://www.youtube.com/@bitplatform")" Target="_blank" AriaLabel="YouTube">
                <div class="social-lnk">
                     <!-- YouTube SVG -->
                    <svg viewBox="0 0 32 32"><path d="M23.6572 11.8735C24 13.21 24 16 24 16C24 16 24 18.79 23.6572 20.1265C23.4667 20.8653 22.9095 21.4465 22.2037 21.643C20.922 22 16.5 22 16.5 22C16.5 22 12.0802 22 10.7962 21.643C10.0875 21.4435 9.531 20.863 9.34275 20.1265C9 18.79 9 16 9 16C9 16 9 13.21 9.34275 11.8735C9.53325 11.1348 10.0905 10.5535 10.7962 10.357C12.0802 10 16.5 10 16.5 10C16.5 10 20.922 10 22.2037 10.357C22.9125 10.5565 23.469 11.137 23.6572 11.8735ZM15 18.625L19.5 16L15 13.375V18.625Z" /></svg>
                </div>
            </BitLink>
            <BitLink Href="https://twitter.com/bitplatformhq" Target="_blank" AriaLabel="Twitter">
                <div class="social-lnk">
                     <!-- Twitter SVG -->
                    <svg viewBox="0 0 32 32"><path d="M22.9075 11.692C22.4053 11.9145 21.8657 12.0649 21.2985 12.1329C21.8838 11.7827 22.3216 11.2315 22.5304 10.5822C21.9805 10.9088 21.3787 11.1387 20.7511 11.2619C20.3291 10.8113 19.7701 10.5126 19.161 10.4123C18.5518 10.3119 17.9266 10.4155 17.3823 10.7069C16.8381 10.9983 16.4052 11.4612 16.151 12.0238C15.8968 12.5864 15.8355 13.2172 15.9765 13.8183C14.8623 13.7623 13.7724 13.4727 12.7774 12.9683C11.7824 12.4639 10.9046 11.7558 10.201 10.8902C9.96036 11.3052 9.82202 11.7864 9.82202 12.2989C9.82175 12.7602 9.93536 13.2145 10.1528 13.6214C10.3702 14.0283 10.6847 14.3753 11.0683 14.6315C10.6234 14.6173 10.1883 14.4971 9.79916 14.2808V14.3169C9.79912 14.9639 10.0229 15.5911 10.4326 16.0919C10.8424 16.5927 11.4127 16.9364 12.0469 17.0645C11.6342 17.1762 11.2014 17.1927 10.7814 17.1126C10.9603 17.6694 11.3089 18.1562 11.7783 18.505C12.2477 18.8539 12.8144 19.0471 13.3991 19.0579C12.4065 19.837 11.1807 20.2597 9.91886 20.2578C9.69533 20.2579 9.472 20.2448 9.25 20.2187C10.5309 21.0423 12.0219 21.4794 13.5447 21.4777C18.6995 21.4777 21.5175 17.2083 21.5175 13.5055C21.5175 13.3852 21.5144 13.2637 21.509 13.1434C22.0572 12.747 22.5303 12.2561 22.9063 11.6938L22.9075 11.692Z" /></svg>
                </div>
            </BitLink>
        </div>
    </div>
</BitFooter>
```

**Explanation:**

1. **`<style>` Block:** Defines CSS rules to style the footer and its contents.
    * `.my-custom-footer`: A custom class applied to the `BitFooter` to scope the styles. This prevents conflicts with other potential footers or global styles.
    * `.footer-content`: Styles the main content container (centering, font size, flex layout for alignment). `gap` and `flex-wrap` improve responsiveness.
    * `.footer-social-lnk-grp`: Styles the container for social links (flex layout, gap between icons).
    * `.social-lnk`: Styles individual social link containers (size, display).
    * `.social-lnk svg`: Ensures SVGs fill their container.
    * `.social-lnk svg path`: Styles the SVG icons themselves (fill color, hover effect). Using CSS variables like `var(--bit-color-primary-main)` integrates with a potential theme.
    * `.heart`: Styles the heart symbol.
2. **`<BitFooter Class="my-custom-footer">`:** Applies the custom CSS class.
3. **Internal Structure:** Uses `div` elements with corresponding classes (`footer-content`, `footer-social-lnk-grp`) to structure the content.
4. **`BitLink` Components:** Used for creating accessible hyperlinks for the social media icons.
    * `Href`: Specifies the URL.
    * `Target="_blank"`: Opens the link in a new tab.
    * `AriaLabel`: Provides accessible labels for screen readers since the links only contain icons.
5. **SVGs:** Inline SVGs are used for the icons.

## API Reference

### BitFooter Parameters

These are parameters specific to the `BitFooter` component.

| Parameter      | Type                  | Default Value | Description                                                                    |
| -------------- | --------------------- | ------------- | ------------------------------------------------------------------------------ |
| `ChildContent` | `RenderFragment?`     | `null`        | The content to be rendered inside the `BitFooter` (usually placed between tags). |
| `Height`       | `int?`                | `null`        | Sets a specific height for the `BitFooter` in pixels. If `null`, height is auto. |
| `Fixed`        | `bool`                | `false`       | If `true`, the footer uses `position: fixed` to stay fixed at the bottom of the viewport, regardless of scrolling. |

### Inherited Parameters (from `BitComponentBase`)

These parameters are inherited from the base component and provide common functionality.

| Parameter        | Type                           | Default Value                       | Description                                                                                 |
| ---------------- | ------------------------------ | ----------------------------------- | ------------------------------------------------------------------------------------------- |
| `AriaLabel`      | `string?`                      | `null`                              | The `aria-label` attribute for the root element, improving accessibility for screen readers. |
| `Class`          | `string?`                      | `null`                              | Custom CSS class(es) to apply to the root `<footer>` element.                               |
| `Dir`            | `BitDir?`                      | `null`                              | Specifies the text direction (`Ltr`, `Rtl`, `Auto`) for the component content.              |
| `HtmlAttributes` | `Dictionary<string, object>` | `new Dictionary<string, object>()`  | Allows capturing and rendering additional HTML attributes on the root `<footer>` element.      |
| `Id`             | `string?`                      | `null`                              | Sets a custom `id` attribute for the root element. If `null`, `UniqueId` might be used internally. |
| `IsEnabled`      | `bool`                         | `true`                              | Whether the component is interactive (primarily affects contained interactive elements if styled accordingly). Usually `true` for a footer. |
| `Style`          | `string?`                      | `null`                              | Custom inline CSS styles to apply to the root `<footer>` element.                           |
| `Visibility`     | `BitVisibility`                | `BitVisibility.Visible`             | Controls the visibility of the component (`Visible`, `Hidden`, `Collapsed`).                |

### Public Members (from `BitComponentBase`)

These are public members available on the component instance.

| Member        | Type               | Default Value      | Description                                                                                                |
| ------------- | ------------------ | ------------------ | ---------------------------------------------------------------------------------------------------------- |
| `UniqueId`    | `Guid`             | `Guid.NewGuid()`   | A read-only unique identifier (`Guid`) generated for each component instance. Useful for internal referencing. |
| `RootElement` | `ElementReference` | *(N/A)*            | An `ElementReference` pointing to the root DOM element (`<footer>`) of the component. Useful for JS interop. |

## Related Enums

### `BitVisibility` Enum

Defines how the component is displayed.

| Name        | Value | Description                                                                                    | CSS Equivalent         |
| ----------- | ----- | ---------------------------------------------------------------------------------------------- | ---------------------- |
| `Visible`   | `0`   | The component is rendered and visible.                                                         | `visibility: visible;` |
| `Hidden`    | `1`   | The component is hidden, but it still occupies space in the layout.                            | `visibility: hidden;`  |
| `Collapsed` | `2`   | The component is hidden and does not occupy any space in the layout (removed from flow).       | `display: none;`       |

### `BitDir` Enum

Defines the text directionality.

| Name   | Value | Description                                                                                                                                                   | HTML `dir` Attribute |
| ------ | ----- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------- |
| `Ltr`  | `0`   | Left-to-right text direction (e.g., English).                                                                                                                 | `ltr`                |
| `Rtl`  | `1`   | Right-to-left text direction (e.g., Arabic, Hebrew).                                                                                                          | `rtl`                |
| `Auto` | `2`   | The browser determines the direction based on the content. Useful for user-generated content where the language is unknown.                                     | `auto`               |

## Key Concepts

* **Content Projection:** Use `ChildContent` (typically by placing content between the `<BitFooter>` tags) to define what appears inside the footer.
* **Styling:** Apply custom styles using the `Class` or `Style` parameters. It's recommended to use the `Class` parameter with external or `<style>` block CSS for better maintainability and reusability, scoping styles with a unique class.
* **Fixed Positioning:** The `Fixed="true"` parameter is useful for footers that should always be visible at the bottom of the screen, regardless of page scroll position. Be mindful of potential content overlap issues when using fixed positioning.

## Feedback

* Provide feedback via [GitHub Issues](https://github.com/bitfoundation/bitplatform/issues/new/choose).
* Start a discussion on [GitHub Discussions](https://github.com/bitfoundation/bitplatform/discussions/new/choose).
* Review/Edit the [Demo Page Source](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Demo/Client/Bit.BlazorUI.Demo.Client.Core/Pages/Components/Layouts/Footer/BitFooterDemo.razor).
* Review/Edit the [Component Source](https://github.com/bitfoundation/bitplatform/blob/develop/src/BlazorUI/Bit.BlazorUI/Components/Layouts/Footer/BitFooter.razor).

**Explanation of the Markdown Structure and Content:**

1.  **Title:** Clear and specific (`# BitFooter Component Reference (Blazor UI)`).
2.  **Overview:** Explains the component's purpose and common uses simply.
3.  **Usage:**
    *   Starts with the most basic example for quick understanding.
    *   Includes a more complex, styled example demonstrating flexibility, complete with necessary CSS and detailed explanations of *why* certain techniques (like custom classes, `BitLink`, SVGs) are used. The CSS and CSHTML are clearly separated using language identifiers in the code blocks (`csharp` for Blazor/CSHTML, `css` for styles).
4.  **API Reference:**
    *   Separates component-specific parameters from inherited ones (`BitComponentBase`) for clarity.
    *   Uses Markdown tables for easy readability of parameters (Name, Type, Default, Description).
    *   Includes public members like `RootElement` which might be relevant for advanced scenarios (like JS interop).
5.  **Related Enums:**
    *   Defines the `BitVisibility` and `BitDir` enums used in the parameters, again using tables for structure. Added CSS/HTML attribute equivalents for better understanding.
6.  **Key Concepts:** Summarizes the most important takeaways for using the component effectively (content projection, styling methods, fixed positioning implications).
7.  **Feedback:** Includes the relevant links from the original documentation for completeness.
8.  **Markdown Formatting:** Uses headers (`#`, `##`, `###`), code blocks (```), tables (`| --- | --- |`), bold (`**`), italics (`*`), and inline code (` `` `) appropriately to structure the information and make it scannable.

This format provides a structured and detailed reference suitable for an AI agent to understand the `BitFooter` component's capabilities, parameters, and common usage patterns.
