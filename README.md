# workspace-eclipse

bnd workspace for Eclipse-based OSGi development, using the latest bnd snapshot
with Eclipse feature support and Eclipse p2 repositories.

## Contents

| File | Purpose |
| --- | --- |
| `cnf/build.bnd` | Local/Release repositories, `-runee: JavaSE-21`, Git manifest headers |
| `cnf/ext/eclipse_4.41_platform.bnd` | Eclipse Platform 4.41 (R-4.41-202608281142) p2 repository |
| `cnf/ext/eclipse_4.41_simrel_2026-09.bnd` | Eclipse SimRel 2026-09 (202609091000) p2 repository |
| `cnf/ext/eclipse_4.41_*_p2.index.xml.gz` | Compressed Eclipse p2 indexes used by the indexed repositories |
| `cnf/ext/osgi-api.bnd` | Maven repository for `osgi-api.mvn` and the `${osgi.api}` macro |
| `cnf/ext/osgi-api.mvn` | Maven coordinates for the OSGi R8 API, bnd 7.4.0, and SLF4J 2.0.20 |
| `cnf/ext/java.bnd` | javac 21 |
| `LICENSE` | Eclipse Public License 2.0 (EPL-2.0) |

The Eclipse repository files are copies of the fragments in
[bndtools/workspace-templates/eclipse](https://github.com/bndtools/workspace-templates/tree/master/eclipse).
`osgi-api.mvn` is derived from
[osgi/cnf/ext/build.mvn](https://raw.githubusercontent.com/bndtools/workspace-templates/6459e763f3478b6becf78926e6ba6ac5e89837f3/osgi/cnf/ext/build.mvn).

## `${osgi.api}` macro

Puts the complete OSGi R8 API on a build path:

```
-buildpath: ${osgi.api}
```

The macro lists every individual `org.osgi.*` bundle from `osgi-api.mvn`. The
aggregate jars (`osgi.core`, `osgi.enterprise`, `osgi.annotation`,
`osgi.promise`) remain in the repository but are not part of the macro because
they duplicate the same packages. Edit `osgi-api.mvn` and the macro together.

## Eclipse repositories

Each Eclipse file defines a `P2Repository` and an `OSGiRepository`, selected by
its `indexed.*` property. Both properties are currently `true`, so the
`OSGiRepository` uses the committed compressed indexes under `cnf/ext/`. Set
`indexed.ecl-4.41` or `indexed.ecl-2026-09` to `false` to use the corresponding
`P2Repository` directly. To refresh its index, set the property to `false` and
run from the workspace root:

```
bnd repo refresh
```

## Build

Requires Java 21 and the bnd CLI with Eclipse feature support.

```
bnd build
```

## License

This workspace is licensed under EPL-2.0. See [LICENSE](LICENSE).
