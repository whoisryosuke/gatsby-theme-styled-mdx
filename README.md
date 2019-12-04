<p align="center">
<a href="https://www.npmjs.com/package/gatsby-theme-styled-mdx"><img alt="npm" src="https://img.shields.io/npm/v/gatsby-theme-styled-mdx"></a>
<a href="https://github.com/whoisryosuke/gatsby-theme-styled-mdx/blob/master/LICENSE"><img alt="NPM" src="https://img.shields.io/npm/l/gatsby-theme-styled-mdx"></a>
</p>

# Gatsby Theme Styled MDX

A template to easily create landing pages or a blog using the [GatsbyJS](http://gatsbyjs.org/docs/) framework to generate a static React powered PWA. It's lightning fast, SEO friendly, and deploys directly to a CDN like Github Pages or [Netlify](http://netlify.com).

You create content your using MDX, a mix of Markdown and JSX, allowing you to import and use React components inside of your Markdown (and much more). And you can create those React components inside Storybook, an isolated development environment for coding more accessible components.

🔎 Check out the [how-to-use MDX file](https://github.com/whoisryosuke/gatsby-theme-styled-mdx-example/blob/master/content/pages/how-to-use.mdx) to see MDX in action!

## Features

- 🎛 MDX
- 🔏 Typescript
- 💄 Styled Components
- 📦 Styled System
- ⚙️ Rebass
- ☎️ SEO component
- 🐦 Twitter embeds
- 📱 PWA
- ✈️ Offline-ready
- 📇 RSS
- 📝 Setup for blogs
- 📡 Webpack aliasing
- 👕 Prettier + ESLint + Markdown Lint
- 🔌 Nodemon

# Getting Started

1. Clone the example repo: `git clone git@github.com:whoisryosuke/gatsby-theme-styled-mdx-example.git`
1. Install any dependencies: `yarn`
1. Run the development server: `yarn develop`
1. Your site should be running at: http://localhost:8000

## Manual Setup

1. Create a new Gatsby project: `npx gatsby new myproject`
2. Install the theme as a dependency: `yarn add gatsby-theme-styled-mdx`
3. Add the theme and necessary filesystem configurations to `gatsby-config.js`:

```js
module.exports = {
  plugins: [
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `content`,
        path: `${__dirname}/content/`,
      },
    },
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `content`,
        path: `${__dirname}/src/pages/`,
      },
    },
    { resolve: `gatsby-theme-styled-mdx`, options: {} },
  ],
}
```

4. Create directories that will hold your blog and page content. By default (see above filesystem paths), the theme is configured to grab MDX files from a `/content/` folder located in your project root. You can also store content in subfolders to organize it, Gatsby will search the content folder recursively.

```shell
📦
├── 📂 content
    ├── 📂 blog
        └── 📄 sample-blog.mdx
    ├── 📄 another-blog-post.mdx
    └── 📄 sample-page.mdx
├── 📂 node_modules
├── 📂 src
├── 📄 .gitignore
├── 📄 package.json
```

5. Create a test MDX file in the `/content/` directory you just made (see [Post Format](#Post+Format+%2F+Fields))
6. Start the development server: `gatsby develop`

## Configure SEO plugins

This theme comes pre-installed with SEO plugins for a site manifest, sitemap, and integrating Google Analytics.

Add the following to the plugins array of your `gatsby-config.js` and customize any values necessary:

```js
{
  resolve: `gatsby-plugin-manifest`,
  options: {
    name: 'Your Website Name',
    short_name: 'YourSite',
    start_url: '/',
    background_color: '#F5F5F5',
    theme_color: '#005CDD',
    display: 'minimal-ui',
    icon: `${__dirname}/static/assets/favicon/android-chrome-512x512.png`, // This path is relative to the root of the site.
    // icons: [
    //   {
    //     // Everything in /static will be copied to an equivalent
    //     // directory in /public during development and build, so
    //     // assuming your favicons are in /static/favicons,
    //     // you can reference them here
    //     src: `/assets/favicons/android-chrome-192x192.png`,
    //     sizes: `192x192`,
    //     type: `image/png`,
    //   },
    //   {
    //     src: `/assets/favicons/android-chrome-512x512.png`,
    //     sizes: `512x512`,
    //     type: `image/png`,
    //   },
    // ],
  },
},
{
  resolve: `gatsby-plugin-sitemap`,
  options: {
    // output: `/some-other-sitemap.xml`,
    // exclude: [`/path/to/page`, `/another/page`],
    query: `
    {
      site {
        siteMetadata {
          siteUrl
        }
      }

      allSitePage {
        edges {
          node {
            path
          }
        }
      }
  }`,
  },
},
{
  resolve: `gatsby-plugin-google-analytics`,
  options: {
    trackingId: '420',
    // Puts tracking script in the head instead of the body
    head: false,
    // Setting this parameter is optional
    anonymize: true,
    // Setting this parameter is also optional
    respectDNT: true,
  },
},
```

> For more information about each plugin and it's API, check out their Github or Gatsby documentation.

## Theme Structure

- [Frontpage](src/pages/index.js)
- [MDX Pages](src/templates/mdx-page.js)
- MDX Blog
- - [Single Blog Post](src/templates/blog-post.js)
- - [Pagination Archive](src/templates/blog-archive.js)
- Tags
- - [Single Tag Archive](src/templates/tags.js)
- - [All Tag Archives](src/pages/tags.js)

## Post Format / Fields

```markdown
---
title: Deploy a Static React Blog using GatsbyJS and Github
date: '2018-03-21'
section: blog
cover_image: './bulma-css-framework@1x.jpg'
tags:
  [
    'design',
    'development',
    'react',
    'github',
    'gatsbyjs',
    'ssg',
    'static site generator',
  ]
---

Your post here
```

- Section can be `blog` or `page`.
- Tags must be array
- Date must be in 'YYYY-MM-DD' format. If you forget to add a zero (e.g. 2019-4-20 instead of 2019-04-20) GraphQL will crash.
- Body content can include Markdown, HTML, or JSX.

> You can also use custom components in your body content, like Rebass components. You can find all these components here to reference or override: `gatsby-theme-styled-mdx/src/layouts/Theme.jsx`

## Plugins

### [Twitter](https://www.gatsbyjs.org/packages/gatsby-plugin-twitter/?=)

Seamlessly embed Tweets into posts by copying the blockquote portion of the embed code to your Markdown file. Don't copy the linked JS file, the plugin handles that automatically.

### [Manifest](https://www.gatsbyjs.org/packages/gatsby-plugin-manifest/?=)

Configure in `gatsby-config.js`.

### [RSS Feed](https://www.gatsbyjs.org/packages/gatsby-plugin-feed/?=)

Configure in `gatsby-config.js`.

## Development

This is a Gatsby theme, which works as a dependency installed on another Gatsby site. This means you have to work in an environment that supports editing relative node modules, like Yarn Workspaces. To expedite development, there is a "workspace" repo that you can clone to replicate this environment easily.

1. Clone the workspace repo: `git clone git@github.com:whoisryosuke/gatsby-theme-styled-mdx-workspace.git`
1. Clone the example repo (inside workspace folder): `git clone git@github.com:whoisryosuke/gatsby-theme-styled-mdx-example.git`
1. Clone the theme (inside workspace folder): `git clone git@github.com:whoisryosuke/gatsby-theme-styled-mdx.git`
1. Install all dependencies by running `yarn` in the workspace root.
1. Start the development server (in workspace root): `yarn develop`

> Check out [the Gatsby guide on themes](https://www.gatsbyjs.org/docs/themes/what-are-gatsby-themes/) for more information on the architecture and how to work with themes

## Deployment

### Github Pages

We locally build the files, then deploy using an NPM script that updates a specific Git repo branch called `gh-pages`.

To enable this, just initialize a git repo in the project, commit your changes, and add your Github repo as a remote repo. Make sure to label the remote as `origin`, otherwise the Gatsby deploy won't know which repo to push to.

**Deploy site to `origin` remote repo:**

`npm run deploy`

#### Creating or editing content

1. `git pull` from remote origin to ensure you have the latest posts and to merge any conflicts.
2. Add a new folder to `content/pages` or `content/blog` named after your post. This will be converted to the slug of the article -- you don't need to 'kebab-case' your title, but keep the format in mind.
3. Create a MDX file in the folder. Make sure to use previous files as a template to include all the appropriate frontmatter fields (listed above).
4. Fill out the post, optionally add a cover image (see next step for handling images)
5. For any images, include them in the same folder as the post's Markdown and link locally using `<img src="./my-image.jpg" />`. Or add them to the `/static/assets/` folder and it'll be accessible at `http://yourwebsite-or-localhost.com/assets/your-img.jpg`.
6. Run `npm run deploy` in the project root to deploy to Github Pages. Or commit code to Github's master branch to trigger a Netlify deploy.

### Netlify

This site is also capable of deploying on Netlify. Simply login to Netlify, create a new app, and point to this repository. Follow the steps, make sure Netlify is running `gatsby build` and pointing to the `/public` directory. This also allows you to use the Netlify CMS, since it requires a server for OAuth2 support and hosting on Netlify allows you re-build on each edit (rather than building from you personal machine and deploying from there).

## References

- [Example Gatsby project using theme](github.com/whoisryosuke/gatsby-theme-styled-mdx-example)
- [Development Workspace for theme](github.com/whoisryosuke/gatsby-theme-styled-mdx-workspace)

## Credits

- [GatsbyJS](http://gatsbyjs.org)
- [ReactJS](http://reactjs.org)
- [Styled Components](http://styled-components.com)
- [Styled System](https://github.com/styled-system/styled-system)
- [ryosuke-gatsby-blog](https://github.com/whoisryosuke/ryosuke-gatsby-blog/)
- [gatsby-starter-typescript-rebass-netlifycms](https://github.com/damassi/gatsby-starter-typescript-rebass-netlifycms/)
