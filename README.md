# Dungeon World - The Story So Far

A simple, self-contained static site intended to document a group's RPG campaign. It's tailored for Dungeon World, but it could be made to work with any RPG. It's intended to be player facing, so no DM tools like documenting fronts.

## How to Use

* Customize `src/assets/story.json` to contain the information about your campaign. See `src/schemas` for the information on how to structure this information. Samples are available in `src/assets`.
* Add all the other media assets you want. You'll have to manually insert them into the code where you want them.
* Run `npm run dev` to make sure everything looks the way you want.
* Run `npm run build` to generate the final package.
* Post the contents of the `dist` folder to a web server your players can see.
