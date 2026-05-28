# Gametime Examples

## Basic Game Loop

```clojure
(use GameTime)

(defn main []
  (let [clock (Clock.new)]
    (while true
      (do
        (Clock.tick! &clock)
        (let [dt (Clock.dt &clock)]
          (update-game-logic dt))
        (render-frame)))))
```

## Slow Motion Effect

```clojure
(use GameTime)

(let [clock (Clock.new)]
  (do
    (Clock.set-scale! &clock 0.2f) ;; 20% speed
    (while in-bullet-time
      (do
        (Clock.tick! &clock)
        (let [dt (Clock.scaled-dt &clock)]
          (update-actors dt))))))
```

## Pause Logic

```clojure
(use GameTime)

(defn handle-input [clock]
  (if (paused-pressed?)
    (Clock.pause! clock)
    (Clock.unpause! clock)))
```
