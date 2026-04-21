## Hi, I'm Darek 👋

Senior software engineer, self-taught since 11. Nearly two decades of shipping production code across mobile, backend, and developer tooling. Now building open-source infrastructure for algorithmic trading in Rust.

**Currently:** Streaming technical analysis library → [`quantedge-ta`](https://crates.io/crates/quantedge-ta) on crates.io

---

### What I'm Building

**[quantedge-ta](https://github.com/dluksza/quantedge-ta)** — Technical analysis that takes streaming seriously.

Most TA libraries assume batch data. Real trading systems get one tick at a time. `quantedge-ta` is built for live feeds: O(1) updates, forming-bar repainting, type-safe convergence, no silent garbage values.

```rust
use quantedge_ta::{Sma, SmaConfig};
use std::num::NonZero;

let mut sma = Sma::new(SmaConfig::close(NonZero::new(20).unwrap()));

for kline in live_stream {
    if let Some(value) = sma.compute(&kline) {
        println!("SMA(20): {value}");
    }
}
```

[![crates.io](https://img.shields.io/crates/v/quantedge-ta.svg)](https://crates.io/crates/quantedge-ta)
[![docs.rs](https://docs.rs/quantedge-ta/badge.svg)](https://docs.rs/quantedge-ta)
[![CI](https://github.com/dluksza/quantedge-ta/actions/workflows/ci.yml/badge.svg)](https://github.com/dluksza/quantedge-ta/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/dluksza/quantedge-ta/branch/main/graph/badge.svg)](https://codecov.io/gh/dluksza/quantedge-ta)

---

### Background

- 🦀 **Rust** — Built trading systems across three languages (Dart → Elixir → Rust). The Dart version still runs unattended with 1yr+ uptime. Parts of the Rust version became [`quantedge-ta`](https://crates.io/crates/quantedge-ta).
- 🎓 **GSoC alumni** — Apache Cocoon, eGit (Eclipse Foundation). Eclipse Top Contributor 2011.
- 📦 **Top 10 Gerrit contributor** — Code review infrastructure behind Android, Chromium, and LibreOffice.
- 📱 **Mobile** — Flutter, React Native, Dart. Speaker at Flutter London and Confitura Warsaw (code review, 200+ audience).
- 🏢 **19 years professional** — NCDC Szczecin (6yr), CollabNet Berlin (6yr), Adaptavist London (5yr), now independent contractor.

---

### Selected Projects

| Project | Stack | Status |
|---|---|---|
| [quantedge-ta](https://github.com/dluksza/quantedge-ta) | Rust | Active, [on crates.io](https://crates.io/crates/quantedge-ta) |
| [HabitChallenge](https://habitchallenge.co/) | Flutter / Dart | 263K+ downloads, 4.7★ ([Play Store](https://play.google.com/store/apps/details?id=org.luksza.HabitChallenge&utm_source=home) · [App Store](http://apple.co/2xU40sy?pt=126711173&ct=home)) |
| [screenful](https://github.com/dluksza/screenful) | Lua / AwesomeWM | Stable, 160+ ⭐ |

---

### Writing

I write about software engineering and open source at **[luksza.org](https://luksza.org)**.

---

### Reach me

[![LinkedIn](https://img.shields.io/badge/LinkedIn-dluksza-0A66C2?style=flat&logo=linkedin)](https://linkedin.com/in/dluksza)
[![X](https://img.shields.io/badge/X-@dluksza-000000?style=flat&logo=x)](https://x.com/dluksza)
[![Blog](https://img.shields.io/badge/Blog-luksza.org-FF5722?style=flat)](https://luksza.org)

---

*London. Building things that compound.*
