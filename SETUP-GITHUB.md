# Creating This Repo on GitHub

```
cd homelab
git init
git add .
git commit -m "Initial homelab documentation"
git branch -M main
# create an empty repo on github.com first (no README), then:
git remote add origin git@github.com:<your-username>/homelab.git
git push -u origin main
```

Your git identity is already `mrgravityrune`. The included `.gitignore` blocks `*.bin`/`*.rom` so no BIOS dumps get committed.
