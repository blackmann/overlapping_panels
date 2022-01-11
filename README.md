# Overlapping Panels [![Pub](https://img.shields.io/pub/v/overlapping_panels.svg)](https://pub.dev/packages/overlapping_panels)

Add Discord-like navigation to your app. Demo project here: [overlapping_panels_demo](https://github.com/blackmann/overlapping_panels_demo)


<img src="https://i.ibb.co/MsBy18m/ezgif-com-gif-maker.gif" alt="Demo" height="400">


### TODO

This widget does not support navigation events yet. So pressing the back button, does not slide the `main` panel back into view. This feature will be implemented in the nearest future.

### Usage

Simple and straight to the point. Just provide usual widgets for all panels:

```dart
class _MyHomePageState extends StatelessWidget {

  @override
  Widget build(BuildContext context) {
    return Stack(
      children: [
        OverlappingPanels(
          // Using the Builder widget is not required. You can pass your widget directly. But to use `OverlappingPanelsState.of(context)` you need to wrap your widget in a Builder
          left: Builder(builder: (context) {
            return const LeftPage();
          }),
          right: Builder(
            builder: (context) => const RightPage(),
          ),
          main: Builder(
            builder: (context) {
              return const MainPage();
            },
          ),
          onSideChange: (side) {
            setState(() {
              if (side == RevealSide.main) {
                // hide something
              } else if (side == RevealSide.left) {
                // show something
              }
            });
          },
        ),
      ],
    );
  }
}
```

To be able to reveal a panel with the tap of a button, for example, do:

```dart
IconButton(
  icon: const Icon(Icons.menu),
  onPressed: () {
    // This is the main point
    OverlappingPanelsState.of(context)?.reveal(RevealSide.left);
  },
)
```