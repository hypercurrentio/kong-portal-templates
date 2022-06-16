# Kong Developer Portal Templates

Developer Portal Template Files for Kong Enterprise Edition

>NOTE: These templates are for use with Kong Developer Portal `v1.3` and above. Please checkout https://github.com/Kong/kong-portal-templates/master-legacy for `v0.36.*` and below.

## Requirements

- [kong-portal-cli](https://github.com/kong/kong-portal-cli)

## Installation

First install the Kong Portal CLI, then follow these instructions:

```bash
$ git clone git@github.com:hypercurrentio/kong-portal-templates.git
$ cd kong-portal-templates
$ portal deploy default
```

## Configuration
### CLI CONF
Update the Kong Admin URL with your information

Path: `workspaces/<workspace-name>/cli.conf.yaml`

### Routes
You can customize your routes from this file

Path: `workspaces/<workspace-name>/router.conf.yaml`

You will see an structure like the next one: 

`/*:` the path that you can use for calling from the browser

`content/index.txt:` The configuration file that is necessary for refering to the HTML file and passing props from Kong to HTML

### Content
You can set some props to these files and using in your HTML file

Path: `workspaces/<workspace-name>/content`

```
In the example above we are using index.txt, we can take a look of the structure of these file

---
layout: homepage.html *The html file (You can find this file inside of workspaces/<workspace-name>/layouts)*

title: Home *Prop* (For using this prop inside of your html you need to use {{page.title}})

hero: *Anidated prop*
  title: Built with Kong
  tagline: Empowering developers across the globe.
---
```

### Add React's Component

For using a react component you need to have first your minified files 
* You can generate these ones from your react project with the next command:
  * `npm run build`

* You need to copy these files generated inside of 
  * `workspaces/<workspace-name>/content/themes/base/assets/js/react`

Import these files inside of your html file

```
{% layout = "layouts/_base.html" %}

{-main-}
  <div class="homepage">
    {(partials/header.html)}
    <main class="page">
      <div id="elementId" email="{{page.email}}"></app-root>
    </main>
    

    <script src="assets/js/react/js/1234-main.js" type="module"><script>
    <link rel="stylesheet" href="assets/js/react/css/1234-main.css">

    {(partials/footer.html)}
  </div>
{-main-}

```

> In the example we are sending email prop from kong to the react component




## Workspaces

Path: `workspaces/<workspace-name>`

Workspaces are a way to segment entities within Kong. Each workspace contains
one portal each with it's own content and themes.

Each Workspace follows the following structure:

- `<workspace-name>/`
  - `content/`
  - [`themes/`](#Themes)
  - [`cli.conf.yaml`](#CLI-Configuration)
  - [`portal.conf.yaml`](#Portal-Configuration)

### CLI Configuration

Path: `workspaces/<workspace-name>/cli.conf.yaml`

Workspace CLI configuration file is used by the Kong Portal CLI tool, see CLI
configuration documentation for more details.

### Portal Configuration

Path: `workspaces/<workspace-name>/portal.conf.yaml`

Workspace specific portal configuration.

Values declared here will take priority over both `theme.conf.yaml` and values
defined in your Kong `kong.conf`.

### Templates Documentation

- [Structure and Filetypes](https://docs.konghq.com/gateway/latest/developer-portal/structure-and-file-types/)
- [Working with Templates](https://docs.konghq.com/gateway/latest/developer-portal/working-with-templates/)
- [Portal CLI](https://docs.konghq.com/gateway/latest/developer-portal/helpers/cli/)

### Template Updates

To integrate updates from this repo into your portal, see the doc at [updating.md](updating.md)

## Libraries Used

- [Lua Resty Template](https://github.com/bungle/lua-resty-template)
- [Swagger UI](https://github.com/swagger-api/swagger-ui)
- [VueJS](https://vuejs.org/)
