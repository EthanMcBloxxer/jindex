# jindex

> A one-file Liquid solution to list all of the files in a directory via Jekyll and/or GitHub Pages

This is a single-file solution to indexing or listing files in a directory with Liquid, Jekyll, and/or GitHub Pages.

It was initially created for "dump" repositories, where there are a bunch of files with no relation to eachother, like if Gists were put in a single repository. All you have to do is insert the `index.html` file, configure GitHub Pages to serve your repository at `main`/`master`, and you now have all of those files hosted on GitHub Pages on the internet, for easier indexing.

**Note:** Jekyll will not actually add any files or folders that start with a period to the built site (these are called dotfiles). This is not an issue with jindex. If you wish to add these to the final built site, then you have to add

```yml
include: /
```

to a `_config.yml` file. This also won't get built with the site, but it will still stay in your repository.

## Base UI

If you want to preview jindex, a fully-built instance is available at [/jindex](https://ethanmcbloxxer.github.io/jindex/) at my website. This is hosted off of this repository.

<div align="center">

![Without Files](https://bloxxing.is-ne.at/L84Q3U.png)
*without files*

![With Files](https://bloxxing.is-ne.at/jmdusd.png)
*with files*

</div>

Custom styles can easily be added to the file, but I advise against adding seperate css files, because they will be listed by jindex itself (and because this was created to be saveable for offline usage). Just use `<style>`. If you want a dark jindex, you can put the following inside of the `<head>` element:

```html
<style>
  body         {color: #e2e2e2; background-color: #191b22;}
  a, a:visited {color: #4ea2df;}
</style>
```

The colors were taken from [Mastodon](https://joinmastodon.org/).

## How
We use Jekyll's `site.static_files` to get every non-Jekyll file and list it in a table. We then find that file's extension by doing `extension = file.extname | downcase | remove_first: '.'`. This will find the file's extension in lowercase (for if someone named their file `document.TXT`) and without a period (Jekyll returns `.TXT`). Then, we use a `case` statement to figure out what "file type" to display. After that, an `<a>` element is generated with the file's name + extension via `file.name`, and with `href="{{ file.path }}"` to link to the file. A new table definition is created with the modification time recieved from `file.modified_time`. We also have a `span` element with user select disabled to convert the file's modified date string to readable format. For the path, we make a new table definition with `file.path | remove: file.name` (to get the path without the file name). If `path` isn't equal to `/` (or root), we get the path reversed, remove the first slash (technically the last slash because we reversed the string), then reverse it again. Now, we have `/folder` if a file is at `/folder/document.txt`.

## Sitemap.xml
If you prefer raw code and an xml file that developers could use, there's also a `sitemap.xml` file that you could easily use alongside or instead of jindex itself. It isn't actively maintained, but it still works if you want a sitemap in general or wish to use an unreadable listing.

## Footer
The footer contains all necessary information for the end user as well as all information required to comply with our license (see below). The version listed is the current running version of Jekyll, which is what creates the site.

## Mobile
Mobile support isn't too great, but I find it to generally work at about 320px wide. Any wider than that and the footer may break and you may have some vertical scrolling. I guess you could just... tilt the phone, though.

## Contributing
I won't include a gigantic "contributing\.md", but keep in mind:

* Use tabs + proper indentation
* Use lowercase for HTML tags
* Use quotes for HTML attributes, Liquid tags don't matter
* Thanks for contributing
* You should (not required) make a pull request in place of an issue if possible
* Don't minify anything more than needed

## License
We're licensed under the MIT License, but if you keep the footer credit which links back to this project and my profile (as well as FontAwesome, or you may be in violation of their ToS), then you've fufilled the license and do not need to specify that the code is licensed or distribute it. This is supposed to be a single-file solution, after all.

## Grammar

### Style
jindex is preferred to be written all-lowercase, as "jindex". Even in the beginning of sentances. jindex. If it is *really* required, use "jIndex", or, if it is so required that you could die if you don't use proper punctuation, you can use "JIndex".

### Abbriviation
If you ever come a situation where you need to abbriviate jindex, you can call it "jI" or "jdex".
