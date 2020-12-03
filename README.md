# FTP deploy action

Deploy files to an FTP server using GitHub actions
---

### Requirements
- You must have ftp access to your server. If your host requires ssh please use my web-deploy action (coming soon)
- Some web hosts change the default port (21), check with your host for your port number

---

### Setup Steps
1. Select the repository you want to add the action to
2. Select the `Actions` tab
3. Select `Blank workflow file` or `Set up a workflow yourself`, if you don't see these options manually create a yaml file `Your_Project/.github/workflows/main.yml`
4. Paste the example above into your yaml file and save
5. Now you need to add a key to the `secrets` section in your project. To add a `secret` go to the `Settings` tab in your project then select `Secrets`. Add a new `Secret` for `password`
6. Update your yaml file settings

---

### Settings
Keys can be added directly to your .yml config file or referenced from your project `Secrets` storage.

To add a `secret` go to the `Settings` tab in your project then select `Secrets`.
I strongly recommend you store your `password` as a secret.

---

### Inputs

### `ftp_host`

**Required** FTP host.

### `ftp_username`

**Required** FTP username.

### `ftp_password`

**Required** FTP password.

### `local_source_dir`

**Required** The local folder to copy.

### `dist_target_dir`

**Required** The remote folder.

### `delete`

Delete files not present in the local folder on the remote folder. Default `"false"`.

### `only_newer`

Download only newer files. Using time as default, see `ignore_time` option. Default `"false"`.

### `ignore_time`

Ignore time when deciding whether to download. Default `"false"`.

If you set to `"true"` the filesize will be used for deciding, this mean if you only change a typo in your document - without a change to the filesize - the file will be ignored.

### `exclude`

Ignore file(s) and/or directorie(s).

Fill an array of regex. E.g. `"'^logs/' '^README.md'"`

### `disable_ssl_certificate_verification`

Disable SSL certificate verification. Default `"true"`.

### `other_flags`

Optional, can be used to set raw string of flag(s) or option(s) for lftp eg. `"--no-empty-dirs --ascii"`, you can refer to the official docs for the full list of available flags and options. <https://lftp.yar.ru/lftp-man.html>

## Example usage

```bash
uses: cultureweb/ftp-deploy-action@v1.0.0
with:
  ftp_host: ${{ secrets.FTP_HOST }}
  ftp_username: ${{ secrets.FTP_USERNAME }}
  ftp_password: ${{ secrets.FTP_PASSWORD }}
  local_source_dir: "build"
  dist_target_dir: "www/my-app"
  delete: "true"
  exclude: "'^logs/' '^README.md'"
```
