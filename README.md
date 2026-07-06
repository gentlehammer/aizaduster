# Aizaduster [WIP]

Maximize recon through scanning Google API key permissions and enabled services in mere seconds. Can also recon past the scope of the key. It's pretty much magic. Supports enumeration against 400+ Google Cloud services.

This program does not take rely on any vulnerabilities*. It is an INSPECTION UTILITY, not an exploit. Pentesters and bug hunters are the intended users. More in the "NOT AN EXPLOIT" section.

> More specifically, this doesn't rely on anything that Google considers a vulnerability. The service listing is not actionable. If it finds an attack vector, that is entirely on the customer project.

The existence of an enabled service on a key does not indicate a proper vulnerability. What happens after getting your results are solely up to you.

## Usage

Blank rn. Actively rewriting. Watch / star the project for updates, and use https://github.com/bedros-p/fireblazer in the meantime. If you want the rewrite faster, pester me on twitter - https://x.com/bedros_p

## Roadmap

Version 1.0 should be capable of the following.

- Enumerate which services are enabled for the underlying project of an API key.
- Supports live / interactive view, plaintext, json, yaml with a well documented schema.
- Enumerate underlying enabled services past API key scope through default service account existence.

### Plans

#### Major Features
- Show which services require OAuth & which require Service Accounts to prevent the pentester from wasting time
- ^ Related, IAM testing on all endpoints through /iam/testPermissions would result in an even greater reduction in time necessary.
- ^ Also related, check if key is bound to service account somehow.
- ?Include flag to check for autopush, staging, preprod and -pa variations of the APIs. Only useful for testing Google owned keys, so it's kind of a personal want.

#### Patches
- Add special detection methods for the (filtered out) false positives (refer to false positives from main.go) - priority would be the GCS API.
- Sort keys by service count

#### Potential Bugs
Back in Fireblazer, if identitytoolkit is enabled but not configured, fireblazer will break on validity checking - "400, configuration not found". Critical issue... but can't reproduce since? If anyone can repro pls file an issue!


## NOT AN EXPLOIT
This program is NOT an exploit in any way.

This whole program relies on the fact that a Discovery endpoint is almost guaranteed to be there on every PUBLIC Google service endpoint, and that it still checks if the project associated with the key uses the intended service for it. This is NOT a design flaw, nor is it a problem.

Google cloud will warn you - restrict your keys. It even has a big yellow warning sign telling you to restrict it when you make it.

What this program relies on can't be avoided by any reasonable measure. If Discovery URLs didn't check for key validity, one could easily test each service with one of the actual endpoints. We do, after all, have a list of all the actual endpoints in a service. It would still show whether or not the API key is used in that project, regardless of an invalid payload to the endpoint. Checking if the endpoint payload is valid before checking for the API key is not possible, as most services tie the project data into different responses, and the project ID is inferred from the API key. It would require each service to have a rewrite of checks.
Or, they can return zero errors of use and make it silently fail, making life hell for the people that actually want to develop with GCP, in an attempt to safeguard information that doesn't pose much of a security risk. The real security risk is entirely dependent on how securely the project is set up. Just additional safeguarding that ruins DX for something that wouldn't be the root problem anyways.

## About

This project is a rewrite of my original project, Fireblazer. That tool was originally meant for enumerating Firebase projects, but the scope creep kicked in when I realized I could check for more than just Firebase. There is (going to be) a separate project, Fireblazer, which focuses entirely on Firebase project utils. If there is no such project while you are reading this *and* you are interested in it, pester me online to get it done. I am not kidding.

It is a rewrite because when I wrote Fireblazer, I was a bit rusty. The code has lots of legacy stuff jumbled in with it, making maintenance a bit hellish. I also intend on having a faster enumeration core.