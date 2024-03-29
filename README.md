# have-a-nice-day
Hey GitHub!

This repository has everyday releases where I wish you a nice day.
I do them manually.

Feel free to silence this repo in `👁 Watch` options if you don't want to receive release notifications in your GitHub dashboard.

And, most importantly, have a nice day!<br>
~ [@bswck](https://github.com/bswck)

## How I make everyday releases
First, I write down my wishes in the proper file. I commit the file and push it, tag the whole revision and release it.

```bash
echo "Hello world, have a great day!" > "$(date -I).md"
git add -A
git commit -m "$(date +%A) wishes"
git push

# Sometimes I need to overwrite a tag if I make a typo, so I use the `-f` flag by default
git tag -sfa "$(date -I)" -m "$(date +%A) wishes"
git push --tags

gh release create "$(date -I)" --notes "$(cat "$(date -I).md")"
```

The whole routine can be semi-automated:

```bash
motd_write() {
  echo "$1" > "$(date -I).md"
  git add -A
  git commit -m "$(date +%A) wishes"
  git push
}

motd_tag() {
  # Sometimes I need to overwrite a tag if I make a typo, so I use the `-f` flag by default
  git tag -sfa "$(date -I)" -m "$(date +%A) wishes"
  git push --tags
}

motd_release() {
  gh release create "$(date -I)" --notes "$(cat "$(date -I).md")"
}

motd() {
  motd_write "$1" && motd_tag && motd_release
}

# Example:
motd "Have a nice $(date +%A) everyone! 🚀"
```
