# bloodhound-ce-ctl

![Python](https://img.shields.io/badge/python-3.10+-blue.svg)
![License](https://img.shields.io/badge/license-MIT-blue)

**bloodhound-ce-ctl** is a CLI management tool for [BloodHound Community Edition](https://github.com/SpecterOps/BloodHound) — built to streamline the repetitive parts of working with BloodHound CE during an engagement.

## Features

- [x] Upload BloodHound collection data (`.json` or `.zip`) via the BloodHound CE API.
- [x] Clear the BloodHound CE database and wait for readiness before re-ingesting.
- [x] Poll upload job status and automatically open your default browser with pre-loaded Cypher queries on completion.
- [x] HMAC-signed API authentication built in.

## Install

```bash
# Latest release (PyPI)
uv tool install bloodhound-ce-ctl
pipx install bloodhound-ce-ctl

# Latest commit (GitHub)
uv tool install git+https://github.com/Mojo8898/bloodhound-ce-ctl
pipx install git+https://github.com/Mojo8898/bloodhound-ce-ctl
```

## Usage

```bash
$ bloodhound-ce-ctl -h
usage: bloodhound-ce-ctl [-h] [-u URL] [-i TOKENID] [-k TOKENKEY] [-d DIR] [-z ZIPFILE] [-c] [-p]
                         [--container CONTAINER] [-v]

Python based CLI manager for BloodHound Community Edition

options:
  -h, --help            show this help message and exit
  -u URL, --url URL     BloodHound URL
  -i TOKENID, --tokenid TOKENID
                        BloodHound Token ID (default: $BH_TOKEN_ID)
  -k TOKENKEY, --tokenkey TOKENKEY
                        BloodHound Token Key (default: $BH_TOKEN_KEY)
  -d DIR, --dir DIR     Directory to scan for .json/.zip files
  -z ZIPFILE, --zip ZIPFILE
                        Single .zip file to upload
  -c, --clear           Clear all data from the database
  -p, --poll            Poll upload job status and open browser on completion
  --container CONTAINER
                        Docker container name (default: bloodhound-bloodhound-1)
  -v, --verbose         Enable verbose debug output
```

### Examples

Clear the database and re-ingest a zip file, polling until complete:
```bash
bloodhound-ce-ctl -i <token_id> -k <token_key> -c -z ./collection.zip -p
```

Ingest all `.json`/`.zip` files from a directory:
```bash
bloodhound-ce-ctl -i <token_id> -k <token_key> -d ./loot/bloodhound/
```

Clear the database only:
```bash
bloodhound-ce-ctl -i <token_id> -k <token_key> -c
```

## Configuration

Token ID and key can be generated from the BloodHound CE UI under **Administration → Manage API Tokens**. It is recommended to store them in environment variables or an alias in your `~/.zshrc` to avoid passing them on every invocation:

```bash
alias bhctl='bloodhound-ce-ctl -i $BH_TOKEN_ID -k $BH_TOKEN_KEY'
```

## Acknowledgments

- Built on top of [BloodHound Community Edition](https://github.com/SpecterOps/BloodHound) by SpecterOps
