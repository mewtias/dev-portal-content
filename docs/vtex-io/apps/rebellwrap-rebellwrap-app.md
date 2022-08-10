---
title: "Ornament Shop"
slug: "rebellwrap-rebellwrap-app"
excerpt: "rebellwrap.rebellwrap-app@3.0.15"
hidden: true
createdAt: "2022-07-05T05:07:30.563Z"
updatedAt: "2022-08-08T08:07:50.082Z"
---
Ornament Shop Project working with GitFlow to manage branches and SASS to compile CSS files.

## Configuration

### First steps
- Clone this repository
- Run ```git flow init``` (accepting defaults branch names from GitFlow)
- Run ```npm install``` or ```yarn``` on the root folder to install dependencies
- Run ```npm install -g sass``` or ```yarn global add sass```

- The **react/** and **react/components/** *.css* files are in **react/styles/** and **react/styles/components/** respectively as *.scss*.
- The **styles/css/** *.css* files are in **styles/scss/** as *.scss*

#### Watching SCSS files
- After installing all dependencies and installing sass globally, run ```npm run sass``` or ```yarn run sass``` to watch your changes.