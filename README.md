# SPS education platform
[![Netlify Status](https://api.netlify.com/api/v1/badges/0a282043-331d-4fdf-9976-5a8a2c20dbfc/deploy-status)](https://app.netlify.com/sites/signalprocessingsystems/deploys)
## How to get started

### GitHub
The SPS education platform is fully available on GitHub. The standard Git workflow applies. Git can be accessed through the command prompt, or more easily for beginners through `https://desktop.github.com/`. The basic workflow here will be making use of Github Desktop:
1. Install Git from `https://git-scm.com/`
2. Install Github Desktop from `https://desktop.github.com/`
3. Open the application and log in
4. (Follow a short git tutorial to get acquainted with all the different terms)
5. Go to `File -> Clone repository` and select the SPS site repository.
6. Specify a path to the location where you want to save the files and click `clone`.

The files should now have been added to your PC.

Making changes goes as follows:
1. Click the `fetch origin` button in Github Desktop to fetch the most recent version of the platform.
2. Make your changes and check them locally, following the guidelines from the next section.
3. Click `commit to master` to save your changes in Git.
4. Click `push origin` to publish them online.
5. The website will update itself after some minutes, so please check afterwards whether your changes were processed.

Ideally the use of branches is preferred, but for now it is okay to use the above guidelines.


### Hugo
It is required to run the website locally on your PC to check whether your changes did not cause any strange errors.
To do so, install Hugo version 0.62 as this version is being used currently from https://github.com/gohugoio/hugo/releases

When installed you should go to the folder where you have cloned the repository into (i.e. the folder containing the config, content, resources,... folders). In this folder open your command prompt (windows users can click in the navigation bar where the file path is and type `cmd` followed by enter). With the command prompt open, call the `hugo server` command and your site should be building locally. The prompt will also specify the address of the website, which you can acces through the browser. This is usually something like `localhost`. Changes in the files will usually automatically be processed locally. If not, try restarting the local server.


### File structure
The current file structure definitely requires still some cleaning but the most important folders are indicated here:
```
 - Config
 -- _default
 --- menus.toml    (this file specifies the menu items as visible from the home page)
 - content
 -- courses  (contains the files for the courses sections)
 -- disciplines (contains the entire curriculum)
 -- files (for all the images, pdf's etc.)
```

## Page elements
All file formats are written in the markdown language. A simple language which allows for the use of plain HTML. Usually it is the easiest to simply copy paste elements from different files into your file. The below sections will specify some common elements:

### Hyperlinks
When linking to another page on the platform the `<a>` tag can be used as
`<a href="path/to/page">text to display</a>`

Convention:
When linking to a page in the **same** folder: use relative urls
When linking to a page in a **different** folder: use absolute urls

### Latex
Latex is largely supported on the website, although sometimes the notation is a tiny bit different. Some special characters need to be escaped by adding another `\` and specialized packages are not supported.
