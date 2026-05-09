## Hi, I'm Darek 👋

I've been writing software for two decades, and shipping it for nearly that long. My code lives in Gerrit (the review infrastructure behind Android and Chromium), in 263K+ downloads HabitChallenge Android/iOS, and now in [`quantedge-ta`](https://crates.io/crates/quantedge-ta), a Rust crate for streaming technical analysis. Self-taught since 11. GSoC alumnus, Eclipse Top Contributor 2011.

**Currently:** [`quantedge`](https://github.com/dluksza/quantedge), a Rust workspace for streaming-first systematic trading. The first crate, [`quantedge-ta`](https://crates.io/crates/quantedge-ta), is on crates.io. Engine, sim, and order book are next.

**Available for Rust / Flutter contract work.** Reach me on [LinkedIn](https://linkedin.com/in/dluksza).

---

### What I'm Building

**[quantedge](https://github.com/dluksza/quantedge)** is a Cargo workspace for systematic trading in Rust. Streaming-first by design.

The thing most TA libraries get wrong: they treat the current bar as final. In live trading, the bar you care about is the one still forming, ticking second by second. `quantedge` makes that explicit in the type system. A strategy declares exactly what it reads up front, the engine surfaces only that, and tests panic loudly the moment evaluation drifts from declaration.

```rust
use quantedge_strategy::{
    EmaConfig, MarketSide, MarketSignal, MarketSignalConfig,
    MarketSnapshot, SignalGenerator, Timeframe, nz,
};

#[derive(Default)]
struct EmaCross { ema9: EmaConfig, ema21: EmaConfig }

impl SignalGenerator for EmaCross {
    fn id(&self) -> &'static str { "ema_9_21_cross" }
    fn name(&self) -> &'static str { "EMA9/EMA21 cross (H4)" }

    // Declare exactly what evaluate() will read.
    // Anything undeclared panics in tests via FakeEngine.
    fn configure<C: MarketSignalConfig>(&self, c: C) -> C {
        c.require_closed_bars(1)
            .require_timeframes(&[Timeframe::HOUR_4])
            .register(&self.ema9)
            .register(&self.ema21)
    }

    fn evaluate(&self, snap: &impl MarketSnapshot) -> Option<MarketSignal> {
        let h4 = snap.for_timeframe(Timeframe::HOUR_4);
        let prev = h4.closed(0)?;       // last closed bar
        let now  = h4.forming();        // currently-building bar

        let (p9, p21) = (prev.value(&self.ema9)?, prev.value(&self.ema21)?);
        let (n9, n21) = (now.value(&self.ema9)?, now.value(&self.ema21)?);

        (p9 <= p21 && n9 > n21).then(|| {
            MarketSignal::from_forming(self, snap, Timeframe::HOUR_4, "bull_cross")
                .with_side(MarketSide::Long)
                .add_reason("bull_cross", "EMA9 crossed above EMA21")
                .build()
        })
    }
}
```

[![crates.io](https://img.shields.io/crates/v/quantedge-ta.svg)](https://crates.io/crates/quantedge-ta)
[![downloads](https://img.shields.io/crates/d/quantedge-ta.svg)](https://crates.io/crates/quantedge-ta)
[![docs.rs](https://docs.rs/quantedge-ta/badge.svg)](https://docs.rs/quantedge-ta)
[![CI](https://github.com/dluksza/quantedge/actions/workflows/ci.yml/badge.svg)](https://github.com/dluksza/quantedge/actions/workflows/ci.yml)
[![codecov](https://codecov.io/gh/dluksza/quantedge/branch/main/graph/badge.svg)](https://codecov.io/gh/dluksza/quantedge)

---

### Background

- 🦀 **Rust today, three languages of trading-bot scar tissue.** Built the same trading system across Dart, Elixir, and Rust. The Dart version still runs unattended with 1yr+ uptime. The Rust version became [`quantedge`](https://github.com/dluksza/quantedge).
- 📦 **Contributed to Gerrit Code Review and JGit**, the code-review and Java Git stack used by Android, Chromium, and LibreOffice.
- 🎓 **GSoC alumnus.** Apache Cocoon, eGit (Eclipse Foundation). Eclipse Top Contributor 2011.
- 📱 **Mobile.** Flutter, React Native. Conference talks at [Flutter London](https://www.youtube.com/watch?v=eo84u6LmlLA) and Confitura Warsaw
---

### Selected Projects

| Project | Stack | Status |
|---|---|---|
| [quantedge](https://github.com/dluksza/quantedge) | Rust | Active workspace. First crate [`quantedge-ta`](https://crates.io/crates/quantedge-ta) on crates.io; engine/sim/order book in flight. |
| [HabitChallenge](https://habitchallenge.co/) | Flutter / Dart | 263K+ downloads, 4.7★ ([Play Store](https://play.google.com/store/apps/details?id=org.luksza.HabitChallenge) · [App Store](http://apple.co/2xU40sy)) |
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
