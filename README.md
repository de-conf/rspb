# rspb

rust fork of [ptpb/pb](https://pb.mgt.moe)

## TL;DR

Create a new paste from the output of cmd:

```
cmd | curl -F c=@- https://deconf.xyz/pb/
```
## Usage
### Creating pastes
```
> echo hi | curl -F c=@- https://deconf.xyz/pb/
date: 2021-01-16 03:26:09.614299435 UTC
digest: 0b8b60248fad7ac6dfac221b7e01a8b91c772421a15b387dd1fb2d6a94aee438
short: e74l
size: 3
url: https://deconf.xyz/pb/e74l
status: created
uuid: 7535e567-173f-4ba0-98ce-71cdd8f02d69
```

<form enctype="multipart/form-data">
  <label>
    <textarea placeholder='Put your paste here' id="c" name='c' rows='20' style="width: 100%; font-family: monospace; font-size: 14px" required></textarea>
  </label>
  <div style="display: flex; align-items: center">
    <input type="submit" value="Submit" formaction="https://deconf.xyz/pb/" formmethod="POST">
  </div>
</form>

### Updating pastes
```
> curl -X PUT -F c=@- deconf.xyz/pb/7535e567-173f-4ba0-98ce-71cdd8f02d69 < config.yaml

https://deconf.xyz/pb/e74l updated
```
### Using mimetypes

Append '.pdf' to hint at browsers that they should probably display a pdf document:
```
https://deconf.xyz/pb/ullp.pdf
```
### Deleting pastes
```
> curl -X DELETE deconf.xyz/pb/7535e567-173f-4ba0-98ce-71cdd8f02d69

deleted 7535e567-173f-4ba0-98ce-71cdd8f02d69
```
### Shortening URLs

```
> echo https://google.com | curl -F c=@- deconf.xyz/pb/u
date: 2021-01-16 03:29:13.865511999 UTC
digest: a1adc32c271516bfb33069304087db349649146f24744b4028d2f975697fd707
short: 1unf
size: 11
url: https://deconf.xyz/pb/1unf
status: created
uuid: b87dcc37-a4c2-4d18-a3a3-c2d875912cde
```

<form enctype="multipart/form-data">
  <label>
    <textarea placeholder='Put your url here' id="c" name='c' rows='1' style="width: 100%; font-family: monospace; font-size: 14px" required></textarea>
  </label>
  <div style="display: flex; align-items: center">
    <input type="submit" value="Submit" formaction="https://deconf.xyz/pb/u" formmethod="POST">
  </div>
</form>

### Syntax highlighting

add '.rs' to the url to highlight rust source

```
https://deconf.xyz/pb/1e6d.rs
```

### Vanity pastes

```
> echo nin | curl -F c=@- https://deconf.xyz/pb/mom
date: 2021-01-16 03:34:22.359830934 UTC
digest: e2f55e5ed88dee2a50c9bb255ad87657e7f173e2560e27ceec8b206e2bc4afaf
short: 20ko
size: 4
url: https://deconf.xyz/pb/mom
status: created
uuid: bac23f0c-0f06-4525-8ae4-624268485ef7
```

### Sunsetting pastes

```
> echo "This message will self-destruct in 5 seconds" | curl -F sunset=5 -F c=@- deconf.xyz/pb/
date: 2021-01-16 03:32:33.225306167 UTC
digest: 15cefec0e22ce1b1bfc1d06c77620cc41f8d6f1664edb023a8d63b5d0b6ef5a7
short: 19vl
size: 45
url: https://deconf.xyz/pb/19vl
status: created
uuid: 7ede8735-7af3-4ee7-87bb-fc63d2a39306
> curl https://deconf.xyz/pb/19vl
This message will self-destruct in 5 seconds
> sleep 5
> curl https://deconf.xyz/pb/19vl
expired
```

<form enctype="multipart/form-data">
  <label>
    <textarea placeholder='Put your paste here' id="c" name='c' rows='20' style="width: 100%; font-family: monospace; font-size: 14px" required></textarea>
  </label>
  <div style="display: flex; align-items: center">
  <label>Expire in (secs): </label>
    <input id="sunset" name='sunset' type='number' min='60' style="width: 20em" value='360000' step='60' required/>
    <input type="submit" value="Submit" formaction="https://deconf.xyz/pb/" formmethod="POST">
  </div>
</form>

## Deploy

Download release and then run docker-compose up
