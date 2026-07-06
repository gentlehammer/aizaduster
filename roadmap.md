# Features

This file only exists as a way to keep track of the rewrite :)

## Main features

### API key enumeration

Tha basic functionality. Hits all the discovery endpoints to check for access. To be used with go:embed - new addition related to this on the section features#apilist

### Batch enum

Check multiple keys at the same time. Hopefully in this rewrite, the stuffing tricks I use will be sufficient to keep scan times from increasing by much.

### Service account existence checks

Check if default service account for proj exists for specific services.

## Subfeatures

- Skip verification
- Worker count
- Oauth screen info extraction. I'm debating whether or not I keep this, it uses Googles own API key and may be unstable...

## New features

### Tuning

Tune the worker count and all for optimal speed.

### API list

The list to get updates suggested by a scheduled Github action for up-to-date collections. Deprecations, hangs, new APIs.

### Apply referrer to all keys

Single flag to set request origin instead of only per-key 

### IAM Testpermissions endpoints

Discovery doc is a good way to check for enablement, but IAM testpermissions endpoint provides more data. Will map out the working endpoints for all of them soon.

### GCS Detection (not for v1)

This is a big one, I hope I can manage it.