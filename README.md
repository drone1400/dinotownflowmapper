# DinoTown Flowmapper

Open `DinoTown_Flowmapper.html` in Chrome, Edge or Firefox. It runs offline, nothing to install.

It replaces the Flowmap Generator steps from the [glitchvid guide](https://glitchvid.com/making-flowmaps-for-source/): no Hammer cleanup copy,
no Crafty, no Blender, no VTFEdit, no image editor.

## Quick guide

### 1. Open the map

Click **Open map...** and pick the map's `.vmf` (an `.obj` also works).

- The tool finds the water brushes by material and takes the water height and area from them.
  If the map has several pools, pick the right **Water material** / **Water surface**,
  or use **Draw area** to cover just one river.
- **Blocks water** is the height band above the water surface where geometry counts as an
  obstacle (default 2 to 64 units). Bridges and ceilings above the top value are ignored.
- Props are not geometry in the `.vmf`. Mark props that stand in the water with the prop tool (`R`),
  or paint blockers over them (`B`).

### 2. Place water objects

| Key | Tool          | Use                                                                      |
| --- | ------------- | ------------------------------------------------------------------------ |
| `I` | Inlet         | Where water comes from                                                   |
| `O` | Outlet        | Where it leaves                                                          |
| `P` | Push          | Click and drag to aim                                                    |
| `S` | Spinner       | For vats / whirlpools                                                    |
| `C` | Calm          | Slows water down                                                         |
| `R` | Prop          | Marks a prop that stands in the water                                    |
| `B` | Paint blocker | Paints obstacles                                                         |
| `W` | Paint water   | Paints water area                                                        |
| `E` | Erase         | Erases painting                                                          |
| `V` | Select        | Move objects; drag the square on the ring to resize, the round handle to aim |

- Push and Calm can be rectangles: pick **Rectangle** in the shape box above the map and drag
  from where the push starts to where it ends. Drag the round end handles to stretch/aim it,
  the square handle to change its width.
- Painting (`B` / `W` / `E`) has a Rectangle mode as well: drag a box to fill it.
- Every slider has a number box next to it: type a value and press Enter.

### 3. Let it settle

Wait until the status chip says **Settled, ready to export**.

The **Flowmap** view shows exactly the colours that get exported. **Water** is an animated preview.

### 4. Export

Click **Download Source pack (.zip)**. The zip contains:

| File                                 | What to do with it                                                                                                                                                            |
| ------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `materials/flowmaps/<map>_flow.vtf`  | Copy into the game's `materials` folder / pack it with the map. Foam is already in alpha and the channel directions already match Valve's water shader, so nothing needs inverting. |
| `<map>_flow.vmf`                     | Copy of the map with the water faces' texture scale and shift already set.                                                                                                    |
| `<map>_hammer_and_vmt.txt`           | The same values to type into Hammer's Face Edit Sheet, plus the VMT lines.                                                                                                    |

Add the VMT lines (`$flowmap` etc.) to the water material.

### 5. Check in game

Set `"$flow_debug" "1"` in the water material: the flowmap colours show on the water in Hammer
and in game. They should line up with the shore. Set it back to `"0"` afterwards.

- **Colours stretched or offset:** set **Water texture size** (Export section) to the real pixel
  size of the water material's `$basetexture` (or `$normalmap` if it has none), then export again.
- **Water runs the wrong way:** tick **Flip red** and/or **Flip green**, export again.

## Simulation grid size

Bigger simulation grids now flow just like small ones (v1 stalled on big grids). They take longer
to settle, so use 256-384 while placing objects and raise it for the final export if you want
smoother shorelines.

## Saving your work

**Save scene** keeps your objects and settings (as `<map>.flowscene.json`) so you can come back
later. The zip includes the scene too.

## Changelog

- **v2:** Rectangle push/calm zones, rectangle painting, typed values next to sliders,
  version shown in the header, fixed water standing still on large simulation grids
  (new multigrid pressure solver, same speed on the map at any grid size).
- **v1:** First version.

## License

MIT, see [LICENSE](LICENSE).
