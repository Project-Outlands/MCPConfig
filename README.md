# MCPConfig
Public facing repo for MCP SRG mappings.

This is NOT intended for end users to use. 
This is NOT a replacement for MCP.
This will NOT allow you to make Mods. DO NOT ASK.
This is ONLY inteded for making part of the process of updating MC obfusication mappings public. As well as publishing those mappings to the [Forge Maven](http://files.minecraftforge.net/maven/de/oceanlabs/mcp/mcp_config/) so that others may access them in a standard way.

You may NOT modify/rehost the mappings without express consent from either LexManos or Searge.
This is intended to prevent conflicting mappings from being published as that does nothing but hurt stability.
You MAY download our mappings from Forge's maven, and use them in your project. Just please give proper credit in some way.

You MAY make suggestions and fixes in the form of Issue reports and Pull Requests to this repo.
You may NOT make any suggestions that are derived from the offical mappings provided by Mojang as those mappings are copywritten by Mojang and we have no rights to redistribute them
There are other projects such as ForgeGradle that are designed for Modder facing development.
This is not for people who don't know what this is.

ALL RIGHTS RESERVED.

# How to Use:

This repo only builds and publishes the `mcp_config` zip (mappings metadata + patches). The patched
sources themselves are produced by the consumer (Mavenizer / ForgeDev), so everything related to
decompiling, mcinjecting or scaffolding a dev workspace has been removed from the build.

```bash
./gradlew makeZip                                   # build only -> build/distributions/mcp_config-<version>.zip

./gradlew publish \
    -PmavenUser=<user> -PmavenPassword=<token>      # publish to https://maven.outlands.top/releases

./gradlew publish -PmavenUrl=file:///tmp/mcprepo    # publish into a local directory instead
```

Versioning: every publish creates `de.oceanlabs.mcp:mcp_config:<mc>-<yyyyMMdd.HHmmss>`, so consumers
must pin an exact timestamp. Both parts can be pinned for idempotent re-runs:

```bash
./gradlew publish -PmcpTimestamp=20261022.210720            # rebuild the same version
./gradlew publish -PmcpVersion=1.12.2-20261022.210720       # pin the whole version
```

Credentials can also come from the `MAVEN_USER` / `MAVEN_PASSWORD` environment variables; publishing
to an `http(s)` repository without them fails fast instead of silently writing somewhere else.

Adding a version means adding `versions/release/<mc version>/` with `config.json`, `joined.tsrg`,
`constructors.txt`, `exceptions.txt` and `patches/`; `settings.gradle` picks it up automatically
(`-Pver=<mc version>` restricts a build to one of them).
