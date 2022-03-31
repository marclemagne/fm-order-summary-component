# Development Log

## New technologies (for me)

- Vite
- Tailwind
- Google Fonts
- Vercel

## 3/30/22

- Captured 3 screenshots: mobile, desktop, and desktop hovering over the "Proceed to Checkout" button
  - Added them to a new `/screenshots` folder
- Added/updated the README using the template provided with the challenge
  - Wasn't able to add the preview URL yet
- Struggled getting this to deploy using Vercel. I wasn't sure what was happening but apparently two `package.json` dependencies were causing an issue on Vercel: (1) `esbuild-darwin-arm64` and (2) `fsevents`
  - The former, I guess, is to support Vite locally and the latter is not supported on Linux
  - It was pretty difficult to figure out what was going on here between Vercel's error logging and Google
  - The solution that ultimately worked was to move both of those dependencies to `optionalDependencies`
- Updated README to include Vercel preview URL: [https://fm-order-summary-component-marclemagne.vercel.app/](https://fm-order-summary-component-marclemagne.vercel.app/)

## 3/29/22

- Updated button to have a transition for the background color
- Updated "Cancel" and "Change" to be buttons instead of links to be more accessible
- Lighthouse is scoring Accessibility as a 95 (both while developing and previewing) but this because the "background and foreground colors do not have a sufficient contrast ratio." This matches the design, though, so I will ignore this for this project
  - Got this up to 98 but adding width/height attributes to `img` elements
- Did some digging into why `a` and `span` tags behave a little weirdly with Prettier. There's a Prettier option (`htmlWhitespaceSensitivity`) to modify this but this behaves kind of odd, too. Leaving the default
- For building, it seems like it's as simple as running `npm run build` which creates the site within the `/dist` folder
  - `/dist` has an `index.html` file and then an `/assets` folder which contains the styles, JavaScript, and image assets
  - You can then run `npm run preview` to preview the production build locally
  - It replaces images with built versions in the `index.html`
    - The build versions have a hash associated with them. `icon-music.svg` becomes `icon-music.80cb256f.svg`
    - What is also interesting is that the Tailwind `body` background classes do not change in the `index.html` file but when built the correct image asset references are there IN THE STYLESHEET. `pattern-background-desktop` becomes `pattern-background-desktop.756ba250.svg`

## 3/28/22

- Noticed a bug before the breakpoint where the hero image doesn't cover the entire width of the card
  - A smaller breakpoint might be useful here but want to use Tailwind's defaults
  - Changed it from defining the maximum width based on the screen size to have one maximum width and then adding a margin around the card. Not the most ideal solution but it works well enough. I could have added padding to the page itself just as easily
- Added a meta description to improve Lighthouse score (SEO is now at 100%)
- Updated Tailwind config to extend `fontFamily` to include "Red Hat Display" as a new `custom` font
  - This can be used in the code as `font-custom`
  - Updated `html, body` in `style.css` to use `@apply` now instead of "basic" CSS
- Updated Tailwind config to extend `colors` to include the color variations from the style guide
  - Then went through the markup to replace the colors I had in `style.css` with the Tailwind classes
- Did some reading on using CSS variables for colors. Looks pretty straightforward but unnecessary for this
- It looks like the drop shadow in the designs match the colors a little more but I mostly want to focus on using default Tailwind classes with some thematic updates for font/colors
  - The Tailwind config could easily be updated to include custom shadow classes, though, if I wanted to go that route

## 3/27/22

- Found and downloaded the [Order Summary Component](https://www.frontendmentor.io/challenges/order-summary-component-QlPmajDUj) challenge
- Created a new [Vite](https://vitejs.dev/guide/) project
- Created a folder in the project for the challenge files
- Added version control
- Set global default branch name to be `main`: `git config --global init.defaultBranch main`
- Changed default branch from `master` to `main`: `git branch -m main`
- Installed Tailwind CSS using this [guide](https://tailwindcss.com/docs/guides/vite)
  - I'm not using Vue or React or anything so not bothering with a `/src` folder
  - I'm not super clear how Tailwind is working. It must have something to do with Vite's development server
- Got the background image in place for desktop
  - Needed to look up how to get it to stretch across the screen. You need to use `background-size: 100% auto` which tells it to use 100% of the width and then figure out the height to maintain its aspect ratio
  - Tailwind supports this kind of oddly using arbitrary values: `bg-[length:100%_auto]`
- Started working on the card styling
  - Centering using flexbox can be tricky even when using `align/justify-items: center`
  - Make sure `html, body` is set to `100%` height
    - I created a base style for this but one can also add `h-full` to the `html` and `body` elements
    - I thought it was cleaner to add the base style
  - The container element also needs to be set to full height
  - Figuring out the right Tailwind classes to use is tricky on top of that
- Installed Prettier Tailwind plugin so it can alphabetize classes
  - Had some problem with this until I realized I installed the wrong thing. The right thing: `npm install -D prettier-plugin-tailwindcss`
- Added "Red Hat Display" from Google Fonts
- Mocked out most of the text content
- Built out plan selection area
- Added responsive classes
  - Tailwind forces you to build for the generic case and then override with responsible helpers (e.g., `sm:text-base`)
- Could not get the height of the button to match with padding
  - I could use an arbitrary value (`h-[50px]`) but I'd prefer not to
- Could not get the border radius exact with the default Tailwind classes
  - It is not far off and Tailwind provides the tools to customize this but I want to mostly use what the library provides
  - There are some exceptions--the biggest probably being the background graphic/sizing
  - Some others managing the width of the card
