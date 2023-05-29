# ELectron app with Vite

## Create a Vite app

Use Vite's preset as the base file structure of our project. Start with the command:
```shell
   npm create vite@latest
```

Then follow Vite's instructions

## Add Electron

Add Electron to our project.
```shell
   npm install -D electron
```

Then we create an `electron` folder in project root, and two files `main.js` and `preload.js`.

## Electron entry file

Electron needs an entry file to work, create `electron/main.js`.

The `preload.js` file will stay blank. But you probably gonna use it in a real world app.

Add it to `package.json`:
```json
   "main": "electron/main.js",
```

And add this to scripts section of `package.json`:
```json
   "electron:dev": "electron ."
```

Test your app, run Vite's dev server in a terminal instance, and Electron in another.

```shell
# First instance
   npm run dev

# Second instance
   npm run electron:dev
```

If you want to run in a single instance/command, create a new file `scripts/dev.mjs`.

And update dev script in `package.json`:
```json
   "electron:dev": "node scripts/dev.mjs"
```

You can now start dev server with a single `npm run electron:dev`.

You won't have live reload nor TypeScript for the `electron/main.js`. For that create `scripts/watch.js`.

## Building the app

Add `electron-builder` to the project:
```shell
   npm install -D electron-builder
```

And create a config file for electron-builder named `electron-builder.yaml` in project root.

Add a `base` property to Vite's config file in `vite.config.ts`.

This adds a `./` prefix on all assets, necessary to work within Electron's `file://` protocol.

Add build script to `package.json`.
```json
   "electron:build": "npm run build && electron-builder"
```

As you can see, we're gonna run Vite's build first, then electron-builder.

Vite's build is located in `dist` directory, Electron's build is located in `release` directory. Make sure to add both to `.gitignore`.

You can now build your app with the `npm run electron:build` command.