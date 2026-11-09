# PREVENT-AD registered — MINC images (new LORIS API)

Aligned with `conpdatasets/preventad-registered-images-in-MINC`: same
`<candidate>/<visit>/images/*.mnc` layout and the same git-annex MD5E keys
(28,761 annexed images, 343 subjects).  Only the download URLs point to the
new instance:

```
https://registeredpreventad-new.loris.ca/api/v0.0.3/candidates/<candidate>/<visit>/images/<file>
```

`candidate.json` and `visit.json` are regular files regenerated from the
current API (the 2020 versions are not served byte-identically).

## Fetch

```bash
TOKEN=$(curl -s -X POST -H 'Content-Type: application/json' \
  -d '{"username":"<user>","password":"<password>"}' \
  https://registeredpreventad-new.loris.ca/api/v0.0.3/login \
  | python3 -c 'import json,sys;print(json.load(sys.stdin)["token"])')

git config annex.http-headers "Authorization: Bearer $TOKEN"
git annex get 5458966/NAPFU48/images      # one subject/visit
```

## Differences from the 2020 dataset

* `5443870` (32 entries) no longer exists in the new database.
* `candidate.json` / `visit.json` (1,900 files) were regenerated and are plain
  git files; they have no annex keys.

* The per-visit `images/images` files are the JSON image listing of that
  visit, regenerated from the current API and stored as regular files.
