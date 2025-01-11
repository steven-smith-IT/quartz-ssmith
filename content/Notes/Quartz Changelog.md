---
created: 2024-12-28
modified: 2025-01-11
share: true
tags:
  - meta
---
I was thoroughly inspired by [Eilleen's Quartz Change Log](https://quartz.eilleeenz.com/Quartz-customization-log) and decided to do much the same. Hopefully this is a massive benefit to future me and a minor benefit to those who want to know what I've done to make my site look slightly different from other quartz sites.

---
## Add Recent Documents Table to front page
Added: Jan 11 2025

This change piggybacks on the [[Quartz Changelog#Add Date Modified to files|Quartz Changelog > Add Date Modified to files]] post. Its a low/no code way to do it and I really appreciate that it requires no changes to the files in obsidian.

1. I use  [Obsidian-Linter](https://github.com/platers/obsidian-linter) to create the `created` and `modified` for each.
2. I have created a dataview table using the [Obsidian Dataview Plugin](https://github.com/blacksmithgu/obsidian-dataview) that queries my library for these fields and creates a dynamic table
3. I upload my files using [Enveloppe](https://github.com/Enveloppe/obsidian-enveloppe) which automatically translates the query to a markdown table so every time I publish there is a new table generated on the index of my site. 
> [!NOTE]- Dataview Query Example
>Note: If i wanted to change this to be last modified, I could instead do `TABLE modified AS "Date Modified"`
> ```
> TABLE created AS "Date Created"
FROM -"tags"
WHERE file.name != "index" and share = true
LIMIT 5
SORT modified desc
> ```

---
## Add Date Modified to files
Added: December 28 2024

This change takes heavy inspiration from [Eilleen](https://www.stevensmith.me/Documentation/Quartz-Meta-Changelog#add-date-modified-to-files) in that I borrow her logic enitrely and just made use of some pre-existing variables that the `lastmod.ts` transformer creates.

I first added [Obsidian-Linter](https://github.com/platers/obsidian-linter) to my vault and created created a frontmatter key of `created` with the value of the file creation date as `YYYY-MM-DD` format. I then created a `modified` key with the value of files's last modified time and the same format.

I then edited the below file as such:

```tsx title="quartz/components/ContentMeta.tsx"
/* Previous lines
if (fileData.dates) {
        segments.push(<Date date={getDate(cfg, fileData)!} locale={cfg.locale} />)
      }    
*/

if (fileData.dates && fileData.slug !== "index"){
        segments.push("Created: " + fileData.dates.created.toDateString() + ", ")
        segments.push("Modified: " + fileData.dates.modified.toDateString() + " - ")
      }
```
