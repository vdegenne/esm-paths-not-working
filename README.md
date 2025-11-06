This repository demonstrates breaking paths in `nodenext` resolution context.

There are two main issues:

1 - In glob context, e.g. when `"exports"` contains a path with a wild card + extension (e.g. `"./*.js"`), the extension is lost in the resolution:

<img width="500"  alt="image" src="https://github.com/user-attachments/assets/61d6f4f1-effc-41de-81fb-311e5702b663" />
