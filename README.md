
### My Library: 2htdp

This time I just did some really simple stuff using the 2htdp library. I looked at the sample code and, using the "planet cute" images from 2htdp/planetcute, made a little thing where the catgirl character moves across the screen for a little bit before stoping.

![](/images/secondpart.png)

```
#lang racket

(require 2htdp/universe)
(require 2htdp/image)
(require 2htdp/planetcute)

(define (stack imgs)
  (cond
    [(empty? (rest imgs)) (first imgs)]
    [else (overlay/xy (first imgs)
                      0 40
                      (stack (rest imgs)))]))

(define (main y)
  (big-bang y
            [on-tick sub1]
            [stop-when zero?]
            [to-draw draw]
            [on-key stop]))

(define MY-MAP (beside/align
                "bottom"
                (stack (list grass-block dirt-block dirt-block))
                (stack (list stone-block stone-block stone-block))
                (stack (list grass-block dirt-block dirt-block))
                water-block
                (stack (list grass-block dirt-block))
                (stack (list grass-block dirt-block dirt-block dirt-block))))

(define init 200)

(define (draw y)
  (define the-map (place-image MY-MAP (/ (image-width MY-MAP) 2) (/ (image-height MY-MAP) 2) (empty-scene 650 500)))
  (place-image character-cat-girl 
               (+ (/ (image-width character-cat-girl) 2) (- init y)) 
               (/ (image-height character-cat-girl) 2)
               the-map))
 
(define (stop y ke)
  0)

(main init)
```

