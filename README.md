# carp-gametime

A foundational game timing and delta-time management library for the [Carp language](https://github.com/carp-lang/Carp).

This module provides high-level abstractions for tracking frame timing, time-scaling, and FPS in real-time applications.

## Features

- **Delta Time (dt)**: Access seconds since the last frame as a float or double.
- **Time Scaling**: Effortlessly implement slow-motion or speed-up effects via `set-scale!`.
- **Pause/Unpause**: Dedicated `pause!` and `unpause!` functions for easy control.
- **FPS Tracking**: Built-in frames-per-second calculation.
- **Total Time**: Track the total elapsed time of your application.
- **Zero Overhead**: Simple struct-based tracking using nanosecond-precision system clocks.

## Design Philosophy

The Gametime module is designed for accuracy and ease of use:

1. **Precision**: Uses `System.nanotime` (Uint64) internally to avoid cumulative floating-point drift.
2. **Pragmatism**: Provides both `dt` (actual) and `scaled-dt` (adjusted by scale).
3. **Stability**: Can provide smoothed delta-time to prevent movement "stutter" caused by OS-level frame spikes.

## Installation

Add this to your project by loading `gametime.carp`.

```clojure
(load "path/to/carp-gametime/gametime.carp")
(use GameTime)
```

## Usage

```clojure
(use GameTime)

(let [clock (Clock.new)]
  (while (not (finished?))
    (do
      (Clock.tick! &clock)
      (let [dt (Clock.dt &clock)]
        (update-physics (* 10.0 dt))) ; Move 10 units per second
      (render-frame))))
```

## Running Tests

```bash
carp -x test/gametime_test.carp
```

## License

MIT
