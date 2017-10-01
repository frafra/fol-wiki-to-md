# Migrazione Mediawiki a Markdown

Procedura di test per FedoraOnLine.it

```
#!/bin/bash -ex

BASE="https://doc.fedoraonline.it"
curl -sL $BASE/Special:AllPages | grep '^<li><a' | cut -d'"' -f2 | xargs -P 8 -i curl -s "$BASE{}?action=raw" -o ".{}.txt"
for file in *.txt
do
  pandoc -f mediawiki -t markdown_github "$file" -o "$(basename $file .txt).md"
done
```

