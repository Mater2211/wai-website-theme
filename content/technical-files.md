---
title: "Files in Repositories"
permalink: /technical/files/
ref: /technical/files/
lang: en
# translators: # Uncomment (remove #) for translations, one - name line per translator.
# - name: Translator 1
# - name: Translator 2
# contributors:
# - name: Contributor 1
# - name: Contributor 2
github:
  repository: w3c/wai-website-theme
  path: content/technical-files.md
footer: > # Text in footer in HTML
  <p> This is the text in the footer </p>
---

{::nomarkdown}
{% include box.html type="start" title="Summary" class="" %}
{:/}

Find out the file structure in a repository:

{::nomarkdown}
{% include box.html type="end" %}
{:/}

{% include toc.html %}


## File Structure

All repositories have a common base structure with the following files
and folders. Only the bold files are expected to be edited by editors.
Files marked with a _T_ are for technical support only

-   (File, _T_) `w3c.json` – Data for the W3C API.
-   (File, _T_) `Gemfile` – A list of ruby gems that are required for the website to work.
-   (File, _T_) `Gemfile.lock` – defines which version of dependencies including gems.
-   (File, _T_) `_config.yml` – Configures the Jekyll installation, usually not touched after the initial setup.
-   (File, _T_) `_config_staging.yml` – Configures the Jekyll installation for Netlify.
-   (Folder, _T_) `_data` – Data files that are used by the theme to render the
    navigations, See 'shared files' below
    -   (File, _T_) `lang.json` – The World's Languages
    -   (File, _T_) `lang.json` – The World's Languages
    -   (File, _T_) `translations.yml` – Translations of the User Interface
    -   (File, _T_) `techniques.yml` – WCAG Techniques data (not widely used)
    -   (File, _T_) `wcag.yml` – WCAG data (not widely used)
    -   (File) `navigation.yaml` – The navigation. Add your page to the navigation to get left-side navigation and a breadcrumb.
-   (File) `README.md` – Readme of the repository. Is never rendered as an HTML file and should contain information about the repository: What is it about, where can I find background information. Includes the link to the repository preview.
-   (Folder) `content-images` – Every repository has a content-images directory that can hold assets in a sub-directory that has the name of the repository. This helps us to keep the assets of different repositories separated.
    -  (Folder) `<repo-name>`
       +  (File) `social.png` – Default social sharing image.
       +  (… Other files used by the repository …)
- (Folder) `content` – The (text) content of the repository.
  - (File) `index.md` – In most repositories content goes into the index.md file or …
  - (File) `other.md` – … other Markdown files in the main directory.

#### Shared Files

A number of files are shared between all the resources and the published site. For example theme,  translation resources and gem dependencies. Unfortunately, there is currently no way to bundle those files with the theme.

So, for now, these files are held in the [wai-website-data](https://github.com/w3c/wai-website-data) repo which is included as git submodule in all the other repositories that want to use them. The files appear in the `_external` folder. Unfortunately git submodules require several commands to ensure the latest version of these files appear in the using repository, which can cause some extra hoops to jump through.

In addition, these files are not directly used, rather the `_data` folder contains symblinks to these shared files. Again this requires extra work for setup but does alow more flexibility, such as using a local file while developing.

To summarise, the code in the resource files make references to files in `_data` folder. These are actually symblinks to files in the submodule `_external`. These files are copies of files held in the `wai-website-data` repository, at a specific version. Keeping this all up-to-date and working requires commands that need to be run as required, usually as part of a website build step, using GitHub Actions

### Notes

- In many repositories what should be in the `content` folder is still in the root folder. This should be addressed when updated. Such a change is breaking when merging to the wai-website repository.
