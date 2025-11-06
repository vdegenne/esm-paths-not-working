This repository demonstrates breaking paths in `nodenext` resolution context.

There are two main issues:

### [1] - In glob context, e.g. when `"exports"` contains a path with a wild card + extension (e.g. `"./a/global/path/_.js"`), the extension is lost in the resolution:

<img width="500"  alt="image" src="https://github.com/user-attachments/assets/61d6f4f1-effc-41de-81fb-311e5702b663" />

### [2] - Another issue is that when paths contain a slash in the suggestion, selecting it will break (remove) the base dirname:

in Neovim:
<img src="https://raw.githubusercontent.com/vdegenne/esm-paths-not-working/refs/heads/main/paths_broken_screencast.gif" />

in VSCode (the paths are not even suggested...)

### Files of interest:

This repository uses a monorepo structure to emulate the issue.

- `./packages/a` represents the external module
  - its `package.json` contains an `"exports"` field interfacing modules to the world.

- `./packages/b` is the consumer and install `./packages/a` in its `"dependencies`.
  - `./packages/b/using-a-lib.ts` consumes package A public exported modules (and this is where path resolution are mostly broken)

### Additional notes

The problem occurs when `"moduleResolution"` is set to `"nodenext"` in `tsconfig.json`.
