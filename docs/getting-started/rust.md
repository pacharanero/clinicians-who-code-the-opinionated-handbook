# Rust

Python first. Rust second. That's the recommendation.

This chapter is for the moment when Python isn't the right tool. That moment will come, eventually, for a small fraction of what you build. When it does, Rust is a strong second choice.

## Why Rust as the second language?

A few reasons:

- **Memory safety without a garbage collector.** Rust catches whole classes of bug at compile time that other systems languages catch only at runtime, or not at all. For software that handles patient data, fewer runtime crashes is a clinical safety property.
- **Performance.** Rust is in the same league as C and C++ for raw speed, without the foot-guns. If you have a Python program that's too slow, rewriting the hot loop in Rust often gives an order-of-magnitude improvement.
- **Excellent for command-line tools.** Rust produces small, fast, statically-linked binaries. Distributing a Rust CLI is much easier than distributing a Python script with its dependencies.
- **Strong type system.** Once your code compiles, it tends to work. The compiler catches a lot of the bugs that you'd otherwise find in production.
- **Modern tooling.** `cargo` is a joy to use. Package management, building, testing, documentation generation, all integrated.

## When to reach for Rust instead of Python

- **Performance-critical code.** Anything that needs to process a lot of data quickly. Image processing, large terminology lookups, heavy numerical work.
- **System-level tooling.** A daemon, a CLI utility, a tool that needs to run on a constrained device.
- **Distributable command-line tools.** If you want clinicians to be able to download a single binary and run it, Rust is excellent for this. Python's distribution story is markedly worse.
- **WebAssembly.** If you want to run code in the browser without JavaScript, Rust compiles cleanly to WASM. Useful for clinical calculators that need to run client-side.
- **Long-lived production services where reliability matters.** Rust's compile-time guarantees pay off over years of operation.

## When NOT to use Rust

- **Prototypes.** Python wins on iteration speed. Don't reach for Rust just to feel sophisticated.
- **Anything with heavy AI/ML libraries.** The Python ML ecosystem is unmatched. Use Python and call into Rust if you need it.
- **Web applications with a small team and quick deadlines.** Django (Python) gets you to a working web app faster than any Rust framework currently does.
- **When you're learning to code.** Rust's learning curve is real. Get comfortable in Python first.

## Interoperability with Python

You don't have to choose. PyO3 lets you write Rust extensions for Python with relatively little ceremony. The pattern is:

1. Write your Python application.
2. Find the function that's too slow.
3. Rewrite that function in Rust as a Python extension.
4. Import it from Python like any other module.

This 'fast bits in Rust, glue in Python' pattern is increasingly common in scientific Python. Polars, Pydantic v2, Ruff, and many other widely-used Python libraries are Rust under the hood.

References:

- PyO3 user guide: <https://pyo3.rs/>
- Maturin (the build tool that bridges Cargo and Python packaging): <https://www.maturin.rs/>

## Distribution

A Rust CLI distributes well as a single binary per platform. The pattern I use:

- `cargo build --release` produces an optimised binary.
- GitHub Actions builds binaries for Linux, macOS, and Windows on tag push.
- Releases are attached to the GitHub release page.
- Users `curl` the binary or use `cargo install` if they have Rust.

For Python interop libraries, publish to PyPI as wheels for each supported platform. `maturin publish` does most of the work.

## Learning resources

- **The Rust Programming Language** ('the Book'): <https://doc.rust-lang.org/book/>. The official, free, well-written introduction. Read it cover to cover.
- **Rust by Example**: <https://doc.rust-lang.org/rust-by-example/>. Short runnable examples for every concept.
- **Rustlings**: <https://github.com/rust-lang/rustlings>. Small interactive exercises, like Python Koans for Rust.
- **The Rustonomicon**: only when you need it. Unsafe Rust and the dark corners. You probably don't.

## Honest expectations

Rust is harder than Python. The compiler will reject your code more often than you expect. The borrow checker, in particular, demands a way of thinking about ownership that doesn't exist in Python. Expect to feel slow for the first few weeks.

The payoff is that once it compiles, it tends to work, and it tends to keep working. For clinical code, that property is valuable.

But again: Python first. Don't add Rust to your project unless you have a specific reason that Python can't address. The mental cost of two languages in one codebase is real.
