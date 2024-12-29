---
created: 2024-12-28
modified: 2024-12-28
share: true
---
I was thoroughly inspired by [Eileen's Quartz Change Log](https://quartz.eilleeenz.com/Quartz-customization-log)and decided to do much the same. The first of which is basically the same as hers.

---
## Add Date Modified to files
Added: December 28 2024

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

This method piggybacks on the variables set by the `lastmod.ts` transformer.