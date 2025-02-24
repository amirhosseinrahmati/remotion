---
id: sequence
title: <Sequence />
sidebar_label: <Sequence />
---

Using a Sequence, you can time-shift certain parts of your animation and therefore make them more reusable. Sequences are also shown in the timeline and help you visually understand the structure of your video.

## API

The Sequence component is a high order component and accepts, besides it's children, the following props:

- `from` _(required)_: At which frame it's children should assume the video starts. When the sequence is at `frame`, it's children are at 0`.

- `durationInFrames` _(required)_: For how man frames the sequence should be displayed. Children are unmounted if they are not within the time range of display. If you don't want to limit the duration of the sequence, you can pass `Infinity`.

- `name` _(optional)_: You can give your sequence a name and it will be shown as the label of the sequence in the timeline of the Remotion preview. This property is purely for helping you keep track of sequences in the timeline.

:::info
Good to know: You can nest sequences within each other and they will cascade. For example, a sequence that starts at frame 60 which is inside a sequence that starts at frame 30 will have it's children start at frame 90. However, nested sequences are not currently displayed in the timeline.
:::

## Example

In the below example, you can see that the component which is wrapped inside a `<Sequence>` has gets time-shifted by 10 frames. This way you can first create the animation within `<SubComponent />` and worry about the timing of it's entrance later.

```tsx
import {useCurrentFrame} from 'remotion';

const SubComponent = () => {
  const frame = useCurrentFrame(); // 15

  return (
    <div>{frame}</div>
  );
}

const MyVideo = () => {
  const frame = useCurrentFrame() // 25

  return (
    <div>
      <Sequence from={10} durationInFrames={100} name="MySequence">
        <SubSequence />
      </Sequence>
    </div>
  );
}
```

## See also

- [Reuse components using Sequences](reusability)
