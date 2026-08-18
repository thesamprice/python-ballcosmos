## Python support for Ball Aerospace COSMOS v4

---

> **Maintained fork.** The upstream `BallAerospace/python-ballcosmos`
> repository is archived and accepts no pull requests, so this fork is the
> living home for fixes. Changes over upstream 2.0.1 (see 2.1.0):
>
> - **Binary parameters are no longer corrupted on the wire.** Bytes were
>   sent latin-1/JSON-escaped and re-materialized as UTF-8 by the server,
>   injecting 0xC2/0xC3 bytes into every payload byte >= 0x80. They are now
>   sent as COSMOS raw-byte hashes; all 256 byte values round trip losslessly
>   (verified against a live CmdTlmServer).
> - **Persistent connections stay persistent.** A reset flag was never
>   cleared, so one disconnect or transient error made every later call open
>   a new TCP connection, leaking one TIME_WAIT ephemeral port per request.
> - **Server errors surface as themselves** instead of dying in the
>   hazardous-command handler with `KeyError: '@target_name'`.
> - **`get_cmd_details(target, cmd)`**: full per-parameter metadata including
>   bit offsets (requires a server providing the method; the modernized
>   COSMOS 4 at `thesamprice/COSMOS4` does).
>
> Install: `pip install git+https://github.com/thesamprice/python-ballcosmos`


This project allows accessing the COSMOS API from the python programming language.
Additional functionality and support will be added over time.

---

Installation:
```
pip install ballcosmos
```

See the docs and examples for usage

 ## Running the test

```
$ docker-compose -f .\compose.yaml build
$ docker-compose -f .\compose.yaml up -d
Creating network "python-ballcosmos_default" with the default driver
Creating python-ballcosmos_ballcosmos_1 ... done
$ docker exec -it python-ballcosmos_ballcosmos_1 /bin/ash
/app # coverage run -m pytest ./tests/
/app # coverage report
```
