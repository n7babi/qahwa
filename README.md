# Qahwa (قهوة)

Qahwa is a native fork of **Java 25** in which every input and every output is Arabic.

It behaves exactly like Java: same features, same semantics, same JVM. But the compiler
understands only Arabic keywords, Arabic names and Arabic-Indic digits (`٠-٩`), and everything
a program or its user can see is Arabic: compiler errors, exceptions, crash reports, `صح`/`خطأ`,
`٣٫١٤`. English Java is rejected, the same way standard Java rejects Arabic.

Qahwa is not a transpiler or a translation layer. It is a fork of `javac` and `java.base`,
packaged as its own JDK.

```
صنف مرحبا {
    عام ساكن فارغ رئيسي(نص[] معطيات) {
        نظام.خرج.اطبع("مرحبا بالعالم");
    }
}
```

(Names follow the draft glossary and may still change.)

> **Status:** early development. Nothing is usable yet. This repository currently holds the
> untouched OpenJDK 25 sources that the fork is built on.

## Commands

| Command | Java equivalent | Purpose |
|---|---|---|
| `قهوة` | `java` | Run a program |
| `اطحن` | `javac` | Compile |
| `تذوق` | `jshell` | Interactive REPL |

Source files use the `.قهوة` extension. The companion IDE, **مقهى** (Maqha), is a right-to-left
fork of Code-OSS and lives in its own repository.

## How it works

- **Compiler:** a fork of `jdk.compiler` with Arabic keywords, Arabic-Indic numerals, forgiving
  spelling (hamza forms, tashkeel and tatweel), Arabic names for the library, and every
  diagnostic translated.
- **Runtime:** a fork of the Java parts of `java.base` that makes printing, formatting, exception
  messages and stack traces Arabic.
- **Packaging:** the patched modules are combined with the stock HotSpot VM using `jlink`. The C++
  VM itself is not rebuilt yet. Inside `.class` files the JDK stays English, but no Arabic program
  can reach those names.

A later milestone renames the JDK all the way down, including the VM.

## Repository layout

```
src/java.base/       fork of java.base (Java sources)
src/jdk.compiler/    fork of javac
src/jdk.jshell/      fork of jshell
```

The first commit is the pristine import of OpenJDK 25.0.5+8 (from Eclipse Temurin's `src.zip`).
Every Qahwa change is a commit on top of it, so the fork's full diff is always one command away:

```
git diff openjdk-25.0.5+8
```

## Platforms

Windows first, then macOS.

## Contributing

The project itself (code, commits, issues, this README) is in English. Everything users see,
including the documentation, is in Arabic. Library names follow the project's master glossary.

## License

Qahwa is derived from OpenJDK and is licensed under the **GNU General Public License, version 2,
with the Classpath Exception**. See [LICENSE](LICENSE), [ASSEMBLY_EXCEPTION](ASSEMBLY_EXCEPTION)
and [ADDITIONAL_LICENSE_INFO](ADDITIONAL_LICENSE_INFO).

Java and OpenJDK are trademarks or registered trademarks of Oracle and/or its affiliates. Qahwa
is an independent project, not affiliated with or endorsed by Oracle.
