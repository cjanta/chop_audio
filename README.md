# chop_audio
## strudel example dnb


samples('github:switchangel/breaks')
samples('github:switchangel/pad')
samples('github:tidalcycles/uzu-drumkit')

setCps(170/60/4)

$: s("breaks/2").fit()
  .scrub(irand(16).div(16).seg(8)
  .rib("<50>", 4))
  .n(irand(2).rib(20, 1))
  .almostNever(ply("2 | 4"))
  .orbit(2).distort("2:.5")
  .gain(slider( 0.15 , 0 , 1, .05))
  ._scope()

$: s("white!8").decay(.08)
   .gain(slider(0.1 , 0 , 1 , .05))
   .almostNever(ply("2 | 4"))

const chops = [
  "0@5 0@3".add(0.5).color("teal"),
  ".16 .3 .11 .5@5".color("yellow"),
  rand.seg(8).rib(36, .5).color("orange")
]

$: s("swpad").scrub(pick(chops, "<0@2 [1@2 2@2] >"))
  .n(4).gain(slider(0.3, 0 , 1 , .1)).note("<c2@3 c3 c4>")
  .room(1).roomsize(4)
  .phaser(.4).hpf(400)
._punchcard()
$: note("<c2 g#1 f1@2>/2")
  .struct("1@5 1@3").lpenv(4).lpa(2)
  .s("supersaw")
  .lpf(100)
  .distort("2:.5")
  .gain(slider(2 , 0 , 3, 1))

all(x => x.lpf(slider(0,0,100).pow(2)))
