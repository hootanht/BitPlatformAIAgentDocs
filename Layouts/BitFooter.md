# BitFooter Component Documentation

The **BitFooter** component is used to display a colored bar at the bottom of a site or application. It typically contains text, icons, links, or even other components. BitFooter is fully customizable with regular CSS and can be integrated into any layout.

---

## Overview

The BitFooter provides a simple way to render a footer section. It is ideal for:
- Displaying copyright or legal notices.
- Including additional links or social icons.
- Presenting a branded message (e.g., "Made with ♥ by bit platform").

The component can be styled via CSS classes, inline styles, or custom themes to match your site’s design.

---

## Usage

### 1. Basic Footer

A basic example where the footer simply displays a text message.

```razor
<div class="container">
  <footer class="bit-ftr">
    <div class="bit-ftr-gut">I'm a Footer</div>
  </footer>
</div>
```

### 2. Enhanced Footer with Social Links

This example demonstrates a more advanced usage with additional content, such as a heart symbol and social links.

```razor
<div class="container">
  <footer class="bit-ftr">
    <div class="bit-ftr-gut">
      <div class="footer-content">
        Made with <span class="text--red">♥</span> by bit platform
        <div class="footer-social-lnk-grp">
          <a class="bit-lnk" href="https://www.linkedin.com/company/bitplatformhq" target="_blank">
            <div class="social-lnk">
              <!-- LinkedIn SVG Icon -->
              <svg viewBox="0 0 32 32">
                <path d="M23.155 23.13H20.2737V18.622C20.2737 17.5464 20.2556 16.164 18.7768 16.164C17.2778 16.164 17.0488 17.3354 17.0488 18.5443V23.13H14.1702V13.8586H16.9322V15.1265H16.9725C17.3562 14.3978 18.2965 13.6289 19.6984 13.6289C22.6158 13.6289 23.1543 15.5484 23.1543 18.0453V23.13H23.155Z"></path>
              </svg>
            </div>
          </a>
          <a class="bit-lnk" href="https://github.com/bitfoundation/bitplatform" target="_blank">
            <div class="social-lnk">
              <!-- GitHub SVG Icon -->
              <svg viewBox="0 0 32 32">
                <path d="M18.5373 10.0257C17.3046 9.73929 16.0226 9.73929 14.7899 10.0257C14.078 9.58908 13.5344 9.3884 13.1391 9.30369C12.97 9.26561 12.7978 9.24767 12.6248 9.25024C12.5461 9.25237 12.4678 9.26183 12.3909 9.27848L12.38 9.28049L12.3767 9.28251H12.3737L12.5119 9.76757L12.3737 9.28352C12.3029 9.30354 12.2373 9.33883 12.1815 9.38692C12.1258 9.435 12.0812 9.49471 12.051 9.56185C11.7535 10.2281 11.6968 10.9771 11.8907 11.6806C11.3886 12.289 11.115 13.0538 11.1172 13.8427C11.1172 15.4088 11.5791 16.4616 12.3667 17.1382C12.9183 17.6122 13.5879 17.8643 14.2595 18.0085C14.1486 18.3161 14.1203 18.6418 14.1425 18.9746V19.5776C13.7321 19.6633 13.4477 19.6361 13.245 19.5696C12.9919 19.4859 12.7973 19.3175 12.6107 19.0754C12.5132 18.945 12.4223 18.8097 12.3384 18.67L12.2809 18.5763C12.2084 18.4556 12.133 18.3365 12.0551 18.2193C11.8635 17.9359 11.5791 17.5809 11.1192 17.4599L10.6311 17.3318L10.375 18.308L10.8631 18.4361C10.9438 18.4562 11.0486 18.5319 11.2211 18.785C11.2846 18.8788 11.3441 18.9766 11.4127 19.0895L11.4813 19.2005C11.576 19.3538 11.685 19.5232 11.811 19.6886C12.0661 20.0213 12.4141 20.3571 12.9304 20.5276C13.2833 20.6446 13.6847 20.6728 14.1425 20.6022V22.4849C14.1425 22.6187 14.1956 22.7469 14.2902 22.8415C14.3848 22.936 14.513 22.9892 14.6467 22.9892H18.6805C18.8142 22.9892 18.9425 22.936 19.037 22.8415C19.1316 22.7469 19.1847 22.6187 19.1847 22.4849V18.8919C19.1847 18.5742 19.1706 18.2828 19.0808 18.0115C19.7494 17.8703 20.414 17.6182 20.9626 17.1443C21.7491 16.4626 22.21 15.3997 22.21 13.8245V13.8235C22.2075 13.0411 21.9338 12.2838 21.4355 11.6806C21.6291 10.9774 21.5725 10.2288 21.2752 9.56286C21.2452 9.49564 21.2009 9.4358 21.1453 9.38754C21.0897 9.33929 21.0242 9.30378 20.9535 9.28352L20.8153 9.76757C20.9535 9.28352 20.9525 9.28352 20.9515 9.28352L20.9495 9.28251L20.9454 9.28049L20.9363 9.27848C20.9114 9.272 20.8862 9.26695 20.8607 9.26335C20.8079 9.25564 20.7547 9.25127 20.7014 9.25024C20.5284 9.24769 20.3558 9.26563 20.1871 9.30369C19.7928 9.3884 19.2492 9.58908 18.5373 10.0257Z"></path>
              </svg>
            </div>
          </a>
          <a class="bit-lnk" href="https://www.youtube.com/@bitplatform" target="_blank">
            <div class="social-lnk">
              <!-- YouTube SVG Icon -->
              <svg viewBox="0 0 32 32">
                <path d="M23.6572 11.8735C24 13.21 24 16 24 16C24 16 24 18.79 23.6572 20.1265C23.4667 20.8653 22.9095 21.4465 22.2037 21.643C20.922 22 16.5 22 16.5 22C16.5 22 12.0802 22 10.7962 21.643C10.0875 21.4435 9.531 20.863 9.34275 20.1265C9 18.79 9 16 9 16C9 16 9 13.21 9.34275 11.8735C9.53325 11.1348 10.0905 10.5535 10.7962 10.357C12.0802 10 16.5 10 16.5 10C16.5 10 20.922 10 22.2037 10.357C22.9125 10.5565 23.469 11.137 23.6572 11.8735ZM15 18.625L19.5 16L15 13.375V18.625Z"></path>
              </svg>
            </div>
          </a>
          <a class="bit-lnk" href="https://twitter.com/bitplatformhq" target="_blank">
            <div class="social-lnk">
              <!-- Twitter SVG Icon -->
              <svg viewBox="0 0 32 32">
                <path d="M22.9075 11.692C22.4053 11.9145 21.8657 12.0649 21.2985 12.1329C21.8838 11.7827 22.3216 11.2315 22.5304 10.5822C21.9805 10.9088 21.3787 11.1387 20.7511 11.2619C20.3291 10.8113 19.7701 10.5126 19.161 10.4123C18.5518 10.3119 17.9266 10.4155 17.3823 10.7069C16.8381 10.9983 16.4052 11.4612 16.151 12.0238C15.8968 12.5864 15.8355 13.2172 15.9765 13.8183C14.8623 13.7623 13.7724 13.4727 12.7774 12.9683C11.7824 12.4639 10.9046 11.7558 10.201 10.8902C9.96 11.3052 9.82202 11.7864 9.82202 12.2989C9.82175 12.7602 9.93536 13.2145 10.1528 13.6214C10.37 14.0283 10.6847 14.3753 11.0683 14.6315C10.6234 14.6173 10.1883 14.4971 9.79916 14.2808V14.3169C9.79912 14.9639 10.0229 15.5911 10.4326 16.0919C10.8424 16.5927 11.4127 16.9364 12.0469 17.0645C11.6342 17.1762 11.2014 17.1927 10.7814 17.1126C10.9603 17.6694 11.3089 18.1562 11.7783 18.505C12.2477 18.8539 12.8144 19.0471 13.3991 19.0579C12.4065 19.837 11.1807 20.2597 9.91886 20.2578C9.69533 20.2579 9.472 20.2448 9.25 20.2187C10.5309 21.0423 12.0219 21.4794 13.5447 21.4777C18.6995 21.4777 21.5175 17.2083 21.5175 13.5055C21.5175 13.3852 21.5144 13.2637 21.509 13.1434C22.0572 12.747 22.5303 12.2561 22.9063 11.6938L22.9075 11.692Z"></path>
              </svg>
            </div>
          </a>
        </div>
      </div>
    </div>
  </footer>
</div>
```

---

## API Reference

### BitFooter Parameters

| Name          | Type               | Default Value | Description                                                           |
|---------------|--------------------|---------------|-----------------------------------------------------------------------|
| **ChildContent** | `RenderFragment?` | `null`        | Specifies the content to render inside the footer.                   |
| **Height**       | `int?`          | `null`        | Sets the height of the BitFooter (in pixels).                         |
| **Fixed**        | `bool`          | `false`       | When true, the footer is rendered with a fixed position at the bottom. |

### Inherited BitComponentBase Parameters

| Name            | Type                         | Default Value                      | Description                                                                  |
|-----------------|------------------------------|------------------------------------|------------------------------------------------------------------------------|
| **AriaLabel**   | `string?`                    | `null`                             | The aria-label for accessibility.                                          |
| **Class**       | `string?`                    | `null`                             | Custom CSS class for the root element.                                     |
| **Dir**         | `BitDir?`                    | `null`                             | Specifies text direction (LTR, RTL, or Auto).                              |
| **HtmlAttributes** | `Dictionary<string, object>` | `new Dictionary<string, object>()` | Additional attributes for the root element.                                |
| **Id**          | `string?`                    | `null`                             | Custom id for the root element; if null, a unique id is generated.           |
| **IsEnabled**   | `bool`                     | `true`                             | Determines whether the component is enabled.                               |
| **Style**       | `string?`                    | `null`                             | Inline CSS styles for the root element.                                    |
| **Visibility**  | `BitVisibility`              | `BitVisibility.Visible`            | Sets the visibility state (visible, hidden, or collapsed).                   |

### Public Members

- **UniqueId:** Read-only unique identifier generated at component construction.
- **RootElement:** Reference to the root DOM element of the component.

---

## Enumerations

### BitDir Enum

| Name  | Value | Description                                                                              |
|-------|-------|------------------------------------------------------------------------------------------|
| **Ltr**  | 0     | Left-to-right text direction (e.g., English).                                          |
| **Rtl**  | 1     | Right-to-left text direction (e.g., Arabic).                                           |
| **Auto** | 2     | Automatically determines direction based on content.                                   |

### BitVisibility Enum

| Name       | Value | Description                                                      |
|------------|-------|------------------------------------------------------------------|
| **Visible**    | 0     | The component is visible.                                     |
| **Hidden**     | 1     | The component is hidden but occupies space (using CSS visibility).|
| **Collapsed**  | 2     | The component is not rendered (using CSS display: none).      |

---