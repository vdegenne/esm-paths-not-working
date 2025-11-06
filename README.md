This repository demonstrates breaking paths in `nodenext` resolution context.

There are two main issues:

## [1] - Base dirname lost when path contains slash

When paths contain a slash in the suggestion, selection will break (remove) the base dirname:

in Neovim:  
<img width=600 src="https://raw.githubusercontent.com/vdegenne/esm-paths-not-working/refs/heads/main/paths_broken_screencast.gif" />

in VSCode (the paths are not even suggested...only root files)
<img width="600"  alt="image" src="https://github.com/user-attachments/assets/b2e836c3-080b-49e8-b145-7c19bb5e1a5b" />

## [2] Extension lost in glob context

In glob context, e.g. when `"exports"` contains a path with a wild card + extension (e.g. `"./a/global/path/_.js"`), the extension is lost in the resolution:

in Neovim:  
<img width="500"  alt="image" src="https://github.com/user-attachments/assets/61d6f4f1-effc-41de-81fb-311e5702b663" />

in VSCode (same):

<img width="500" alt="image" src="https://github.com/user-attachments/assets/28cddf8f-58b2-4858-9932-cfb6fcb2b176" />

## Files of interest:

This repository uses a monorepo structure to emulate the issue.

- `./packages/a` represents the external module
  - its `package.json` contains an `"exports"` field interfacing modules to the world.

- `./packages/b` is the consumer and install `./packages/a` in its `"dependencies`.
  - `./packages/b/using-a-lib.ts` consumes package A public exported modules (and this is where path resolution are mostly broken)

## Additional notes

The problem occurs when `"moduleResolution"` is set to `"nodenext"` in `tsconfig.json`.
