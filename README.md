# Zen Glass

Translucent glass for the Zen Browser UI.

This mod has one job: make the browser chrome translucent and apply a Gaussian
blur to what sits behind it. It changes no layout, adds no scripts, and does not
touch web pages.

## What it does

- Frosted sidebar and vertical tab strip
- Frosted separate top toolbar in multi-toolbar mode
- Frosted URL bar, menus, panels, findbar and status popup
- Editable blur, saturation, tint and radius
- Respects `prefers-reduced-transparency`

## How Nebula does it

[Zen-Nebula](https://github.com/JustADumbPrsn/Zen-Nebula) is a full theme. Its
translucency comes from a small set of CSS tricks, not from JavaScript:

1. It clears the opaque window layer and paints a semi-transparent tint over it:
   `#zen-main-app-wrapper { background: rgb(255 255 255 / 20%) }`.
2. It makes the toolbar background transparent and applies
   `backdrop-filter: blur(32px) saturate(140%)` to the surfaces that should be
   frosted.
3. It uses `light-dark()` tints for light and dark mode, plus a 1px inner edge
   and a soft shadow to keep the glass readable.
4. It asks users to enable `browser.tabs.allow_transparent_browser` when they
   also want web page backgrounds to show the Zen wallpaper.

Zen Glass keeps step 1 to 3 and drops everything else. There is no page
transparency, no animations, no tab restyling and no JavaScript. If you want the
website itself to be transparent too, enable `browser.tabs.allow_transparent_browser`
in `about:config`; this mod does not depend on it.

## Install with Sine

1. Open Zen settings and go to **Sine**.
2. Use **Install from GitHub**.
3. Paste:

   ```
   https://github.com/LaloCornejo/zen-glass
   ```

4. Install and restart Zen.

Sine downloads the repository, reads `theme.json` and loads `userChrome.css`.

## Install manually

1. Open `about:support` and click **Profile Folder**.
2. Open the `chrome` folder. Create it if it does not exist.
3. Copy `userChrome.css` and the `glass` folder into `chrome/`.
4. In `about:config`, set
   `toolkit.legacyUserProfileCustomizations.stylesheets` to `true`.
5. Restart Zen.

If you already have a `userChrome.css`, do not replace it. Add this line at the
top instead:

```css
@import url("glass/glass.css");
```

Then copy the `glass` folder next to it.

## Configure

Edit `glass/config.css`:

```css
--zg-blur: 22px;          /* Gaussian blur radius */
--zg-saturation: 160%;    /* color boost */
--zg-tint-alpha: 0.38;    /* glass opacity */
--zg-light-rgb: 255 255 255;
--zg-dark-rgb: 14 14 18;
--zg-strong-alpha: 0.68;  /* URL bar, menus, findbar */
--zg-radius: var(--zen-border-radius, 12px);
```

Restart Zen after editing. For a softer look, lower `--zg-tint-alpha`. For a
heavier frost, raise `--zg-blur`.

## A note about the backdrop

A blur needs detail behind it. If your Zen theme is a flat solid color, the
glass will look like a tinted panel. Set a Zen gradient, a wallpaper image, or
use Windows Mica to see the Gaussian blur clearly.

## Requirements

- Zen Browser 1.24 or newer
- No dependencies

## Changelog

- **1.0.1** - Fix an empty glass bar on top of the page in single-toolbar mode.
- **1.0.0** - Initial release.

## License

MIT
