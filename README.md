## Approach

This repositary is to replicate the website  https://reboot.studio/ 

The raw code had IntersectionObserver API, upon learning and testing it in some environments, like Bolt.AI, it didn’t work like we wanted. If we use IntersectionObserver API, the context is loaded only in the current momentum of the mouse position , the pre and post context is in hidden state. Also the context became visible sentence by sentence which didn’t replicate the website. So I opted to change the way the code. 

I was observing the source code of the project with inspect to see how it is build. While inspecting the source code, I identified that the changes is done by word by word. To do that I googled and found about native browser scroll. To enable the working mechanism of the scroll I read through some documentations on how its calculated. I used chatgpt to calculate the percentage. The handleScroll function calculates the scroll percentage using the current scroll position, viewport height, and document height.  The code collects the number of words in the website, and according to the percentage of the page scrolled , the words gets visible to the user by adjusting the css. With this way I can update the CSS word by word instead of the entire sentence like in the original code of the website. 

All these developed in a svelte app. 

raw code: https://pastebin.com/mPrBHqhh
reference website: https://reboot.studio/


Everything you need to build a Svelte project, powered by [`sv`](https://github.com/sveltejs/cli).

## Creating a project

If you're seeing this, you've probably already done this step. Congrats!

```bash
# create a new project in the current directory
npx sv create

# create a new project in my-app
npx sv create my-app
```

## Developing

Once you've created a project and installed dependencies with `npm install` (or `pnpm install` or `yarn`), start a development server:

```bash
npm run dev

# or start the server and open the app in a new browser tab
npm run dev -- --open
```

## Building

To create a production version of your app:

```bash
npm run build
```

You can preview the production build with `npm run preview`.

> To deploy your app, you may need to install an [adapter](https://svelte.dev/docs/kit/adapters) for your target environment.






